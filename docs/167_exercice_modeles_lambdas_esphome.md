# 147. Exercice 7 : capteurs template et lambdas ESPHome {#chapitre-exercice_modeles_lambdas_esphome}

## 147.1 Travail demandé {#fiche-travail_demande}

À partir de la configuration de l'exercice précédent, créer deux entités calculées à partir de la lecture du potentiomètre : une valeur en pourcentage et une catégorie textuelle.

1. Copier la configuration actuelle de l'appareil avant de la modifier. Ne pas inclure de mot de passe ni de clé secrète dans les fichiers remis.
1. Vérifier que le capteur ADC `lecture_potentiometre` fonctionne et observer ses valeurs minimale et maximale dans les journaux ESPHome ou dans Home Assistant. Noter ces deux valeurs en volts.
1. Ajouter un capteur `template` nommé « Potentiomètre en pourcentage ». Dans sa lambda, lire `id(lecture_potentiometre).state`, convertir la plage mesurée en une valeur de 0 à 100, et limiter le résultat à cette plage. Utiliser l'exemple de la fiche de cours et remplacer les tensions par celles mesurées.
1. Ajouter un capteur de texte `template` nommé « Catégorie du potentiomètre ». À partir du pourcentage calculé, publier `bas` sous 33 %, `moyen` de 33 % à moins de 67 %, et `élevé` à partir de 67 %.
1. Compiler la configuration. Corriger les erreurs de syntaxe, d'indentation ou d'identifiant avant d'installer le micrologiciel.
1. Installer la configuration, puis ajouter les deux entités au tableau de bord Home Assistant. Tourner lentement le potentiomètre et vérifier que le pourcentage varie et que la catégorie change aux seuils prévus.
1. Tester les deux extrémités de la course du potentiomètre. Confirmer que le pourcentage reste entre 0 et 100 même si la lecture ADC sort légèrement de la plage de calibration.
1. Comparer les journaux ESPHome aux états affichés dans Home Assistant. Expliquer pourquoi le capteur ADC, le pourcentage et la catégorie ont des valeurs ou des unités différentes.

## Remise

Remettre le YAML sans secrets, les valeurs minimale et maximale mesurées, ainsi qu'une courte vérification des deux entités et de leurs changements de catégorie.

## Critères de réussite

* Le capteur template calcule un pourcentage à partir du capteur ADC et son résultat est limité à 0–100 %.
* Le capteur de texte template affiche `bas`, `moyen` ou `élevé` selon le pourcentage.
* Les deux nouvelles entités apparaissent et se mettent à jour dans Home Assistant.
* Les valeurs de calibration correspondent aux lectures réelles du potentiomètre.
* La configuration remise ne contient aucun secret.