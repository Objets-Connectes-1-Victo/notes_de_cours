# 77. Exercice 13 {#chapitre-exercice_13_003}

## 77.1 Les automatisations {#fiche-les_automatisations}

1. [Ajoutez une automatisation](83_les_automatisations_home_assistant.md#fiche-ajouter_une_automatisation_a_l_aide_de_l_interface_graphique) dans laquelle le capteur réel de votre choix agit sur le récepteur réel de votre choix.
2. Créez une seconde automatisation mais cette fois, elle doit travailler avec un capteur virtuel et un récepteur virtuel.
3. Pour chacune de vos automatisations, ajoutez un bouton qui permet de lancer l'automatisation.
4. [Installez l'intégration OpenWeatherMap](84_le_soleil_et_la_meteo_sous_home_assistant.md#fiche-travailler_avec_l_integration_openweathermap).
5. Ajoutez une carte météo sur votre tableau de bord.
6. Modifiez une de vos automatisations pour que l'action n'ait lieu que [s'il fait AU MOINS 10 degrés celcius,modele](83_les_automatisations_home_assistant.md#fiche-ajouter_une_automatisation_a_l_aide_de_l_interface_graphique) (ou autre température de votre choix). Assurez-vous que la carte bouton tienne compte des conditions.
7. Écrivez un script qui allume une lumière virtuelle nommée « Lumière salon virtuelle », allume un téléviseur virtuel puis, après 5 secondes (plus facile à tester qu'avec des minutes ;-) ), éteint la lumière du salon virtuelle.
8. Créez une automatisation qui appelle ce script quand un mouvement est détecté dans le salon mais seulement si l'éclairement est en dessous de 40 lux. Vous pouvez utiliser des capteurs et des récepteurs réels ou virtuels.
9. Écrivez un script qui inscrit votre prénom dans un capteur virtuel textuel, attend qu'un capteur réel envoie un signal de votre choix puis inscrit votre votre nom de famille à la place du prénom.
10. OPTIONNEL : modifiez le script précédent pour qu'il ajoute le nom de famille à la fin de ce qu'il y a déjà dans le capteur virtuel (vous aurez besoin des [modèles](89_les_modeles_home_assistant.md#fiche-les_modeles_dans_home_assistant) pour y parvenir).
11. Créez une nouvelle automatisation qui ferme des stores virtuels [dès que le soleil se couche](84_le_soleil_et_la_meteo_sous_home_assistant.md#fiche-l_integration_sun).