<a id="fiche-automatiser_des_taches_sous_linux_ou_mac"></a>
# 8. Les scripts bash

## 8.1 Automatiser des tâches sous Linux ou Mac

Sous Linux ou Mac, les scripts bash (Bourne Again SHell) permettent d'automatiser des tâches.

Par exemple, on pourrait avoir un script bash qui se charge de copier certains fichiers dans un nouveau dossier dont le nom contient la date du jour.

## Pour plus d'information

« Bash Guide for Beginners ». Machtelt Garrels. <https://tldp.org/LDP/Bash-Beginners-Guide/html/Bash-Beginners-Guide.html>
<a id="chapitre-semaine_1_004"></a>

## 8.2 Passer un paramètre à un script bash

Les scripts bash peuvent recevoir des paramètres, aussi appelés arguments.

Pour appeler le script, il suffit de passer les valeurs des paramètres à la suite du nom du script, séparés par des espaces.

Terminal

./monscript.sh premierparametre deuxiemeparametre

Dans le script, le premier paramètre sera $1, le second sera $2, etc.

Le script pourra utiliser les paramètres comme bon lui semble.

Ici, il ne fait que les afficher à l'écran.

Fichier monscript.sh

#!/bin/bash  
# Pour tester le passage de paramètres

 

echo "Premier paramètre: " $1  
echo "Deuxième paramètre: " $2

Ce qui donnera :

Résultat à l'écran

pi@raspberrypi:~ $ ./monscript.sh a b  
Premier paramètre: a  
Deuxième paramètre: b