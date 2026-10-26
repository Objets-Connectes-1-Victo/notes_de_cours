# 138. Exercice : commander une DEL avec ESPHome {#chapitre-exercice_premier_peripherique_sortie_del}

## 138.1 Travail demandé {#fiche-travail_demande}

Réalisez le premier périphérique de sortie avec le XIAO ESP32-C3.

1. À partir du schéma de la fiche précédente, câbler une DEL avec une résistance en série et une broche GND.
2. Ajouter à la configuration ESPHome un interrupteur GPIO correspondant à la broche utilisée. Vérifier le numéro GPIO sur le brochage du XIAO ESP32-C3.
3. Compiler et installer le micrologiciel. Vérifier que l'interrupteur apparaît dans Home Assistant.
4. Commander la DEL depuis Home Assistant et vérifier visuellement les états activé et désactivé.
5. En cas de problème, vérifier la polarité de la DEL, le câblage, la broche déclarée et les journaux ESPHome.

## Remise

Remettre le fichier YAML sans secrets, un schéma simple du câblage indiquant la broche GPIO et la résistance utilisée, ainsi qu'une preuve que la DEL peut être commandée depuis Home Assistant.

## Critères de réussite

* La DEL est montée avec une résistance en série et fonctionne sans appliquer 5 V à une broche.
* La configuration compile et expose l'interrupteur dans Home Assistant.
* Les états activé et désactivé correspondent au comportement réel de la DEL.