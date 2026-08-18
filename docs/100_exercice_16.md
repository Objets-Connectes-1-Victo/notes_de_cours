# 90. Exercice 16 {#chapitre-exercice_16_006}

## 90.1 Présence {#fiche-presence}

1. [Installez l'application Home Assistant](99_detecteur_de_presence_sous_home_assistant.md#fiche-travailler_avec_l_application_home_assistant) sur votre téléphone.
2. <a href="fiche-gerer_les_personnes.md#gerer_les_personnes">Gérez les informations associées à votre personne</a> afin d'y ajouter une photo de vous et d'y associer votre téléphone.
3. [Définissez deux zones de votre choix](99_detecteur_de_presence_sous_home_assistant.md#fiche-les_zones_dans_home_assistant), par exemple École et Travail.
4. Créez un [device\_tracker](99_detecteur_de_presence_sous_home_assistant.md#fiche-simuler_la_position_gps_d_une_personne_avec_device_tracker_see) qui simule votre propre position. Déplacez-vous virtuellement dans chacune des zones que vous avez configurées.
5. Ajoutez au moins une autre personne. Il peut s'agir d'une personne qui vit sous votre toit ou non. Associez cette personne à un téléphone ou à un device\_tracker.
6. Créez une automatisation qui agit sur votre récepteur [lorsqu'une personne de votre choix arrive à la maison](99_detecteur_de_presence_sous_home_assistant.md#fiche-automatisation_qui_tient_compte_de_la_presence).
7. Créez une automatisation qui agit sur votre récepteur lorsqu'une personne de votre choix est à la maison depuis 5 minutes.
8. Créez une automatisation qui agit sur votre récepteur lorsqu'il n'y a plus personne à la maison. Attention : il devra être déclenché quand l'une ou l'autre des personne quitte et l'action sera exécutée seulement si les deux personnes sont absentes.
9. En vue du prochain l'exercice, assurez-vous de laisser votre boîte domotique branchée pendant environ 24 heures afin qu'elle puisse accumuler les données de vos capteurs.