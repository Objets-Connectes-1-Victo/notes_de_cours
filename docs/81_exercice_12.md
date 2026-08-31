# 72. Exercice 12 {#chapitre-exercice_12_005}

## 72.1 Capteurs virtuels et tableau de bord {#fiche-capteurs_virtuels_et_tableau_de_bord}

1. À l'aide de l'interface graphique, [créez un capteur virtuel](79_les_capteurs_virtuels.md#fiche-configurer_un_capteur_virtuel) pour simuler un capteur d'ouverture de porte. Il doit être représenté par l'icône door.
1. Installez [le module complémentaire File Editor](77_le_fichier_configurationyaml.md#fiche-travailler_avec_le_module_complementaire_file_editor) si ce n'est pas déjà fait.
fait.
1. [À l'aide du fichier configuration.yaml](77_le_fichier_configurationyaml.md#fiche-Editer_le_fichier_configuration_yaml), créez un second capteur virtuel pour simuler le nombre de chats qui sont entrés dans une chatière. Vous pouvez utiliser le module complémentaire de votre choix pour éditer le fichier configuration.yaml.
1. Prenez soin de [valider vos configurations](77_le_fichier_configurationyaml.md#fiche-validation_des_configurations) avant de [les recharger,recharger](77_le_fichier_configurationyaml.md#fiche-Editer_le_fichier_configuration_yaml) (inutile de redémarrer le système au complet).
1. À l'aide de la technique de votre choix, créez un récepteur virtuel pour simuler une ampoule.
1. [Créez un tableau de bord personnalisé](80_les_tableaux_de_bord.md#fiche-creer_un_tableau_de_bord_personnalise) qui permet de **modifier** l'état de vos capteurs virtuels. Plusieurs types de cartes peuvent faire l'affaire, à vous de choisir celui qui vous convient.
1. Dans votre tableau de bord, ajoutez une [carte qui affiche une icône différente selon l'état de la porte virtuelle](80_les_tableaux_de_bord.md#fiche-changer_l_icone_d_une_entite_selon_son_etat).
1. [Créez une sauvegarde](72_sauvegarde_de_home_assistant.md#fiche-sauvegarde_de_home_assistant) de votre Home Assistant et copiez le fichier sur votre ordinateur.
1. En prévision du prochain cours, [créez-vous une clé d'API OpenWeatherMap](84_le_soleil_et_la_meteo_sous_home_assistant.md#fiche-service_openweathermap). Vous l'utiliserez seulement dans le prochain exercice mais en la créant tout de suite, vous serez assurés de ne pas avoir à attendre le délai d'activation.
<!--
1. Dans votre tableau de bord, ajoutez une [carte qui permet d'afficher une image de vous](80_les_tableaux_de_bord.md#fiche-utiliser_vos_propres_images_dans_un_tableau_de_bord_lovelace).
1. [À l'aide de la commande scp,port](53_scripts_python_pour_envoyer_et_recevoir_du_signal_sur_le_gpio.md#fiche-copier_un_fichier_sur_une_machine_linux_a_partir_d_un_autre_ordinateur), copiez sur votre ordinateur le fichier /mnt/data/supervisor/homeassistant/.storage/core.entity\_registry qui contient toutes les entités. Notez que ce type de manipulation pourrait vous être demandé en examen.
-->