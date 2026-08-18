# 87. Exercice 15 {#chapitre-exercice_15_003}

## 87.1 Encore plus d'automatisations {#fiche-encore_plus_d_automatisations}

1. Faites le nécessaire pour pouvoir [envoyer du courriel avec Home Assistant](94_notification_par_courriel.md#fiche-configurer_home_assistant_pour_l_envoi_de_courriel). L'adresse de courriel utilisée doit être au format homeassistant@mondomaine.com.
2. Modifiez une de vos automatisations pour qu'en plus d'agir sur le récepteur, [elle envoie un courriel pour vous aviser de ce qui vient de se passer](94_notification_par_courriel.md#fiche-automatisation_qui_envoie_un_courriel). Le message envoyé devra contenir une information au sujet d'un capteur de votre choix, obtenue à l'aide d'un modèle.
3. Modifiez cette automatisation pour qu'en plus d'envoyer un courriel, elle écrive la valeur du capteur [dans un fichier journal](92_deboguer_home_assistant.md#fiche-Ecrire_dans_un_fichier_journal).
4. Créez une automatisation qui [retrouve l'adresse IP du Raspberry Pi à l'aide d'un modèle,modele](67_chapitre_de_reference_pour_home_assistant.md#fiche-trouver_l_adresse_ip_de_home_assistant) et qui vous l'envoie par courriel lors du démarrage de Home Assistant.
5. Créez une automatisation qui effectue l'action de votre choix [à 10h tous les jours](93_automatisations_qui_tiennent_compte_de_lheure.md#fiche-automatisation_qui_tient_compte_de_l_heure) (vous pouvez changer l'heure pour vos tests).
6. Créez une automatisation qui effectue l'action de votre choix seulement si le capteur est activé entre 10h et 12h inclusivement (vous pouvez changer l'intervalle de temps pour vos tests).
7. Créez une automatisation qui effectue l'opération de votre choix à partir du déclencheur de votre choix mais seulement le samedi et le dimanche.
8. [Créez une sauvegarde](72_sauvegarde_de_home_assistant.md#fiche-sauvegarde_de_home_assistant) de votre Home Assistant et copiez le fichier sur votre ordinateur.