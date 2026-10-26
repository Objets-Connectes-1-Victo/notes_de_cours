# 134. Les entités intégrées ESPHome {#chapitre-entites_integrees_esphome}

## 134.1 Objectif {#fiche-objectif}

Un appareil ESPHome peut publier des informations sur son fonctionnement et sa connexion, même sans capteur externe. Home Assistant reçoit ces informations comme des entités.

## Informations disponibles

Ajouter les blocs suivants à la configuration de l'appareil créée au cours précédent. Ne pas remplacer les blocs `esphome`, `esp32`, `wifi`, `api` et `ota` déjà générés.

Dans ESPHome, `sensor:` sert à déclarer des capteurs qui publient une valeur numérique, par exemple une température, une force de signal ou une durée. En comparaison, `binary_sensor:` publie un état binaire (par exemple en ligne ou hors ligne) et `text_sensor:` publie du texte (par exemple une adresse IP ou une version).

Le "name" de chaque entité est celui qui sera affiché dans Home Assistant. L'identifiant interne de l'entité est dérivé du nom, mais peut différer selon la langue et les caractères utilisés. 

```yaml
sensor:
  - platform: internal_temperature
    name: "Température interne de la puce"
    update_interval: 60s

  - platform: wifi_signal
    name: "Force du signal Wi-Fi"
    id: wifi_signal_dbm
    update_interval: 60s

  - platform: uptime
    name: "Durée de fonctionnement"
    update_interval: 60s

binary_sensor:
  - platform: status
    name: "Wi-Fi connecté"

text_sensor:
  - platform: wifi_info
    ip_address:
      name: "Adresse IP"
    ssid:
      name: "Réseau Wi-Fi"
    mac_address:
      name: "Adresse MAC"

  - platform: version
    name: "Version d'ESPHome"
```

* `internal_temperature` mesure la température interne de la puce. Ce n'est pas une mesure fiable de la température de la pièce.
* `wifi_signal` rapporte la force du signal Wi-Fi en dBm. Une valeur plus près de zéro indique généralement un signal plus fort.
* `uptime` indique depuis combien de temps l'appareil fonctionne depuis son dernier démarrage.
* `status` indique si le nœud ESPHome est joignable par l'intégration.
* `wifi_info` publie des renseignements sur la connexion Wi-Fi.
* `version` indique la version d'ESPHome installée.


## À retenir

Ces entités facilitent le diagnostic et la supervision. Elles ne remplacent pas des capteurs externes : en particulier, la température interne de la puce ne doit pas être présentée comme la température ambiante.

## Références

* [Capteurs ESPHome](https://esphome.io/components/sensor/)
* [Capteur de force du signal Wi-Fi](https://esphome.io/components/sensor/wifi_signal/)
* [Capteur de durée de fonctionnement](https://esphome.io/components/sensor/uptime/)
* [Informations Wi-Fi](https://esphome.io/components/text_sensor/wifi_info/)