# 139. Lire un bouton : actions et rebond mécanique {#chapitre-bouton_actions_rebond_esphome}

## 139.1 Lire un bouton avec une entrée GPIO {#fiche-entree_gpio}

Un bouton poussoir peut être lu avec une entrée numérique. Le montage ci-dessous utilise la résistance de rappel interne du XIAO ESP32-C3 : le bouton relie la broche GPIO4 à GND lorsqu'on appuie.

```text
GPIO4 (D2) ---- bouton poussoir ---- GND
```

Avec la résistance de rappel (`pullup`), l'entrée est normalement à l'état haut. L'appui la relie à GND; `inverted: true` fait correspondre cet état bas à l'état logique « activé » du capteur binaire. Ne jamais appliquer 5 V à une broche du ESP32-C3.

```yaml
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO4
      mode:
        input: true
        pullup: true
      inverted: true
    name: "Bouton"
    id: bouton
    filters:
      - delayed_on: 20ms
      - delayed_off: 20ms
    on_press:
      then:
        - switch.toggle: led_montage
    on_release:
      then:
        - logger.log: "Bouton relâché"
```

L'exemple suppose que l'interrupteur `led_montage` a déjà été déclaré dans la configuration de la DEL. Vérifier le numéro GPIO dans le brochage de la carte utilisée.

## Actions et états

`on_press` exécute les actions lorsque le bouton passe à l'état activé; `on_release` s'exécute lorsqu'il revient à l'état désactivé. Ici, l'appui bascule la DEL. Ces actions sont exécutées par l'ESP32-C3 et ne nécessitent pas que Home Assistant soit connecté.

Le capteur binaire publie aussi l'état du bouton dans Home Assistant lorsqu'il est joignable. On peut ainsi vérifier l'entrée dans le tableau de bord tout en gardant les actions locales sur l'appareil.

## Rebond mécanique et filtre

Les contacts physiques d'un bouton ne changent pas toujours d'état proprement. Pendant quelques millisecondes, ils peuvent établir et interrompre plusieurs fois le contact : c'est le rebond mécanique. Sans filtrage, ces transitions rapides peuvent être interprétées comme plusieurs appuis.

ESPHome ne supprime pas automatiquement ce rebond pour une entrée GPIO. Les filtres `delayed_on` et `delayed_off` ci-dessus attendent que chaque nouvel état reste stable pendant 20 ms avant de le publier. Cette durée est un point de départ; elle peut être ajustée selon le bouton et le montage.

## Références

* [Capteur binaire GPIO ESPHome](https://esphome.io/components/binary_sensor/gpio/)
* [Filtres de capteur binaire ESPHome](https://esphome.io/components/binary_sensor/)