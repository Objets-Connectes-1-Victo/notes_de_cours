# 72. Exercice 12 {#chapitre-exercice_12_005}

## 72.1 Capteurs virtuels et tableau de bord {#fiche-capteurs_virtuels_et_tableau_de_bord}

1. À l'aide de l'interface graphique, créez un capteur virtuel pour simuler un capteur d'ouverture de porte. Il doit être représenté par l'icône door.
2. Installez le module complémentaire File Editor.
3. Afin de vous assurer d'avoir un éditeur fonctionnel peu importe les conditions qui arrivent (par exemple, File Editor ne sera pas disponible s'il y a une panne Internet), installez également le module complémentaire Studio Code Server.
4. À l'aide du fichier configuration.yaml, créez un second capteur virtuel pour simuler le nombre de chats qui sont entrés dans une chatière. Vous pouvez utiliser le module complémentaire de votre choix pour éditer le fichier configuration.yaml.
5. Prenez soin de valider vos configurations avant de les recharger (inutile de redémarrer le système au complet).
6. À l'aide de la technique de votre choix, créez un récepteur virtuel pour simuler une ampoule.
7. Créez un tableau de bord personnalisé qui permet de **modifier** l'état de vos capteurs virtuels. Plusieurs types de cartes peuvent faire l'affaire, à vous de choisir celui qui vous convient.
8. Dans votre tableau de bord, ajoutez une carte qui affiche une icône différente selon l'état de la porte virtuelle.
9. Dans votre tableau de bord, ajoutez une carte qui permet d'afficher une image de vous.
10. À l'aide de la commande scp, copiez sur votre ordinateur le fichier /mnt/data/supervisor/homeassistant/.storage/core.entity\_registry qui contient toutes les entités. Notez que ce type de manipulation pourrait vous être demandé en examen.
11. Créez une sauvegarde de votre Home Assistant et copiez le fichier sur votre ordinateur.
12. En prévision du prochain cours, créez-vous une clé d'API OpenWeatherMap. Vous l'utiliserez seulement dans le prochain exercice mais en la créant tout de suite, vous serez assurés de ne pas avoir à attendre le délai d'activation.