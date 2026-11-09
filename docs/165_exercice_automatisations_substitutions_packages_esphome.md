# 145. Exercice 6 : automatisations, substitutions et packages ESPHome {#chapitre-exercice_automatisations_substitutions_packages_esphome}

## 145.1 Travail demandé {#fiche-travail_demande}

À partir de la configuration de l'exercice précédent, organiser le YAML avec des substitutions et un package, puis comparer une automatisation exécutée par ESPHome à une automatisation Home Assistant.

1. Copier la configuration actuelle de l'appareil avant de la modifier. Ne pas inclure les mots de passe ni les clés dans une remise ou une capture d'écran.
1. Ajouter des substitutions pour le nom technique unique de l'appareil et son nom convivial. Réutiliser au moins une substitution dans le nom d'une entité, puis compiler pour confirmer que les expressions sont remplacées correctement.
1. Dans le dossier de configuration ESPHome, créer un sous-dossier `packages`, puis y créer le fichier `commande_del.yaml` contenant le script `activation` de la fiche de notions. Le script doit allumer `del_variable`, attendre 750 ms et éteindre la lumière.
1. Inclure le package dans le YAML principal avec `!include packages/commande_del.yaml`. Vérifier que le chemin correspond à l'emplacement réel des fichiers.
1. Dans la déclaration existante de *lecture_potentiometre*, dans la section `on_value`, vérifier si le voltage dépasse 1.7 V. Exécuter alors le script `activation`; sous le seuil, ne pas lancer le script. Ne pas créer de seconde déclaration pour un identifiant déjà utilisé.
1. Compiler la configuration. Corriger les erreurs de syntaxe, d'indentation, de chemin ou d'identifiant avant l'installation. Installer la version corrigée sur l'appareil.
1. Tester avec le potentiomètre sous puis au-dessus du seuil. Vérifier l'action de la DEL et les journaux ESPHome. Ajuster le seuil si les mesures réelles du potentiomètre le justifient.
1. Dans Home Assistant, créer une automatisation comparable : le changement d'état du capteur du potentiomètre déclenche l'automatisation; si sa valeur dépasse 2 V, allumer l'entité de la lumière pendant 750 ms, puis l'éteindre. Vérifier le résultat dans les journaux du système et sur le tableau de bord.
1. Comparer les deux automatisations. Lors d'un test bref et contrôlé, rendre Home Assistant inaccessible sans couper l'alimentation de l'ESP32-C3; vérifier si l'action locale sur la DEL continue, puis rétablir la connexion. Noter quelles fonctions dépendent du serveur ou du réseau.

## Remise

Remettre le YAML principal et le fichier de package sans secrets, ainsi qu'une courte comparaison des deux automatisations. Indiquer le seuil choisi, le résultat du test de déconnexion et les éléments qui ont continué à fonctionner localement.

## Critères de réussite

* Les substitutions sont définies et réutilisées dans la configuration.
* Le package local est inclus avec un chemin valide et contient le script de commande de la DEL.
* Le déclencheur `on_value` exécute le script local seulement lorsque la mesure dépasse le seuil choisi.
* L'automatisation Home Assistant réagit aux changements du capteur et applique la même condition lorsque le serveur et l'appareil communiquent.
* La comparaison distingue clairement les fonctions locales de celles qui dépendent de Home Assistant.
* Les fichiers remis ne contiennent ni mot de passe ni clé secrète.