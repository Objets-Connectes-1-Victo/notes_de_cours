<a id="fiche-detecter_la_presence_avec_un_cellulaire"></a>
# 55. Exercice 9
<a id="chapitre-pour_le_prochain_cours_013"></a>

## 55.1 Détecter la présence avec un cellulaire

1. Installez le plugin qui correspond à votre situation.
   1. Si vous désirez travailler avec le plugin Networks (recommandé) : installez le <a href="fiche-travailler_avec_le_plugin_networks.md#travailler_avec_le_plugin_networks">plugin Networks</a>. Notez qu'au Cégep, ceci ne fonctionnera que si vous utilisez le réseau Domotique-Pedago.
   2. Si vous désirez travailler avec le plugin Détection de téléphone :
      1. <a href="fiche-activer_bluetooth_sur_raspberry_pi_os_lite.md#activer_bluetooth_sur_raspberry_pi_os_lite">Activez le Bluetooth</a> sur votre Raspberry Pi. Notez que vous n'avez aucun appareil Bluetooth à pairer à cette étape.
      2. Installez le <a href="fiche-travailler_avec_le_plugin_detection_de_telephone.md#travailler_avec_le_plugin_detection_de_telephone">plugin Détection de téléphone</a>.
   3. Si vous n'avez pas de téléphone, votre prof pourra vous prêter un localisateur d'objet. Vous travaillerez alors <a href="fiche-travailler_avec_le_plugin_bluetooth_advertisement_blea.md#travailler_avec_le_plugin_bluetooth_advertisement_blea">avec le plugin BLEA</a>.
2. Configurez le plugin pour qu'il détecte votre présence à partir de votre téléphone (ou votre localiseur d'objet). L'équipement doit se nommer « Téléphone de » suivi de votre nom.
3. Si vous vivez avec d'autres personnes qui possèdent un téléphone, configurez Jeedom pour qu'il détecte la présence d'au moins une autre personne.
4. Créez un équipement virtuel pour simuler votre présence et votre absence. L'équipement doit se nommer « Présence virtuelle de » suivi de votre nom.
5. Créez un second équipement virtuel pour simuler la présence ou l'absence d'une autre personne de votre choix.
6. Créez un scénario qui enregistre une information dans le fichier journal nommé presence dès que vous arrivez à la maison. Le scénario se déclenchera avec votre téléphone ou avec votre équipement virtuel.
7. Modifiez le scénario pour que le log ait lieu seulement s'il est passé 22h ou avant 6h.
8. Créez un scénario qui allume la lumière (réelle ou virtuelle) dès qu'une personne arrive à la maison et qui éteint toutes les lumières lorsqu'il n'y a plus personne à la maison.
9. Faites une impression d'écran du Dashboard qui montre que vous êtes présent à la maison et qui montre vos deux équipements de présence virtuelle. Nommez-la au format nomprenom-Dashboard-Telephone.png. Réalisez les impressions d'écran pour montrer les déclencheurs et les détails de vos nouveaux scénarios. Donnez-leur des noms significatifs selon ce qui vous a été enseigné dans ce cours. Remettez vos fichiers sur la plateforme électronique du cours afin que votre prof constate que vous avez terminé l'exercice.

Notez que lors de l'examen qui est prévu au prochain cours, vous devrez remette votre carte micro SD à votre professeur une fois l'examen terminé.

Vous devrez utiliser votre carte personnelle au cours d'après si la correction de l'examen n'est pas terminée.