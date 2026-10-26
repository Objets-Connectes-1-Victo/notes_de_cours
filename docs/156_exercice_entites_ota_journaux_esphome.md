# 136. Exercice : entités intégrées, OTA et journaux {#chapitre-exercice_entites_ota_journaux_esphome}

## 136.1 Travail demandé {#fiche-travail_demande}

À partir de la configuration du XIAO ESP32-C3, ajoutez les entités intégrées présentées dans la fiche précédente.

1. Ajouter les capteurs `internal_temperature`, `wifi_signal` et `uptime`, le capteur binaire `status`, ainsi que les informations `wifi_info` et `version`.
2. Compiler le micrologiciel et relever toute erreur de validation. Corriger la configuration avant l'installation.
3. Installer la mise à jour par OTA. Garder la carte alimentée pendant toute l'opération.
4. Ouvrir les journaux et repérer les messages indiquant le démarrage, la connexion Wi-Fi et la disponibilité de l'API.
5. Si ce n'est pas déjà fait, ajouter l'appareil dans Home Assistant et vérifier que les entités sont disponibles. (*Paramètres - Intégrations - Découvertes*)
6. Entrer la clé de chiffrement de l'API dans Home Assistant pour que l'intégration puisse se connecter à l'appareil. Vérifier que l'état de l'appareil passe à "en ligne" et que les entités sont accessibles. (Dans le .yml de l'appareil: *api.encryption.key*)
7. Dans Home Assistant, vérifier la présence des entités, puis ajouter au tableau de bord la force du signal, la durée de fonctionnement et le statut du Wi-Fi.