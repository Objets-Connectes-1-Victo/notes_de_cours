# Planification ESPHome

Le cours d'introduction basé sur les fiches 152 et 153 a déjà été donné en S08, cours 2. Les 10 cours à préparer sont répartis à raison de deux cours par semaine de S09 à S13; chacun fera l'objet d'une fiche et comprendra un exercice.

## S08

### Cours 2 — Introduction et première installation (déjà donné)

* **Contenu :** rôle d'ESPHome, ESPHome Device Builder, configuration initiale du XIAO ESP32-C3, installation USB et connexion à Home Assistant (fiches 152 et 153).
* **Exercice :** créer un appareil avec un nom unique, installer son micrologiciel et vérifier qu'il se connecte au Wi-Fi et apparaît dans Home Assistant.

## S09

### Cours 1 — Informations intégrées et connexion à Home Assistant

* **Contenu :** entités intégrées ESPHome : `internal_temperature`, `wifi_signal`, `uptime`, `status`, `wifi_info` et `version`; découverte des entités et affichage dans un tableau de bord Home Assistant.
* **Exercice :** ajouter ces capteurs et informations à la configuration, installer la mise à jour par OTA, puis créer un tableau de bord affichant leur état. Préciser que `internal_temperature` mesure la température de la puce, et non celle de la pièce.

## S10

### Cours 2 — Première sortie : contrôler une DEL

* **Contenu :** entrées/sorties numériques, choix des broches du XIAO ESP32-C3, résistance en série et limites électriques des broches 3,3 V; déclarer une sortie et un interrupteur ESPHome.
* **Exercice :** monter une DEL avec sa résistance et la commander depuis Home Assistant; documenter la broche utilisée et vérifier les états marche/arrêt.

### Cours 3 — Faire varier l'intensité d'une DEL

* **Contenu :** sortie PWM, configuration d'une lumière monochrome et réglage de la luminosité depuis Home Assistant.
* **Exercice :** transformer le montage précédent en lumière réglable, tester plusieurs niveaux de luminosité et observer l'effet d'une transition.

## S11

### Cours 4 — Lire un bouton

* **Contenu :** entrées numériques, capteur binaire, résistance de rappel interne, logique inversée et rebond mécanique.
* **Exercice :** brancher un bouton sur une broche compatible, exposer son état dans Home Assistant et vérifier les états relâché et appuyé.

### Cours 5 — Lire un potentiomètre

* **Contenu :** entrée analogique (ADC) du ESP32-C3, câblage du potentiomètre, plage de tension permise et publication d'une valeur dans Home Assistant.
* **Exercice :** exposer la position du potentiomètre comme capteur, la représenter dans Home Assistant et comparer les valeurs aux positions minimale et maximale.

## S12

### Cours 6 — Réagir aux entrées

* **Contenu :** déclencheurs et actions ESPHome, réaction à un bouton ou à un seuil de capteur; distinction entre une logique exécutée sur l'appareil et une automatisation Home Assistant.
* **Exercice :** faire basculer une DEL à chaque pression sur le bouton, puis créer une automatisation Home Assistant qui réagit à un changement de l'entrée.

### Cours 7 — Afficher des données sur un écran LCD

* **Contenu :** identifier le type d'écran disponible, câblage et broches requises, configuration de l'afficheur et mise à jour des informations affichées. Privilégier un écran I2C si le matériel le permet.
* **Exercice :** afficher au minimum une valeur disponible (par exemple la durée de fonctionnement ou la force du signal Wi-Fi) et vérifier son actualisation. Adapter le câblage et la configuration au modèle réel d'écran.

## S13

### Cours 8 — Intégrer les composants dans un appareil

* **Contenu :** organiser une configuration complète, nommer clairement les entités et combiner entrées, sorties, afficheur et informations réseau; utiliser les journaux pour diagnostiquer un problème.
* **Exercice :** réaliser un appareil qui combine bouton, DEL, potentiomètre et LCD, et rendre ses états ou mesures utiles dans Home Assistant.

### Cours 9 — Journaux, OTA et dépannage

* **Contenu :** lire les journaux ESPHome, repérer les erreurs fréquentes de configuration ou de connexion, effectuer une mise à jour OTA et savoir quand revenir à une installation USB.
* **Exercice :** diagnostiquer un problème préparé (entité absente, mauvaise broche ou appareil hors ligne), corriger la configuration et valider la correction par les journaux et Home Assistant.

### Cours 10 — Projet de synthèse et validation

* **Contenu :** révision du cycle configuration-compilation-installation, mise à jour OTA, validation du montage et dépannage; présentation des choix de broches et des entités.
* **Exercice :** finaliser et démontrer un appareil ESPHome fonctionnel. Remettre la configuration YAML sans secrets, un schéma de branchement et une courte vérification des fonctions dans Home Assistant.

## Matériel et précautions

* Matériel de base : XIAO ESP32-C3, DEL, résistances, boutons, potentiomètre et écran LCD disponible en classe.
* Vérifier le brochage et la compatibilité de chaque broche avec le modèle exact de carte. Ne jamais appliquer 5 V à une entrée du ESP32-C3.
* Vérifier le type d'interface du LCD avant la séance; le câblage, les broches et la configuration varient selon le modèle.
* Garder les mots de passe et les clés dans `secrets.yaml`; ne pas les inclure dans les exercices remis.

