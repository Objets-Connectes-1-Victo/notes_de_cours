# 18. Exercice 1 {#chapitre-exercice_1_005}

## 18.1 Installation de Jeedom {#fiche-installation_de_jeedom}

Si vous ne réussissez pas à terminer cet exercice pendant le cours, vous devez absolument terminer à la maison avant le prochain cours.

1. Installez Jeedom sur votre Raspberry Pi.
2. Branchez votre Pi sur le réseau filaire afin d'obtenir de meilleures performances.
   1. Ne faites pas le sudo apt upgrade pour l'instant, c'est trop long au Cégep. Vous devrez le faire en devoir chez vous.
   2. Effectuez toutes les configurations présentées sur la fiche d'installation de Jeedom maisne faites pas la configuration d'adresses IP statiques pour l'instant.
3. Une fois le Raspberry Pi démarré, vérifiez l'adresse IP de votre Pi. Au Cégep, le Wi-Fi fournira une adresse DHCP au format 172.19.240.xxx. Avec le réseau filaire qui passe par le commutateur fourni, l'adresse sera au format 192.168.29.xxx.
4. Faites le nécessaire pour pouvoir vous brancher via SSH sans avoir à entrer votre mot de passe à chaque fois.
5. Accédez à Jeedom à partir de votre navigateur. Le but ici est simplement de vous assurer que vous avez accès à Jeedom. Nous commencerons à le configurer au prochain cours.
6. Si vous avez travaillé jusqu'ici en filaire, faites le nécessaire pour que le tout fonctionne sans fil et vice-versa. Vous devez pouvoir travailler avec ces deux interfaces. Si vous n'aviez pas configuré le réseau sans fil dans Raspberry Pi Imager, vous pouvez le faire en suivant les étapes de cette fiche : « configurer\_le\_reseau\_wi-fi\_sur\_le\_raspberry\_pi ».
7. OPTIONNEL : faites en sorte que l'adresse IP du Pi vous soit envoyée par courriel lors du démarrage.
8. Effectuez une sauvegarde manuelle de Jeedom et téléchargez-la sur votre poste de travail.
9. Sur une nouvelle carte micro SD, faites une nouvelle installation de Jeedom puis restaurez le système à partir de la sauvegarde que vous venez de réaliser. Vous aurez ainsi deux cartes fonctionnelles qui contiennent un Jeedom dans le même état.
10. Prenez le temps de visionner la petite vidéo qui montre comment bien rouler votre câble réseau.