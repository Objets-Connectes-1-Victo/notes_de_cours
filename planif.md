# Planification ESPHome

Le cours d'introduction basé sur les fiches 152 et 153 a déjà été donné en S08 et compte comme cours 1. Le cours 2 a également lieu en S08. Les cours 3 à 10 sont répartis à raison de deux cours par semaine de S09 à S12; le cours 11 termine la séquence en S13. Chaque cours comprend une fiche et un exercice.

## S08

### Cours 1 — Introduction et première installation (déjà donné)

* **Contenu :** rôle d'ESPHome, ESPHome Device Builder, configuration initiale du XIAO ESP32-C3, installation USB et connexion à Home Assistant (fiches 152 et 153).
* **Exercice :** créer un appareil avec un nom unique, installer son micrologiciel et vérifier qu'il se connecte au Wi-Fi et apparaît dans Home Assistant.

### Cours 2 — Informations intégrées, première DEL, journaux, OTA et dépannage

* **Contenu :** exposer les entités intégrées `internal_temperature`, `wifi_signal`, `uptime`, `status`, `wifi_info` et `version` dans Home Assistant; monter et déclarer une première DEL; lire les journaux, reconnaître les erreurs fréquentes, effectuer une mise à jour OTA et savoir quand revenir à une installation USB.
* **Exercice :** ajouter les informations intégrées à la configuration et au tableau de bord, commander une DEL avec une résistance, puis diagnostiquer un problème préparé à l'aide des journaux et effectuer une mise à jour OTA. Préciser que `internal_temperature` mesure la puce, et non la pièce.

## S09

### Cours 3 — Lire un bouton et utiliser les actions ESPHome

* **Contenu :** entrées numériques, capteur binaire, résistance de rappel interne, logique inversée et rebond mécanique; actions ESPHome déclenchées par `on_press` et `on_release`.
* **Exercice :** brancher un bouton sur une broche compatible, exposer son état dans Home Assistant et configurer une action ESPHome pour basculer la DEL à chaque pression; vérifier les états relâché et appuyé.

### Cours 4 — Contrôler l'intensité d'une DEL avec un potentiomètre

* **Contenu :** sortie PWM, configuration d'une lumière monochrome, entrée analogique (ADC) du ESP32-C3 et lecture d'un potentiomètre; associer une valeur d'entrée au réglage de la luminosité.
* **Exercice :** transformer le montage du premier cours en lumière réglable, exposer la valeur du potentiomètre comme capteur et l'utiliser pour faire varier la luminosité de la DEL; comparer le contrôle par potentiomètre et par Home Assistant.

## S10

### Cours 5 — Automatisations ESPHome et Home Assistant

* **Contenu :** approfondir les actions, conditions, déclencheurs et scripts ESPHome; organiser une automatisation exécutée localement sur l'ESP32-C3. Comparer avec une automatisation Home Assistant, exécutée par le serveur et fondée sur les entités disponibles. Une logique ESPHome locale peut continuer à commander les composants reliés à la carte si Home Assistant ou la connexion Wi-Fi devient indisponible; les fonctions qui nécessitent Home Assistant ou le réseau, comme les commandes depuis son tableau de bord, ne sont alors pas disponibles.
* **Exercice :** programmer une action locale déclenchée par le bouton, avec une condition fondée sur une mesure, puis la réutiliser dans un script ESPHome. Créer ensuite une automatisation Home Assistant équivalente et comparer leur comportement en simulant de façon contrôlée une perte de connexion avec Home Assistant. Noter ce qui continue de fonctionner sur la carte et ce qui dépend du serveur.

### Cours 6 — Modèles (templates) et lambdas

* **Contenu :** capteurs et sorties template; créer une valeur calculée à partir d'un capteur existant; notions de base des lambdas C++ dans ESPHome et cas où une formule YAML suffit.
* **Exercice :** créer un capteur template qui convertit la valeur du potentiomètre en pourcentage et un second qui indique une catégorie (bas, moyen ou élevé); comparer leurs valeurs dans Home Assistant.

## S11

### Cours 7 — Capteur de température et automatisation sur seuil

* **Contenu :** identifier le modèle du capteur de température disponible, le câbler et l'exposer dans Home Assistant; combiner sa mesure avec les actions du bouton et la valeur analogique du potentiomètre. Distinguer la température ambiante de `internal_temperature`, qui mesure la puce.
* **Exercice :** construire un appareil où le bouton commande la DEL, le potentiomètre règle son intensité et la température est mesurée dans Home Assistant; créer une automatisation qui réagit à un seuil de température. Vérifier le fonctionnement de chaque entité.

### Cours 8 — Afficher et intégrer les données sur un écran LCD

* **Contenu :** identifier le type d'écran disponible, son câblage et ses broches; configurer l'afficheur pour montrer les valeurs des capteurs et états de l'appareil. Organiser les entités et combiner l'écran avec les composants déjà utilisés. Privilégier un écran I2C si le matériel le permet.
* **Exercice :** construire un appareil qui combine bouton, DEL, potentiomètre et LCD; afficher une mesure sur l'écran et exposer les entités utiles dans Home Assistant. Adapter le câblage et la configuration au modèle réel d'écran.

## S12

### Cours 9 — Bluetooth LE : proxy ESPHome et Bermuda

* **Contenu :** rôle du Bluetooth Low Energy (BLE), configuration du XIAO ESP32-C3 comme proxy Bluetooth ESPHome, puis utilisation de l'intégration Bermuda dans Home Assistant pour estimer la pièce où se trouve un appareil BLE compatible.
* **Exercice :** activer le proxy BLE, le vérifier dans Home Assistant, puis configurer Bermuda avec une balise ou un appareil BLE disponible et observer les changements de pièce. L'exercice dépend de la disponibilité d'un appareil BLE compatible.

### Cours 10 — Projet de synthèse : conception et réalisation

* **Contenu :** révision du cycle configuration-compilation-installation, mise à jour OTA, lecture des journaux et dépannage; présentation des choix de broches et des entités.
* **Exercice :** concevoir et assembler un appareil ESPHome qui combine les composants étudiés; remettre une première configuration YAML sans secrets et un schéma de branchement.

## S13

### Cours 11 — Projet de synthèse : démonstration et validation

* **Contenu :** tester le fonctionnement complet, lire les journaux, effectuer une mise à jour OTA et corriger les problèmes; présenter les choix de broches et les entités créées.
* **Exercice :** démontrer l'appareil, diagnostiquer et corriger un problème préparé à l'aide des journaux, puis remettre la configuration YAML finale sans secrets, le schéma de branchement et une vérification des fonctions dans Home Assistant.

## Matériel et précautions

* Matériel de base : XIAO ESP32-C3, DEL, résistances, boutons, potentiomètre, écran LCD disponible en classe et capteur de température compatible (modèle à confirmer).
* Vérifier le brochage et la compatibilité de chaque broche avec le modèle exact de carte. Ne jamais appliquer 5 V à une entrée du ESP32-C3.
* Vérifier le type d'interface du LCD avant la séance; le câblage, les broches et la configuration varient selon le modèle.
* Vérifier le modèle et les exigences de câblage du capteur de température avant la séance.
* Garder les mots de passe et les clés dans `secrets.yaml`; ne pas les inclure dans les exercices remis.

