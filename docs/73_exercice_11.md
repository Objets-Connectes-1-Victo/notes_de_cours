# 65. Exercice 11 {#chapitre-exercice_11_005}

## 65.1 Commencer à travailler avec Home Assistant {#fiche-commencer_a_travailler_avec_home_assistant}

1. Changez le nom de votre installation Home Assistant. Ce nom doit correspondre à votre nom complet au format Prénom NomDeFamille. À vous de fouiller dans les options de menu pour trouver comment faire.
2. [Configurez votre clé Z-Wave](71_commencer_a_travailler_avec_home_assistant.md#fiche-configurer_la_cle_usb_z-wave_sur_home_assistant) sur Home Assistant.
3. [Ajoutez un capteur et un récepteur](71_commencer_a_travailler_avec_home_assistant.md#fiche-ajouter_un_appareil_connecte_z-wave_a_home_assistant) de votre choix à votre système. Rappel : les modes d'emplois de vos objets connectés sont sur Teams.
4. Donnez un nom significatif à vos appareils puis testez-les à l'aide de l'écran Aperçu.
5. Faites une impression d'écran de votre écran Aperçu.
6. [Créez une sauvegarde de Home Assistant](72_sauvegarde_de_home_assistant.md#fiche-sauvegarde_de_home_assistant) puis téléchargez-la sur votre poste de travail.
7. Afin de pouvoir travailler sur votre système domotique à la maison, vous avez deux choix. Vous devez sélectionner celui qui vous convient et effectuer les manipulations en conséquence.  
   1. Brancher le Raspberry Pi à votre routeur à la maison à l'aide d'un câble RJ-45. Aucune configuration spéciale ne sera alors requise.
   2. Connecter le Raspberry Pi à votre réseau sans fil à la maison ou à l'aide du partage de connexion de votre cellulaire. Vous devrez [créer un autre fichier de configuration,plusieursconfigurations](67_chapitre_de_reference_pour_home_assistant.md#fiche-configurer_l_acces_au_reseau_dans_home_assistant) pour ce réseau.
8. Si vous avez choisi de travailler à la maison à l'aide du sans fil, copiez votre fichier de configuration dans le dossier network sur une clé USB correctement configurée. Branchez la clé au Raspberry Pi puis redémarrez-le. Vérifiez que le fichier a été correctement copié dans le dossier /etc/NetworkManager/system-connections.
9. OPTIONNEL : effectuez ces manipulations pour vous brancher manuellement à un autre réseau sans fil. Dans les manipulations que je vous propose, vous vous brancherez au réseau régulier du Cégep. Par contre, vous ne pourrez pas accéder à l'interface Web de Home Assistant à partir de ce réseau.

   1. Branchez clavier et écran au Raspberry Pi. Vous verrez l'invite ha >.
   2. [Accédez au terminal HassOS,consolehavsterminal](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-la_console_home_assistant).
   3. Demandez à HassOS [de vous lister les réseaux sans fil disponibles,terminal](67_chapitre_de_reference_pour_home_assistant.md#fiche-configurer_l_acces_au_reseau_dans_home_assistant).
   4. Repérez le réseau régulier du Cégep. C'est la colonne SSID qui nous intéresse.
   5. Connectez le Pi à ce réseau.
   6. Vérifiez que vous avez maintenant [une adresse IP](67_chapitre_de_reference_pour_home_assistant.md#fiche-trouver_l_adresse_ip_de_home_assistant) qui correspond à ce réseau.
   7. Reconnectez-vous maintenant à Domotique-Pedago.
   8. [Déconnectez maintenant le Wi-Fi](04_linux.md#fiche-nmcli_l_outil_en_ligne_de_commande_du_networkmanager). Plusieurs manipulations pourraient être requises pour que tous les réseaux sans fil soient déconnectés. La bannière de Home Assistant devrait maintenant vous donner seulement l'adresse IP du réseau filaire.
10. [Éteignez Home Assistant de façon sécuritaire](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-Eteindre_home_assistant_de_facon_securitaire).
11. Déposez votre impression d'écran sur la plateforme électronique du cours.