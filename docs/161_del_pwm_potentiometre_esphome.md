# 141. Modulation de largeur d'impulsions (PWM) {#chapitre-del_pwm_potentiometre_esphome}

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
    pin: GPIO5 # À remplacer par la broche choisie pour la DEL
    # Fréquence du signal PWM - 1000 Hz par défaut
    # frequency: 1000 Hz
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

## Références

* [Sortie LEDC ESPHome](https://esphome.io/components/output/ledc/)
* [Lumière monochrome ESPHome](https://esphome.io/components/light/monochromatic/)
* [Brochage du XIAO ESP32-C3 (Seeed Studio)](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)
