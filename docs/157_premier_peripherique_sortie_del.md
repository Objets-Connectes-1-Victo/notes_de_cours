# 137. Premier périphérique de sortie : une DEL {#chapitre-premier_peripherique_sortie_del}

## 137.1 Montage électrique {#fiche-montage_electrique}

Une broche configurée comme sortie peut commander un périphérique simple. Pour ce premier montage, l'ESP32-C3 allumera et éteindra une DEL.

Utiliser une broche de sortie disponible sur le modèle exact de carte. Pour le XIAO ESP32-C3, D1 correspond à GPIO3; vérifier le brochage de la carte avant de câbler.

```text
GPIO3 (D1) ---- résistance 220 à 330 ohms ---- anode DEL |>| cathode ---- GND
```

La patte longue de la DEL est généralement l'anode et la patte courte, près du côté plat du boîtier, la cathode. La résistance doit être en série avec la DEL. Ne jamais brancher une DEL directement entre une broche et GND. Les broches du XIAO ESP32-C3 utilisent une logique de 3,3 V; ne pas leur appliquer 5 V.

## Déclarer la sortie dans ESPHome

Ajouter un interrupteur GPIO à la configuration :

```yaml
switch:
  - platform: gpio
    pin: GPIO3
    id: led_montage
    name: "DEL du montage"
```

Après compilation et installation, cet interrupteur devrait être disponible dans Home Assistant. L'état activé applique un niveau logique haut à la broche; si la DEL est branchée avec la polarité indiquée, elle s'allume.

## Vérifications et précautions

1. Vérifier le câblage hors tension avant de connecter la carte.
2. Confirmer que la broche choisie correspond au numéro GPIO de la configuration, et pas seulement au nom imprimé sur la carte.
3. Si la DEL ne s'allume pas, vérifier sa polarité, la résistance, la connexion GND et la broche dans les journaux.

## Références

* [Interrupteur GPIO ESPHome](https://esphome.io/components/switch/gpio/)
* [Brochage du XIAO ESP32-C3](https://wiki.seeedstudio.com/xiao_esp32c3_getting_started/)