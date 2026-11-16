# 148. Capteur de température et automatisation sur seuil {#chapitre-capteur_temperature_esphome}

## 148.1 Choisir et câbler le capteur

Un capteur de température externe mesure la température de son environnement. Il ne faut pas le confondre avec `internal_temperature`, qui mesure la puce du microcontrôleur et ne représente pas la température de la pièce.

Avant le branchement, lire le modèle inscrit sur le composant ou son module et vérifier sa fiche technique. Le protocole, le brochage, la tension d'alimentation et la configuration ESPHome varient selon le modèle. L'exemple de cette fiche utilise un DHT11, qui mesure la température et l'humidité. Un DS18B20 ou un autre modèle demande une plateforme et un câblage différents.

Pour le DHT11 classique à quatre broches, placer la grille face à soi et les broches vers le bas : de gauche à droite, elles sont généralement **VCC, DATA, NC, GND**. `NC` (« non connecté ») reste inutilisée. Raccorder VCC à 3,3 V, GND à la masse et DATA à une broche GPIO libre. La ligne de données nécessite généralement une résistance de rappel d'environ 4,7 kΩ entre DATA et 3,3 V. Vérifier si le capteur ou son module possède déjà cette résistance. Certains modules ont trois broches et un ordre différent : suivre leurs inscriptions et leur fiche technique plutôt que de supposer le brochage.

![dh11](https://www.circuitbasics.com/wp-content/uploads/2015/12/DHT11-Pinout-for-three-pin-and-four-pin-types-2-1024x742.jpg)

Le DHT11 communique avec le microcontrôleur par un protocole numérique propriétaire à un seul fil de données, avec des impulsions dont la durée représente les bits. Une lecture transmet une trame de 40 bits : humidité entière, humidité décimale, température entière, température décimale et somme de contrôle. Ce protocole n'est pas le bus Dallas `one_wire` du DS18B20, même si les deux utilisent une ligne de données. ESPHome gère le signal et ses timings avec `platform: dht`.

!!! warning

    Couper l'alimentation avant de modifier le câblage. Vérifier le brochage du modèle exact et ne jamais appliquer 5 V à une entrée du XIAO ESP32-C3. Ne pas se fier uniquement à la couleur des fils d'une sonde.

## 148.2 Déclarer un DHT11 dans ESPHome

La plateforme `dht` permet de publier les mesures du DHT11. Dans l'exemple, la ligne DATA est raccordée à `GPIO4`. La configuration avancée de `pin` désactive le pull-up interne, car le module possède déjà sa résistance de rappel externe :

```yaml
sensor:
  - platform: dht
    pin:
      number: GPIO4
      mode:
        input: true
        pullup: false # La résistance de rappel est déjà présente sur le module
    model: DHT11
    update_interval: 10s
    temperature:
      name: "Température ambiante"
      id: temperature_ambiante
      unit_of_measurement: "°C"
      accuracy_decimals: 0
    humidity:
      name: "Humidité ambiante"
      accuracy_decimals: 0
```

La déclaration `platform: dht` lit le capteur; `model: DHT11` indique explicitement son modèle. Les sections `temperature` et `humidity` créent chacune une entité numérique. La mesure d'humidité est facultative : elle peut être omise si seul le capteur de température est requis. Un intervalle de 10 secondes respecte le rythme de lecture du DHT11 et évite de l'interroger inutilement souvent. `pullup: false` désactive seulement la résistance interne de la broche; la résistance physique du module reste raccordée entre DATA et 3,3 V.

Dans les exercices précédents, le bouton utilisait `GPIO4`. Pour réserver cette broche au DHT11 dans l'exercice, déplacer le bouton vers une broche libre compatible et modifier sa configuration en conséquence.

Ne pas ajouter ce fragment comme un second bloc `sensor:` s'il en existe déjà un : ajouter plutôt la déclaration `- platform: dht` sous le bloc existant, avec la même indentation que les autres capteurs. Conserver les autres sections de la configuration.

Après compilation et installation, vérifier dans les journaux que le capteur est détecté et qu'il publie une valeur plausible. L'entité de température est ensuite disponible dans Home Assistant; l'ajouter au tableau de bord pour observer ses mises à jour.

### Dépannage de base

* **La lecture échoue ou les journaux signalent des valeurs invalides :** vérifier le modèle, le brochage, le GND commun, la broche choisie et la résistance de rappel de DATA. Garder les fils courts et essayer le réglage `pullup: false` sous `pin` si le module possède déjà sa résistance de rappel.
* **La compilation échoue :** vérifier la plateforme correspondant au modèle et l'indentation YAML; `dht` doit contenir les sections `temperature` et, facultativement, `humidity`.
* **La valeur est indisponible ou peu plausible :** consulter les journaux, vérifier le câblage et comparer avec un thermomètre de référence. Le DHT11 a une précision et une résolution modestes; tenir compte de son temps de réponse et de son emplacement.
* **La température de la puce diffère :** c'est normal; `internal_temperature` ne mesure pas l'air ambiant.

## 148.3 Automatiser avec un seuil dans Home Assistant

Un déclencheur d'état numérique peut démarrer une automatisation Home Assistant lorsque la température franchit une limite. Par exemple, on peut allumer une lumière lorsque la mesure passe au-dessus d'un seuil choisi. Le nom de l'entité doit être celui de l'appareil réel; il ne faut pas présumer qu'il s'appelle exactement `sensor.temperature_ambiante`.

Dans l'éditeur d'automatisations de Home Assistant :

1. Ajouter un déclencheur **État numérique** et sélectionner le capteur de température.
1. Saisir une limite supérieure adaptée au test, par exemple `26 °C`.
1. Ajouter une action, par exemple allumer la lumière ESPHome.
1. Enregistrer, puis consulter la trace de l'automatisation pour vérifier le déclencheur et l'action.

Un déclencheur numérique se produit lorsque la mesure **franchit** la limite, et non continuellement pendant qu'elle reste au-dessus. Si la température est déjà au-dessus de la limite lorsque l'automatisation est créée, elle ne se déclenche pas avant un nouveau franchissement. Une seconde automatisation avec une limite de retour plus basse (par exemple allumer au-dessus de 26 °C et éteindre sous 24 °C) crée une hystérésis simple et évite les changements répétés autour d'une seule limite.

Cette automatisation est exécutée par Home Assistant : elle dépend donc du serveur et de la communication avec l'appareil. Le capteur continue d'être lu par l'ESP32 même si Home Assistant est temporairement indisponible, mais cette automatisation ne peut alors ni s'exécuter ni commander la lumière.

!!! note

    Une automatisation de cours qui commande une lumière n'est pas un dispositif de sécurité thermique. Ne pas utiliser ce montage pour protéger une personne, un appareil ou un bâtiment contre la surchauffe.

## Références

* [Capteur de température et d'humidité DHT ESPHome](https://esphome.io/components/sensor/dht/)
* [Déclencheur numérique Home Assistant](https://www.home-assistant.io/docs/automation/trigger/#numeric-state-crossed-threshold-trigger)
* [Capteur de température interne ESPHome](https://esphome.io/components/sensor/internal_temperature/)
