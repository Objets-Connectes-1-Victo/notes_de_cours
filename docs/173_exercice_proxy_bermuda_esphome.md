# 153. Exercice 10 : proxy BLE et présence avec Bermuda {#chapitre-exercice_proxy_bermuda_esphome}

## 153.1 Travail demandé {#fiche-travail_demande}

En équipe de deux ou trois, configurer un Home Assistant pour l'équipe et y connecter les proxys ESPHome de ses membres. Utiliser le téléphone Android d'un membre comme balise iBeacon avec l'application Home Assistant Companion, puis comparer les observations des proxys placés aux coins opposés de la pièce avec Bermuda. Un proxy ESPHome ne doit être utilisé que par un seul Home Assistant à la fois.

Le propriétaire du téléphone doit consentir à son utilisation comme balise et à son suivi durant l'exercice. Ne pas suivre le téléphone d'une autre personne. La transmission iBeacon peut augmenter la consommation de la batterie; la désactiver à la fin.

1. Former une équipe de deux ou trois et choisir le Home Assistant de l'équipe. Chaque membre prépare son XIAO ESP32-C3 comme proxy BLE et l'ajoute à ce Home Assistant, sans connecter le même proxy à un autre Home Assistant.
1. Faire une copie de la configuration ESPHome de chaque appareil. Noter son nom, le réseau utilisé et les broches déjà occupées. Vérifier que chaque carte est bien un XIAO ESP32-C3.
1. Dans la configuration YAML existante, ajouter les composants suivants. Ne pas créer un deuxième bloc s'ils sont déjà présents :

   ```yaml
   esp32_ble_tracker:

   bluetooth_proxy:
     active: false
   ```

   `active: false` suffit pour relayer les annonces BLE et évite de configurer des connexions GATT actives, qui ne sont pas nécessaires à cet exercice.
   
1. Compiler la configuration et corriger les erreurs avant l'installation. Lors de la toute première activation de `esp32_ble_tracker`, installer le micrologiciel par USB si ESPHome demande de redimensionner la partition. Après cette installation initiale, les mises à jour peuvent généralement se faire par OTA.
1. Installer le micrologiciel et consulter les journaux ESPHome. Vérifier que l'appareil démarre et rejoint le Wi-Fi. Si des erreurs de mémoire ou de partition apparaissent, suivre le message fourni par ESPHome et demander de l'aide avant de poursuivre.
1. Dans Home Assistant, vérifier que tous les appareils ESPHome de l'équipe sont connectés et que leurs proxys sont disponibles dans **Paramètres > Appareils et services > Bluetooth**.
1. Placer les proxys à des coins éloignés de la pièce; avec trois proxys, utiliser trois coins si possible. Dans Home Assistant, créer une pièce (area) d'essai par emplacement, par exemple `Coin A`, `Coin B` et, s'il y a un troisième proxy, `Coin C`. Affecter chaque appareil ESPHome à la pièce (area) correspondante. Ces pièces (areas) représentent des emplacements de réception dans une seule pièce physique.
1. Sur le téléphone Android, ouvrir **Paramètres > Companion app > Manage sensors > Bluetooth sensors > BLE Transmitter**. Activer le capteur et la transmission iBeacon. Le téléphone sera détecté comme un iBeacon, pas comme un appareil Home Assistant; il n'est pas nécessaire d'associer l'application Companion au Home Assistant de l'équipe. Laisser le téléphone près du premier proxy et vérifier que son annonce est reçue; si nécessaire, consulter la fiche de cours pour le dépannage de la détection.
1. Dans l'instance Home Assistant de l'équipe, installer Bermuda depuis **Paramètres > Marketplace**. Redémarrer Home Assistant si demandé, puis ajouter **Bermuda BLE Trilateration**.
1. Dans la configuration de Bermuda, sélectionner l'iBeacon du téléphone. Vérifier dans ses appareils et entités que Bermuda fournit des informations de présence, de pièce estimée ou de distance.
1. Déplacer le téléphone près du proxy du `Coin A`, puis du `Coin B`. Attendre la mise à jour des observations et noter le RSSI reçu par chaque proxy ainsi que la pièce estimée par Bermuda. Répéter les essais près du centre de la pièce et comparer les résultats.
1. La pièce estimée par Bermuda est une approximation à partir des récepteurs et du signal; les deux pièces (areas) d'essai ne permettent pas d'obtenir une position exacte ni de distinguer des pièces physiques, puisqu'elles sont dans une seule salle.
1. À la fin, vérifier les journaux et les entités, puis supprimer de Bermuda les appareils de test qui ne doivent plus être suivis.
1. Désactiver la transmission iBeacon dans l'application Android.

### Dépannage

* **Aucune annonce détectée :** vérifier que la transmission iBeacon est active dans l'application Android, que le téléphone est à portée, que Bluetooth est disponible dans Home Assistant et que les proxys sont connectés.
* **Le proxy n'apparaît pas dans Home Assistant :** vérifier les journaux ESPHome, la connexion Wi-Fi, l'intégration ESPHome et la configuration Bluetooth de Home Assistant.
* **Un proxy cesse d'être disponible quand un autre Home Assistant est configuré :** vérifier que chaque proxy est connecté uniquement à l'instance Home Assistant de son équipe.
* **Bermuda avertit qu'un appareil n'a pas de pièce (area) et mentionne `hci0` :** `hci0` est l'adaptateur Bluetooth local du Raspberry Pi qui héberge Home Assistant, et non un proxy ESPHome de l'équipe.
* **La compilation ou l'installation échoue après l'ajout du tracker :** lire l'erreur ESPHome. Une installation USB peut être nécessaire la première fois pour appliquer la nouvelle partition.
* **Bermuda ne crée pas d'entités pour la balise :** vérifier que l'intégration est installée, que la balise est sélectionnée dans sa configuration et qu'elle est reconnue comme appareil BLE compatible.
* **La pièce estimée est instable ou incorrecte :** vérifier l'affectation des pièces (areas) d'essai, la position des proxys et la couverture. Le RSSI varie avec les obstacles et l'orientation; une estimation de pièce n'est pas une mesure exacte.

## Remise

Remettre la configuration ESPHome sans secrets, une capture ou une description montrant les proxys de l'équipe dans son Home Assistant, et un tableau des observations :

| Emplacement du téléphone | RSSI du proxy Coin A | RSSI du proxy Coin B | RSSI du proxy Coin C (si présent) | Pièce estimée par Bermuda |
| --- | --- | --- | --- | --- |
| Près du Coin A | À compléter | À compléter | À compléter | À compléter |
| Près du Coin B | À compléter | À compléter | À compléter | À compléter |
| Au centre | À compléter | À compléter | À compléter | À compléter |

Ne pas inclure d'adresse, de nom ou de donnée permettant d'identifier un appareil personnel sans autorisation.

## Critères de réussite

* `esp32_ble_tracker` et `bluetooth_proxy` sont ajoutés correctement à la configuration existante.
* Le XIAO ESP32-C3 démarre, rejoint le Wi-Fi et est visible comme proxy Bluetooth dans Home Assistant.
* Le téléphone Android autorisé diffuse un iBeacon détecté par les proxys de l'équipe.
* Bermuda suit la balise et présente des entités ou observations pertinentes.
* Les observations des proxys placés aux coins opposés sont comparées dans le Home Assistant de l'équipe.
* Les résultats expliquent les limites du RSSI et de l'estimation de pièce, et aucun secret ni suivi non autorisé n'est remis.
