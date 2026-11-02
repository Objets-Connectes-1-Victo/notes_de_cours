# 141. Contrôler l'intensité d'une DEL avec un potentiomètre {#chapitre-del_pwm_potentiometre_esphome}

## 141.1 Modulation de largeur d'impulsions {#fiche-pwm}

Une sortie PWM (modulation de largeur d'impulsions) commute rapidement entre les états bas et haut. Elle ne produit donc pas une tension qui augmente graduellement : elle envoie une suite d'impulsions numériques. En variant la proportion du temps passé à l'état haut, ESPHome règle la luminosité moyenne d'une DEL. Sur ESP32, la plateforme de sortie `ledc` génère le signal PWM.

### Rapport cyclique (duty cycle)

Le rapport cyclique est la fraction de chaque période pendant laquelle le signal reste à l'état haut. Il se calcule ainsi :

```text
rapport cyclique = durée à l'état haut / durée d'une période × 100 %
```

Par exemple, si le signal est à l'état haut pendant la moitié de chaque période, son rapport cyclique est de 50 %. La DEL est alors alimentée pendant la moitié du temps et paraît moins lumineuse que lorsqu'elle reste allumée en continu. À 0 %, elle est toujours éteinte; à 100 %, elle est toujours allumée. Entre ces deux valeurs, le rapport cyclique détermine le temps d'allumage de la DEL.

La fréquence indique combien de périodes sont produites par seconde. Elle est distincte du rapport cyclique : on peut garder la même fréquence et modifier le rapport cyclique pour changer l'intensité, ou garder le même rapport cyclique et modifier la fréquence. La commutation est généralement assez rapide pour que l'œil perçoive une luminosité stable plutôt qu'un clignotement. La luminosité perçue n'est toutefois pas nécessairement proportionnelle au rapport cyclique, car la perception visuelle n'est pas linéaire.

Le PWM sert notamment à faire varier l'intensité d'une DEL ou d'une bande lumineuse et à régler la vitesse d'un moteur à courant continu. Un moteur demande plus de courant que la broche d'un ESP32 ne peut fournir : il faut utiliser un pilote de moteur ou un transistor adapté, avec une alimentation appropriée. Un servomoteur se commande aussi avec un signal en impulsions, mais c'est principalement la durée de l'impulsion qui indique la position demandée; il doit être alimenté et raccordé selon les exigences de son modèle.

La lumière monochrome reprend la sortie PWM comme canal de luminosité :

```yaml
output:
  - platform: ledc
    pin: GPIO5
    id: sortie_del_pwm

light:
  - platform: monochromatic
    output: sortie_del_pwm
    name: "DEL à intensité variable"
    id: del_variable
```

Toutes les broches GPIO exposées du XIAO ESP32-C3 peuvent servir de sortie PWM avec `ledc`; il n'y a pas de broche PWM dédiée. Choisir une broche qui n'est pas déjà utilisée par un autre composant et vérifier que son circuit ne perturbe pas le démarrage de la carte.

### Commander la lumière depuis Home Assistant

Après avoir installé la configuration sur l'ESP32 et ajouté l'appareil ESPHome à Home Assistant, l'entité de lumière déclarée dans le bloc `light` apparaît sous le nom « DEL à intensité variable ». Dans le tableau de bord, modifier une carte existante ou en ajouter une de type **Lumière**, puis sélectionner cette entité. Son curseur permet de régler la luminosité; la commande est envoyée à l'ESP32, qui ajuste le rapport cyclique du signal PWM.



## Convertisseur analogique-numérique (ADC)

Un convertisseur analogique-numérique (ADC) mesure une tension et la transforme en valeur numérique que le programme peut lire. Il sert à lire un potentiomètre ou un capteur analogique, par exemple un capteur de lumière ou un capteur qui fournit une tension variable. Contrairement à une entrée numérique, qui indique essentiellement un état bas ou haut, l'ADC permet de suivre plusieurs niveaux de tension.

Sur le XIAO ESP32-C3, les broches analogiques exposées sont :

| Broche de la carte | GPIO | Canal ADC |
| --- | --- | --- |
| D0 / A0 | GPIO2 | ADC1_CH2 |
| D1 / A1 | GPIO3 | ADC1_CH3 |
| D2 / A2 | GPIO4 | ADC1_CH4 |
| D3 / A3 | GPIO5 | ADC2_CH0 |

Pour des mesures fiables, privilégier D0/A0, D1/A1 ou D2/A2, qui utilisent ADC1. Seeed signale que les lectures sur D3/A3 (ADC2) peuvent être perturbées. Ne jamais appliquer plus de 3,3 V à une entrée du XIAO. Les valeurs mesurées dépendent aussi de la carte et de sa configuration; vérifier la plage réelle avant de l'utiliser dans un calcul.

## Lire le potentiomètre

Un potentiomètre se câble comme un diviseur de tension : ses deux bornes extérieures vont à 3,3 V et GND, et sa borne centrale (curseur) à une entrée ADC compatible. La mesure ADC est une valeur numérique proportionnelle à la tension lue.

```yaml
sensor:
  - platform: adc
    pin: GPIO4
    id: lecture_potentiometre
    name: "Position du potentiomètre"
    update_interval: 100ms
```

Le capteur ADC ESPHome publie une tension en volts. La valeur réellement obtenue dépend de la carte, de l'atténuation et du potentiomètre; mesurer les valeurs minimale et maximale avant de convertir cette plage en luminosité.


### Réagir à un changement dans Home Assistant

Une fois l'appareil ESPHome ajouté à Home Assistant, le capteur apparaît comme une entité de type `sensor` (par exemple `sensor.position_du_potentiometre`; le nom exact peut varier). Pour créer une réaction, ouvrir **Paramètres > Automatisations et scènes**, créer une automatisation et ajouter un déclencheur lié à cette entité :

* Un déclencheur **État** réagit à chaque nouvelle valeur publiée par le capteur. Ajouter ensuite une action, par exemple envoyer une notification ou commander une autre lumière.
* Un déclencheur **Valeur numérique** réagit lorsque la mesure franchit un seuil. Par exemple, déclencher une action lorsque la tension passe au-dessus de 2 V. Les seuils sont en volts; les choisir après avoir observé les valeurs minimale et maximale dans Home Assistant.

Avec un `update_interval` de 100 ms, les changements d'état peuvent arriver très souvent. Pour éviter des actions répétées ou instables, préférer un seuil numérique, éventuellement avec une durée minimale, plutôt qu'une action à chaque lecture. Éviter aussi de commander la même lumière à la fois depuis une automatisation Home Assistant et depuis une action ESPHome déclenchée par chaque lecture du potentiomètre.


## Associer la mesure à la luminosité

Pour commander la lumière directement depuis le potentiomètre, une action déclenchée par la mise à jour du capteur peut appeler `light.turn_on`. La valeur mesurée doit être normalisée en luminosité entre 0 et 1, puis limitée à cette plage. Une lambda ESPHome peut effectuer ce calcul; la fiche sur les templates et lambdas approfondira cette syntaxe.



On peut ainsi comparer le réglage depuis Home Assistant à celui du potentiomètre. Toutefois, si l'automatisation met à jour la lumière à chaque nouvelle lecture du potentiomètre, elle peut remplacer presque immédiatement le réglage fait dans le tableau de bord. Pour tester la commande Home Assistant seule, désactiver temporairement cette automatisation ou prévoir un mode qui choisit la source de commande.

## Précautions

* Ne jamais dépasser 3,3 V sur une broche du XIAO ESP32-C3.
* Confirmer que la broche choisie est une entrée ADC compatible et ne pas la partager avec la sortie PWM.
* Utiliser une résistance en série avec la DEL et vérifier le câblage hors tension.

## Références

* [Sortie LEDC ESPHome](https://esphome.io/components/output/ledc/)
* [Lumière monochrome ESPHome](https://esphome.io/components/light/monochromatic/)
* [Capteur ADC ESPHome](https://esphome.io/components/sensor/adc/)
* [Brochage du XIAO ESP32-C3 (Seeed Studio)](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)