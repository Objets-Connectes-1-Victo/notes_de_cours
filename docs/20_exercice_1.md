# 18. Exercice 1 {#chapitre-exercice_1_005}

## 18.1 Installation de Jeedom {#fiche-installation_de_jeedom}

Si vous ne réussissez pas à terminer cet exercice pendant le cours, vous devez absolument terminer à la maison avant le prochain cours.

1. [Installez Jeedom](17_jeedom_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_jeedom_et_premier_acces) sur votre Raspberry Pi.
2. Branchez votre Pi sur le réseau filaire afin d'obtenir de meilleures performances.
   1. Ne faites pas le sudo apt upgrade pour l'instant, c'est trop long au Cégep. Vous devrez le faire en devoir chez vous.
   2. Effectuez toutes les configurations présentées sur la fiche d'installation de Jeedom maisne faites pas la configuration d'adresses IP statiques pour l'instant.
3. Une fois le Raspberry Pi démarré, [vérifiez l'adresse IP de votre Pi](05_raspberry_pi.md#fiche-trouver_l_adresse_ip_du_raspberry_pi). Au Cégep, le Wi-Fi fournira une adresse DHCP au format 172.19.240.xxx. Avec le réseau filaire qui passe par le commutateur fourni, l'adresse sera au format 192.168.29.xxx.
4. Faites le nécessaire pour pouvoir [vous brancher via SSH sans avoir à entrer votre mot de passe à chaque fois](05_raspberry_pi.md#fiche-permettre_le_branchement_ssh_sans_demander_le_mot_de_passe_a_chaque_fois).
5. [Accédez à Jeedom,acceder](17_jeedom_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_jeedom_et_premier_acces) à partir de votre navigateur. Le but ici est simplement de vous assurer que vous avez accès à Jeedom. Nous commencerons à le configurer au prochain cours.
6. Si vous avez travaillé jusqu'ici en filaire, faites le nécessaire pour que le tout fonctionne sans fil et vice-versa. Vous devez pouvoir travailler avec ces deux interfaces. Si vous n'aviez pas configuré le réseau sans fil dans Raspberry Pi Imager, vous pouvez le faire en suivant les étapes de cette fiche : « [configurer\_le\_reseau\_wi-fi\_sur\_le\_raspberry\_pi](05_raspberry_pi.md#fiche-configurer_le_reseau_wi-fi_sur_le_raspberry_pi) ».
7. OPTIONNEL : faites en sorte que l'[adresse IP du Pi vous soit envoyée par courriel lors du démarrage](05_raspberry_pi.md#fiche-envoyer_l_adresse_ip_par_courriel_apres_le_demarrage_du_raspberry_pi).
8. Effectuez une [sauvegarde manuelle de Jeedom](18_pour_vous_assurer_de_ne_rien_perdre_en_cas_de_probleme.md#fiche-copie_de_securite_de_jeedom) et téléchargez-la sur votre poste de travail.
9. Sur une nouvelle carte micro SD, faites une nouvelle [installation de Jeedom](17_jeedom_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_jeedom_et_premier_acces) puis [restaurez le système à partir de la sauvegarde que vous venez de réaliser,restaurer](18_pour_vous_assurer_de_ne_rien_perdre_en_cas_de_probleme.md#fiche-copie_de_securite_de_jeedom). Vous aurez ainsi deux cartes fonctionnelles qui contiennent un Jeedom dans le même état.
10. Prenez le temps de visionner [la petite vidéo qui montre comment bien rouler votre câble réseau](05_raspberry_pi.md#fiche-comment_bien_rouler_un_cable_reseau).