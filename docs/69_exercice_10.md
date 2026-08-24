# 61. Exercice 10 {#chapitre-exercice_10_006}

## 61.1 Installation de Home Assistant {#fiche-installation_de_home_assistant}

Dans cet exercice, vous allez effectuer l'installation de Home Assistant.

Vous devez absolument avoir terminé avant le prochain cours.

- [Installez Home Assistant](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_home_assistant_et_premier_acces) sur votre Raspberry Pi.

<!--
   Note : lors du démarrage du Raspberry Pi, vous aurez besoin d'un réseau rapide pour finaliser l'installation.   
   Le plus simple est de travailler avec une connexion câblée.  
   Il est également possible de configurer la connexion au réseau CEGEPVICTO pour que l'installation soit plus rapide. Vous aurez donc, en plus de la connexion réseau pour Domotique-Pedago, [une connexion pour un réseau Wif-Fi sans mot de passe,none](67_chapitre_de_reference_pour_home_assistant.md#fiche-configurer_l_acces_au_reseau_dans_home_assistant).
-->

<!--
2. OPTIONNEL : Donnez à votre système [une adresse IP statique,ipstatique](67_chapitre_de_reference_pour_home_assistant.md#fiche-configurer_l_acces_au_reseau_dans_home_assistant) selon les informations fournies par votre prof.

3. Accédez [à l'interface Web de Home Assistant,acceder](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_home_assistant_et_premier_acces).

4. Branchez-vous à Home Assistant [via SSH](67_chapitre_de_reference_pour_home_assistant.md#fiche-se_brancher_a_home_assistant_via_ssh) puis [faites afficher les informations sur le réseau,networkinfo](67_chapitre_de_reference_pour_home_assistant.md#fiche-trouver_l_adresse_ip_de_home_assistant).
-->
- Accédez à l'interface Web de Home Assistant [via l'URL `http://ha<num kit>.local`](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_home_assistant_et_premier_acces).
- Configurer votre nom de réseau tel que demandé  (ex. ha1, ha2, etc.) dans Home Assistant.
- Mettez à jour Home Assistant si nécessaire.
- Installer les Add-ons *Terminal & SSH* et *File Editor* dans Home Assistant.
- Connectez-vous à Home Assistant via le Web terminal de l'add-on *Terminal & SSH*.
- Faites afficher les informations sur le réseau dans Home Assistant via la commande `ha banner` et notez l'adresse IP du Pi.
- Faites une impression d'écran qui montre l'adresse IP ainsi trouvée.
- Passer au Home Assistant CLI via la commande `login`. (le mot de passe est `root` si demandé)
- [Éteignez Home Assistant de façon sécuritaire](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-Eteindre_home_assistant_de_facon_securitaire).
- Déposez votre impression d'écran sur la plateforme électronique du cours.
- N'oubliez pas de passez à nouveau votre portable au réseau CEGEPVICTO avant de sortir du cours.