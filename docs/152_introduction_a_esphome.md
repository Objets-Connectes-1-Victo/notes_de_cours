# 132. Introduction à ESPHome {#chapitre-introduction_a_esphome}

## 132.1 Qu'est-ce qu'ESPHome? {#fiche-quest-ce_qu_esphome}

ESPHome est un système qui permet de programmer des microcontrôleurs comme les ESP32 et les ESP8266 à l'aide de fichiers de configuration YAML. Il transforme cette configuration en micrologiciel qui s'exécute directement sur la carte.

ESPHome n'est pas une boîte domotique. Il sert plutôt à créer des appareils connectés, par exemple un capteur de température ou un relais, qui peuvent ensuite communiquer avec Home Assistant.

## Fonctionnement général

La configuration d'un appareil précise notamment le modèle de la carte, les composants utilisés et les moyens de communication. ESPHome compile cette configuration pour produire le micrologiciel adapté à la carte.

Une fois l'appareil configuré et connecté au réseau Wi-Fi, l'intégration ESPHome de Home Assistant peut communiquer avec lui sur le réseau local. Home Assistant peut alors ajouter les capteurs, interrupteurs ou autres entités déclarés dans la configuration.

Les trois éléments principaux sont :

* **ESPHome Device Builder** : l'interface qui permet de créer et de modifier la configuration YAML, puis de compiler et d'installer le micrologiciel.
* **Micrologiciel ESPHome** : le programme installé sur le microcontrôleur. Il applique la configuration et communique avec les capteurs, les récepteurs et le réseau.
* **Intégration ESPHome de Home Assistant** : le composant de Home Assistant qui se connecte à l'appareil ESPHome, généralement par l'API ESPHome, et rend ses capteurs et commandes disponibles sous forme d'entités.


## Étapes habituelles

1. Ouvrir le tableau de bord d'ESPHome Device Builder.
2. Créer un appareil et choisir le modèle exact de la carte.
3. Modifier sa configuration YAML pour déclarer le réseau et les composants nécessaires.
4. Compiler le micrologiciel et l'installer sur la carte. La première installation se fait souvent par USB; les mises à jour suivantes peuvent généralement être envoyées par le réseau.
5. Ajouter ou confirmer l'appareil dans Home Assistant, puis vérifier que ses entités sont disponibles.

## Exemple de configuration

L'ESPHome Device Builder va générer un fichier de configuration YAML qui ressemble à ceci, le Builder permet ensuite de modifier ce fichier pour ajouter les capteurs et sorties utilisés par l'appareil :

```yaml
esphome:
  name: capteur-salon
  friendly_name: Capteur du salon

esp32:
  board: esp32dev

logger:

api:
  encryption:
    key: !secret api_key

ota:
  - platform: esphome
    password: !secret ota_password

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

Les valeurs `!secret` sont définies dans le fichier `secrets.yaml` du dossier de configuration ESPHome. Cette méthode évite d'inscrire les mots de passe directement dans le fichier de l'appareil ou de les partager par erreur.

Dans une configuration complète, les composants ESPHome permettent ensuite de déclarer les capteurs et les sorties utilisés par le montage. Le choix des composants et des broches dépend du modèle de carte et du circuit électrique.

## Mise à jour OTA

OTA signifie « Over-The-Air », c'est-à-dire « par les airs ». Une mise à jour OTA envoie un nouveau micrologiciel à la carte par le réseau Wi-Fi, sans devoir la brancher à l'ordinateur avec un câble USB.

Pour qu'une mise à jour OTA fonctionne, la carte doit déjà exécuter un micrologiciel ESPHome qui prend en charge OTA, être alimentée et être joignable sur le réseau. On lance alors la compilation et l'envoi depuis le tableau de bord ESPHome. La première installation nécessite souvent une connexion USB; OTA sert surtout aux installations et modifications suivantes. Il ne faut pas confondre OTA avec l'intégration `api`, qui permet à Home Assistant d'échanger avec l'appareil.

Dans l'exemple, le bloc `ota` active le mécanisme ESPHome et demande un mot de passe pour autoriser l'installation. Ce mot de passe est différent de la clé de chiffrement du bloc `api`. Le mot de passe OTA doit rester secret et l'envoi doit être effectué sur un réseau de confiance. OTA fonctionne sur le réseau local; il n'est pas nécessaire d'exposer l'appareil directement à Internet.

Si l'appareil ne répond plus après une modification, il peut être nécessaire de le reconnecter par USB pour réinstaller un micrologiciel fonctionnel. Gardez donc la carte accessible et évitez de couper son alimentation pendant une mise à jour.

## Précautions

* Vérifiez le modèle précis de la carte et la compatibilité des broches avant de compiler.
* Les broches d'un ESP32 fonctionnent généralement en logique 3,3 V. Ne branchez pas directement un signal 5 V sans vérifier les limites de la carte.
* Protégez les identifiants Wi-Fi et les clés d'accès. Ne publiez pas le fichier `secrets.yaml` -> assurez-vous qu'il est bien ignoré par Git si vous utilisez un dépôt (.gitignore).

## Pour plus d'information

* [Documentation officielle d'ESPHome](https://esphome.io/)
* [ESPHome et Home Assistant](https://www.home-assistant.io/integrations/esphome/)