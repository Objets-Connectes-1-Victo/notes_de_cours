# 140. Exercice : bouton et filtre anti-rebond {#chapitre-exercice_bouton_anti_rebond_esphome}

## 140.1 Travail demandé {#fiche-travail_demande}

À partir du circuit DEL du cours précédent, ajoutez un bouton poussoir et configurez son entrée dans ESPHome.

1. Hors tension, brancher un côté du bouton à GPIO4 (D2) et l'autre à GND.
1. Déclarer le bouton comme `binary_sensor` GPIO avec la résistance de rappel interne ("pullup") et l'inversion logique appropriée.
1. Configurer `on_press` pour allumer la DEL et consigner un message dans les journaux; configurer `on_release` pour l'éteindre et consigner un autre message.
1. Tester le bouton et vérifier son état dans les journaux ESPHome et dans Home Assistant.
1. Dans Home Assistant, créer un capteur texte virtuel nommé « Dernier appui du bouton ».
1. Créer une automatisation qui se déclenche lorsque l'entité du bouton passe à `on`, puis met à jour le capteur texte avec l'heure de l'appui.
1. Ajouter l'entité du bouton et le helper texte au tableau de bord. Appuyer sur le bouton et vérifier que le message « Bouton appuyé à HH:MM:SS » est mis à jour.
1. Regarder si la transition de l'état du bouton est stable ou si elle change plusieurs fois rapidement.
1. Ajouter les filtres `delayed_on` et `delayed_off` avec une durée initiale de 20 ms. Compiler et installer la mise à jour.
1. Comparer les journaux et le comportement avant et après filtrage en appuyant plusieurs fois rapidement. Expliquer pourquoi le filtre réduit les transitions parasites; le rebond peut être difficile à observer sur un bouton particulier.
1. Vérifier que la DEL reste allumée pendant que le bouton est maintenu et s'éteint au relâchement, sans messages répétés dus au rebond.