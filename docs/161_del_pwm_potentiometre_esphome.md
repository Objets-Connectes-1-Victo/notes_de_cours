# 141. Contrôler l'intensité d'une DEL avec un potentiomètre {#chapitre-del_pwm_potentiometre_esphome}

## 141.1 Modulation de largeur d'impulsions {#fiche-pwm}

Une sortie PWM (modulation de largeur d'impulsions) commute rapidement entre les états bas et haut. En variant la proportion du temps passé à l'état haut, ESPHome peut régler la luminosité moyenne d'une DEL. Sur ESP32, la plateforme de sortie `ledc` génère le signal PWM.

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

Utiliser une broche différente de celle réservée au potentiomètre et vérifier le brochage du XIAO ESP32-C3. La DEL doit rester protégée par une résistance en série.

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

## Associer la mesure à la luminosité

Pour commander la lumière directement depuis le potentiomètre, une action déclenchée par la mise à jour du capteur peut appeler `light.turn_on`. La valeur mesurée doit être normalisée en luminosité entre 0 et 1, puis limitée à cette plage. Une lambda ESPHome peut effectuer ce calcul; la fiche sur les templates et lambdas approfondira cette syntaxe.

La lumière demeure aussi disponible dans Home Assistant. On peut ainsi comparer le réglage local par potentiomètre à celui fait avec la commande de luminosité dans le tableau de bord.

## Précautions

* Ne jamais dépasser 3,3 V sur une broche du XIAO ESP32-C3.
* Confirmer que la broche choisie est une entrée ADC compatible et ne pas la partager avec la sortie PWM.
* Utiliser une résistance en série avec la DEL et vérifier le câblage hors tension.

## Références

* [Sortie LEDC ESPHome](https://esphome.io/components/output/ledc/)
* [Lumière monochrome ESPHome](https://esphome.io/components/light/monochromatic/)
* [Capteur ADC ESPHome](https://esphome.io/components/sensor/adc/)