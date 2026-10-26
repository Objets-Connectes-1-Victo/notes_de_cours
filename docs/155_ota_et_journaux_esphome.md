# 135. OTA et journaux ESPHome {#chapitre-ota_et_journaux_esphome}

## 135.1 Mise à jour OTA {#fiche-mise_a_jour_ota}

OTA signifie « Over-The-Air ». ESPHome peut envoyer un nouveau micrologiciel à l'appareil par le réseau, sans câble USB. La première installation se fait généralement par USB; OTA sert aux mises à jour suivantes.

L'appareil doit être alimenté et joignable sur le réseau. La configuration de base doit contenir une plateforme OTA, généralement celle-ci dans les configurations récentes :

```yaml
ota:
  - platform: esphome
    password: !secret ota_password
```

Conserver le mot de passe OTA dans `secrets.yaml`. Il est distinct de la clé de chiffrement de l'API Home Assistant. Ne pas interrompre l'alimentation pendant l'installation. Si l'appareil n'est plus joignable après une modification, le rebrancher en USB peut être nécessaire pour réinstaller un micrologiciel fonctionnel.

## Lire les journaux

Le bloc suivant active les journaux série et réseau :

```yaml
logger:
```

Dans ESPHome Device Builder, ouvrir les journaux de l'appareil pour observer son démarrage, sa connexion Wi-Fi, les erreurs de configuration et les messages des composants. Les journaux peuvent aussi être consultés par USB lorsque l'appareil ne se connecte plus au réseau.

Quelques vérifications utiles :

* Une erreur de compilation indique généralement une configuration YAML invalide, un composant manquant ou une valeur incompatible.
* L'absence de connexion peut provenir du nom du réseau, du mot de passe, de la portée Wi-Fi ou d'une alimentation instable.
* Si une entité n'apparaît pas, vérifier que sa configuration est bien enregistrée, compilée, installée et publiée par l'API ESPHome.

## Distinguer API et OTA

L'API ESPHome permet à Home Assistant de communiquer avec l'appareil. OTA sert à installer un micrologiciel par le réseau. Ce sont deux fonctions distinctes : une panne de l'API peut rendre les entités indisponibles dans Home Assistant sans empêcher l'appareil d'exécuter sa configuration locale.

## Références

* [Composant OTA ESPHome](https://esphome.io/components/ota/)
* [Composant Logger](https://esphome.io/components/logger/)
* [Intégration ESPHome dans Home Assistant](https://www.home-assistant.io/integrations/esphome/)