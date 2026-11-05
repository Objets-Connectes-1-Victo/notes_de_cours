# 142. Convertisseur analogique-numérique (ADC) {#chapitre-adc_potentiometre_esphome}

## 142.1 Mesurer une tension

Un convertisseur analogique-numérique (ADC) mesure une tension et la transforme en valeur numérique que le programme peut lire. Il sert à lire un potentiomètre ou un capteur analogique, par exemple un capteur de lumière ou un capteur qui fournit une tension variable. Contrairement à une entrée numérique, qui indique essentiellement un état bas ou haut, l'ADC permet de suivre plusieurs niveaux de tension.

Sur le XIAO ESP32-C3, les broches analogiques exposées sont :

| Broche de la carte | GPIO | Canal ADC |
| --- | --- | --- |
| D0 / A0 | GPIO2 | ADC1_CH2 |
| D1 / A1 | GPIO3 | ADC1_CH3 |
| D2 / A2 | GPIO4 | ADC1_CH4 |
| D3 / A3 | GPIO5 | ADC2_CH0 |

Pour des mesures fiables, privilégier D0/A0, D1/A1 ou D2/A2, qui utilisent ADC1. Seeed signale que les lectures sur D3/A3 (ADC2) peuvent être perturbées. Ne jamais appliquer plus de 3,3 V à une entrée du XIAO.

## 142.2 Lire le potentiomètre

Un potentiomètre se câble comme un diviseur de tension : ses deux bornes extérieures vont à 3,3 V et GND, et sa borne centrale (curseur) à une entrée ADC compatible. La mesure ADC est une valeur numérique proportionnelle à la tension lue.

Par défaut, ESPHome utilise une atténuation de `0db`; la lecture plafonne alors autour de 1,1 V. Pour mesurer une plage de tension plus large, notamment celle d'un potentiomètre alimenté en 3,3 V, utiliser `12db`. Cette atténuation augmente la plage mesurable, mais ne permet jamais de dépasser la limite électrique de 3,3 V sur la broche. La plage réellement mesurable varie selon la puce; vérifier les valeurs obtenues et ne pas supposer que toute la plage 0–3,3 V sera mesurée sans saturation.

```yaml
sensor:
  - platform: adc
    pin: GPIO4 # À remplacer par la broche choisie pour le potentiomètre
    attenuation: 12db
    id: lecture_potentiometre
    name: "Position du potentiomètre"
    update_interval: 100ms
```

Le capteur ADC ESPHome publie une tension en volts. La valeur réellement obtenue dépend de la carte, de l'atténuation et du potentiomètre; mesurer les valeurs minimale et maximale avant de convertir cette plage en luminosité.

## 142.3 Associer la mesure à la luminosité dans Home Assistant

Une fois l'appareil ESPHome ajouté à Home Assistant, le capteur apparaît comme une entité de type `sensor` (par exemple `sensor.position_du_potentiometre`; le nom exact peut varier). Pour créer une réaction, ouvrir **Paramètres > Automatisations et scènes**, créer une automatisation et ajouter un déclencheur lié à cette entité :

* Un déclencheur **État** réagit à chaque nouvelle valeur publiée par le capteur.
* Un déclencheur **Valeur numérique** réagit lorsque la mesure franchit un seuil. Par exemple, déclencher une action lorsque la tension passe au-dessus de 2 V. Les seuils sont en volts; les choisir après avoir observé les valeurs minimale et maximale dans Home Assistant.

Pour associer la mesure à une lumière, ajouter l'action **Allumer la lumière** et sélectionner la lumière à commander. La luminosité doit être calculée à partir de la tension : utiliser les valeurs minimale et maximale observées pour faire correspondre la plage du potentiomètre à la plage de luminosité. Une automatisation déclenchée à chaque changement permet un réglage continu; un déclencheur numérique convient plutôt à une commande par seuil.

Avec un `update_interval` de 100 ms, les changements d'état peuvent arriver très souvent. Pour éviter des actions répétées ou instables, on peut arrondir la valeur lue à un multiple de 0,05 V, par exemple, pour réduire le nombre de changements d'état. Cela se fait avec un filtre dans la configuration ESPHome :

```yaml
    ...
    update_interval: 100ms
    filters:
      - round_to_multiple_of: 0.05
```

D'autres filtres sont disponibles pour lisser les mesures (ex: *moving_avg*), mais ils introduisent un délai dans la réaction. Le choix dépend de l'application et de la tolérance aux délais.

Pour envoyer à Home Assistant une valeur correspondant directement à la plage de luminosité attendue par ses actions, calibrer la tension vers une valeur de 0 à 255 :

```yaml
    ...
    update_interval: 100ms
    filters:
      - calibrate_linear:
          - 0.0 -> 0
          - 3.1 -> 255
```

Remplacer `0.0` et `3.1` par les tensions minimale et maximale mesurées. Après ce filtre, l'état du capteur n'est plus une tension en volts, mais une valeur calibrée de 0 à 255. La luminosité d'une lumière dans Home Assistant utilise cette même plage; dans une action YAML `light.turn_on`, on peut donc utiliser l'état du capteur comme valeur de `brightness`.

## 142.4 Associer la mesure à la luminosité dans ESPHome

Dans ESPHome, la luminosité d'une lumière est un nombre décimal (`float`) entre `0.0` et `1.0`. Pour commander la lumière directement depuis le potentiomètre, calibrer la tension vers cette plage, puis utiliser la valeur calibrée `x` dans l'action `on_value`. Remplacer `0.0` et `3.1` par les tensions minimale et maximale mesurées, et `del_variable` par l'identifiant de la lumière déclarée dans ESPHome.

```yaml
    ...
    update_interval: 100ms
    filters:
      - calibrate_linear:
          - 0.0 -> 0.0
          - 3.1 -> 1.0
    on_value:
      then:
        - light.turn_on:
            id: del_variable
            brightness: !lambda "return x;"
            transition_length: 0.1s
```

ESPHome anime la transition de luminosité sur 1s par défaut.  Comme nous demandons une mise à jour de la valeur au 100ms (*update_interval*), les animations s'accumulent et retardent l'utilisation de la luminosité courante. 

La valeur `transition_length` permet de réduire le délai de transition: .1s correspond au *update_interval* et assure que les animations ne s'accumulent pas.

Cette automatisation s'exécute sur l'appareil. Si Home Assistant commande aussi la même lumière, les deux commandes peuvent se remplacer; prévoir un mode qui choisit la source de commande ou désactiver temporairement l'une des deux méthodes pendant les essais.

## 142.5 Précautions

* Ne jamais dépasser 3,3 V sur une broche du XIAO ESP32-C3.
* Confirmer que la broche choisie est une entrée ADC compatible et ne pas la partager avec la sortie PWM.
* Utiliser une résistance en série avec la DEL et vérifier le câblage hors tension.

## 142.6 Références

* [Capteur ADC ESPHome](https://esphome.io/components/sensor/adc/)
* [Brochage du XIAO ESP32-C3 (Seeed Studio)](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)
