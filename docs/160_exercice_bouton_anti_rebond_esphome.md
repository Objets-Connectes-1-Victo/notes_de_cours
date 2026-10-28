# 140. Exercice : bouton et filtre anti-rebond {#chapitre-exercice_bouton_anti_rebond_esphome}

## 140.1 Travail demandé {#fiche-travail_demande}

À partir du circuit DEL du cours précédent, ajoutez un bouton poussoir et configurez son entrée dans ESPHome.

1. Hors tension, brancher un côté du bouton à GPIO4 (D2) et l'autre à GND. Utiliser une autre broche si l'enseignant le demande, puis vérifier son numéro GPIO.
2. Déclarer le bouton comme `binary_sensor` GPIO avec la résistance de rappel interne et l'inversion logique appropriée.
3. Configurer `on_press` pour basculer l'interrupteur de la DEL et `on_release` pour consigner un message dans les journaux.
4. Tester le bouton et vérifier son état dans les journaux ESPHome et dans Home Assistant.
5. Ajouter les filtres `delayed_on` et `delayed_off` avec une durée initiale de 20 ms. Compiler et installer la mise à jour.
6. Comparer les journaux et le comportement avant et après filtrage en appuyant plusieurs fois rapidement. Expliquer pourquoi le filtre réduit les transitions parasites; le rebond peut être difficile à observer sur un bouton particulier.
7. Vérifier que la DEL réagit toujours à un appui et qu'une pression maintenue ne provoque pas de basculements répétés.

## Remise

Remettre la configuration YAML sans secrets, un schéma de branchement indiquant GPIO et GND, et une courte explication du rebond mécanique ainsi que du rôle des filtres utilisés.

## Critères de réussite

* Le bouton est lu correctement avec une entrée GPIO et une résistance de rappel.
* Les actions à l'appui et au relâchement fonctionnent.
* Les filtres sont configurés et leur effet est expliqué, même si le rebond n'est pas visible à chaque essai.
* Le montage n'applique jamais 5 V à une broche du ESP32-C3.