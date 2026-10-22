# 133. Installer ESPHome Device Builder sous Windows et configurer le XIAO ESP32-C3 {#chapitre-installer_esphome_device_builder_sur_windows}

## 133.1 Installer ESPHome Device Builder {#fiche-installer_esphome_device_builder}

ESPHome Device Builder existe sous forme d'application de bureau pour Windows 11. Cette application est distincte du module complémentaire ESPHome installé dans Home Assistant.

1. Ouvrir la page officielle [Installer ESPHome](https://esphome.io/install/) et choisir l'onglet Windows.
2. Télécharger le fichier d'installation `.exe` à partir du lien officiel.
3. Ouvrir le fichier téléchargé et suivre les étapes de l'installateur.
4. Lancer ESPHome Device Builder à partir du menu Démarrer.

Au premier lancement, l'application prépare les outils nécessaires et ouvre le tableau de bord dans le navigateur Web. Il n'est pas nécessaire d'installer Python séparément.

## Créer la configuration du XIAO ESP32-C3

Utiliser un câble USB-C qui permet le transfert de données, puis connecter le XIAO ESP32-C3 à l'ordinateur.

1. Dans le tableau de bord, choisir **Create device**, puis **New Device Setup**.
2. Donner un nom unique à l'appareil, *esphomeXX* 
3. Choisir *Seeed XIAO ESP32C3* comme carte (attention il y en a un autre avec un nom semblable)
4. Entrer le nom et le mot de passe du réseau Wi-Fi. Utiliser Domotique Pedago
5. Laisser ESPHome Device Builder générer les paramètres de sécurité proposés par l'assistant.

Le fichier de configuration YAML doit identifier la variante ESP32-C3. Voici un exemple de configuration initiale :

```yaml
esphome:
  name: xiao-esp32-c3
  friendly_name: XIAO ESP32-C3

esp32:
  variant: esp32c3
  flash_size: 4MB
  framework:
    type: esp-idf

logger:

api:
  encryption:
    key: !secret api_encryption_key

ota:
  - platform: esphome
    password: !secret ota_password

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

Les valeurs référencées avec `!secret` sont conservées dans `secrets.yaml`, dans le dossier de configuration ESPHome. Garder les valeurs générées par l'assistant pour la clé de chiffrement de l'API et le mot de passe OTA. Remplacer les noms des secrets dans la configuration si l'assistant utilise d'autres noms. Ne pas publier `secrets.yaml` ni l'ajouter à un dépôt Git.

Assurez-vous que *ota* et *api* sont activés pour permettre la mise à jour OTA et la communication avec Home Assistant. L'API ESPHome est utilisée par Home Assistant pour découvrir l'appareil et accéder à ses entités.

## Installer le micrologiciel par USB

La toute première installation du micrologiciel doit se faire par USB. Une fois la configuration créée :

1. Choisir **Install** pour l'appareil.
2. Sélectionner l'installation par connexion série/USB et le port COM correspondant au XIAO ESP32-C3.
3. Laisser ESPHome compiler le micrologiciel, puis l'envoyer à la carte.
4. Attendre la fin de l'installation et le redémarrage de la carte.

Si aucun port COM n'apparaît, vérifier que le câble USB-C permet le transfert de données, essayer un autre port USB et reconnecter la carte. La procédure de connexion physique et de dépannage est décrite dans le guide officiel [Physical Device Connection](https://esphome.io/guides/physical_device_connection/).

Après le redémarrage, la carte devrait se connecter au Wi-Fi. ESPHome Device Builder peut ensuite afficher les journaux de l'appareil et son état en ligne. Si Home Assistant est sur le même réseau, il peut découvrir l'appareil et proposer l'ajout de l'intégration ESPHome.

*Consulter l'intégration ESPHome de Home Assistant pour plus de détails sur l'ajout de l'appareil et la configuration des entités.*

Les installations suivantes peuvent être envoyées par OTA, sans rebrancher la carte par USB, tant qu'elle est joignable sur le réseau.

## Références

* [Installation officielle d'ESPHome Device Builder](https://esphome.io/install/)
* [Guide de démarrage ESPHome](https://esphome.io/install/getting-started/)
* [Plateforme ESP32 dans ESPHome](https://esphome.io/components/esp32/)
* [Guide Seeed Studio du XIAO ESP32-C3](https://wiki.seeedstudio.com/xiao_esp32c3_getting_started/)