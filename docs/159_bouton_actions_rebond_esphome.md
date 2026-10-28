# 139. Lire un bouton : actions et rebond mécanique {#chapitre-bouton_actions_rebond_esphome}

## 139.1 Lire un bouton avec une entrée GPIO {#fiche-entree_gpio}

Une broche GPIO peut être configurée comme entrée ou comme sortie. Pour lire un signal numérique, ESPHome utilise un `binary_sensor` avec `platform: gpio`. L'entrée détecte deux niveaux logiques, généralement interprétés comme activé et désactivé; elle ne mesure pas une tension variable. 

!!! note

    Pour une tension variable, on utilise plutôt un capteur analogique ADC (`platform: adc`)

Dans la configuration, le numéro `GPIO` désigne la broche du microcontrôleur, qui peut avoir un autre nom imprimé sur la carte. 

Le mode d'entrée et une résistance de rappel (`pullup` ou `pulldown`) donnent un état stable lorsque le circuit externe n'impose pas de niveau. Si ni résistance de rappel interne ni résistance externe n'est configurée, la broche est flottante : elle n'a pas de niveau défini et peut changer d'état sans appui sur le bouton. Dans les exemples ci-dessous, `pulldown` ou `pullup` fixe ce niveau au repos.

!!! warning
    
    Vérifier le brochage de la carte et les limites électriques avant de connecter un circuit; les entrées du XIAO ESP32-C3 ne tolèrent pas 5 V.

### Exemple simple : bouton avec résistance `pulldown`

La résistance de rappel interne maintient l'entrée à l'état bas lorsque le bouton est relâché. Le bouton relie GPIO4 à 3,3 V lorsqu'on appuie : l'état lu passe alors à haut.

![Bouton avec résistance de rappel interne `pulldown`](img/esphome_montage_bouton_pulldown.png)

```text

```yaml
binary_sensor:
  - platform: gpio
    pin:
      number: GPIO4
      mode:
        input: true
        pulldown: true
    name: "Bouton"
    id: bouton
```

À l'appui, le capteur binaire passe directement à l'état activé. Cette première configuration ne contient aucun filtre; elle sert à comprendre la lecture de l'entrée avant d'aborder le rebond mécanique.

### Variante : bouton avec `pullup`, inversion et anti-rebond

Avec un câblage `pullup`, l'entrée est normalement à l'état haut et le bouton la relie à GND lorsqu'on appuie. Le niveau électrique lu à l'appui est donc bas. L'option `inverted: true` inverse cette correspondance pour que l'état logique publié par le capteur binaire soit activé pendant l'appui.

```text
GPIO4 (D2) ---- bouton poussoir ---- GND
```

Avec la résistance de rappel (`pullup`), l'entrée est normalement à l'état haut. L'appui la relie à GND; `inverted: true` fait correspondre cet état bas à l'état logique « activé » du capteur binaire.

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