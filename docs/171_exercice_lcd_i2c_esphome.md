# 151. Exercice 8 : écran LCD et bus I²C {#chapitre-exercice_lcd_i2c_esphome}

## 151.1 Travail demandé {#fiche-travail_demande}

Intégrer un écran LCD au montage ESPHome développé dans les exercices précédents. Le montage doit conserver le bouton, la DEL, le potentiomètre et le capteur de température; l'écran doit présenter au moins une mesure et les entités utiles doivent rester disponibles dans Home Assistant.

Le modèle d'écran et son interface doivent être vérifiés avant le branchement. Les étapes ci-dessous décrivent un LCD1602 de 16 colonnes × 2 lignes équipé d'un adaptateur I²C PCF8574; adapter le câblage et la plateforme ESPHome si le matériel est différent.

1. Copier la configuration actuelle de l'appareil. Vérifier qu'il s'agit d'un LCD1602 à caractères avec un adaptateur I²C PCF8574, puis consulter sa fiche technique, son brochage, sa tension d'alimentation et son interface. Un écran graphique I²C demande une autre plateforme ESPHome.
1. Hors tension, repérer les bornes GND, VCC, SDA et SCL du module. Raccorder GND à la masse commune, VCC à une tension prise en charge par le module, SDA à `GPIO6` et SCL à `GPIO7`, conformément au diagramme de brochage du XIAO ESP32-C3. Vérifier que ces broches sont libres dans la configuration; ESPHome permet d'en choisir d'autres si le montage l'exige.
1. Avant la mise sous tension, vérifier que les résistances de rappel de SDA et SCL ne tirent pas les lignes à 5 V. Ne jamais appliquer 5 V à une entrée de l'ESP32-C3.
1. Ajouter ou compléter la section `i2c:` dans le YAML avec `sda: GPIO6`, `scl: GPIO7` et `scan: true` (ou les autres broches compatibles retenues pour le montage). Compiler, installer le micrologiciel, redémarrer l'appareil et examiner les journaux ESPHome.
1. Noter les adresses trouvées par le scanner. Pour un LCD1602 avec adaptateur PCF8574, `0x27` et `0x3F` sont des adresses courantes; retenir celle détectée et la comparer à la documentation du module.
1. Déclarer le LCD1602 avec `platform: lcd_pcf8574`, `dimensions: 16x2` et l'adresse repérée. Ajouter une entité texte template ESPHome, par exemple « Texte du LCD », avec `mode: text`, `optimistic: true` et une longueur maximale de 16 caractères. Utiliser cette entité dans la lambda d'affichage pour écrire le texte sur la première ligne.
1. Compiler et installer la configuration. Dans Home Assistant, ajouter l'entité texte à une carte, modifier sa valeur et vérifier qu'elle s'affiche sur le LCD. Cette première étape confirme que Home Assistant peut commander le contenu de l'écran via ESPHome.
1. Ajouter ensuite la mesure de température sur la deuxième ligne. Réutiliser l'identifiant du capteur déjà déclaré dans la configuration; ne pas créer un deuxième bloc `i2c:`, `display:` ou `sensor:` s'il en existe déjà un.
1. Compiler et installer la configuration modifiée. Vérifier que le texte change depuis Home Assistant et que la mesure affichée évolue avec le capteur. Garder les chaînes assez courtes pour les 16 caractères de chaque ligne.
1. Vérifier séparément le bouton, la commande de la DEL et la lecture du potentiomètre. Dans Home Assistant, confirmer que les entités utiles — bouton, lumière, potentiomètre et température — sont toujours disponibles; l'afficheur local ne remplace pas ces entités.
1. Si le scanner ne trouve pas d'adresse, vérifier hors tension SDA, SCL, GND, VCC, les broches choisies et la compatibilité des tensions. Après correction, redémarrer et consulter à nouveau les journaux. Si une adresse apparaît mais que l'écran reste vide, vérifier la plateforme, les dimensions, l'adresse, le contraste et le rétroéclairage.

## Remise

Remettre la configuration YAML sans secrets, un schéma indiquant les broches et les tensions, l'adresse I²C détectée, le modèle de l'écran et une capture ou une description de la mesure affichée. Expliquer brièvement ce que le scanner permet de vérifier et ce qu'il ne permet pas de confirmer.

## Critères de réussite

* Le câblage correspond au modèle réel de l'écran et respecte les niveaux logiques du XIAO ESP32-C3.
* ESPHome balaie le bus au démarrage et les journaux permettent de relever l'adresse du module.
* L'adresse trouvée et les paramètres de l'écran sont utilisés dans sa configuration ESPHome.
* Une entité texte Home Assistant permet de modifier le contenu de la première ligne du LCD.
* L'écran affiche aussi une mesure réelle sur la deuxième ligne et la met à jour.
* Le bouton, la DEL, le potentiomètre et les entités utiles dans Home Assistant continuent de fonctionner.
