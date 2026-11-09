# 147. Exercice 7 : capteurs template et lambdas ESPHome {#chapitre-exercice_modeles_lambdas_esphome}

## 147.1 Travail demandé {#fiche-travail_demande}

À partir de la configuration de l'exercice précédent, créer deux entités calculées à partir de la lecture du potentiomètre : une valeur en pourcentage et une catégorie textuelle. Utiliser `on_value` sur le capteur de pourcentage pour régler la lumière à partir du potentiomètre, avec une luminosité maximale de 70 %.

1. Copier la configuration actuelle de l'appareil dans une nouvelle configuration d'appareil.
1. Vérifier que le capteur ADC `lecture_potentiometre` fonctionne et observer ses valeurs minimale et maximale dans les journaux ESPHome ou dans Home Assistant. Noter ces deux valeurs en volts.
1. Ajouter un capteur `template` nommé « Potentiomètre en pourcentage ». Dans sa lambda, lire `id(lecture_potentiometre).state`, convertir la plage mesurée en une valeur de 0 à 100, et limiter le résultat à cette plage. Utiliser l'exemple de la fiche de cours et remplacer les tensions par celles mesurées.
1. Dans la déclaration de ce capteur, ajouter un déclencheur `on_value` qui règle la luminosité de `del_variable` à partir de `x`, la valeur courante du pourcentage. Calculer `brightness` avec `x * 0.007f` pour limiter la luminosité à 70 % lorsque le potentiomètre atteint 100 %. Utiliser une courte `transition_length` pour que les mises à jour successives ne s'accumulent pas.
1. Ajouter un capteur de texte `template` nommé « Catégorie du potentiomètre ». À partir du pourcentage calculé, publier `bas` sous 25 %, `moyen` de 25 % à moins de 75 %, et `élevé` à partir de 75 %.
1. Compiler la configuration. Corriger les erreurs de syntaxe, d'indentation ou d'identifiant avant d'installer le micrologiciel.
1. Installer la configuration, puis ajouter les deux capteurs au tableau de bord Home Assistant. Tourner lentement le potentiomètre et vérifier que le pourcentage varie et que la catégorie change aux seuils prévus.
1. Vérifier que `on_value` ajuste la lumière selon le potentiomètre jusqu'à 70 % de sa luminosité maximale. Commander ensuite la lumière depuis Home Assistant; noter que la prochaine mise à jour du capteur réapplique la luminosité déterminée par le potentiomètre.
1. Tester les deux extrémités de la course du potentiomètre. Confirmer que le pourcentage reste entre 0 et 100 même si la lecture ADC sort légèrement de la plage de calibration.
1. Comparer les journaux ESPHome aux états affichés dans Home Assistant. Expliquer pourquoi le capteur ADC, le pourcentage et la catégorie ont des valeurs ou des unités différentes.


## Critères de réussite

* Le capteur template calcule un pourcentage à partir du capteur ADC et son résultat est limité à 0–100 %.
* Le capteur de texte template affiche `bas`, `moyen` ou `élevé` aux seuils de 25 % et 75 %.
* Les deux nouvelles entités apparaissent et se mettent à jour dans Home Assistant.
* Le déclencheur `on_value` du capteur template ajuste la lumière selon le potentiomètre et limite la luminosité à 70 %.
* Les valeurs de calibration correspondent aux lectures réelles du potentiomètre.