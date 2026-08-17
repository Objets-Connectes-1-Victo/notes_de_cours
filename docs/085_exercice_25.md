# 362 — 3. Exercice 25

## 363 — 3.1 Chat et chien

NOTE : deux cours sont requis pour cet exercice mais puisque vous avez la possibilité d'effectuer une simulation d'examen, vous avez deux choix :

* terminer cet exercice à la maison et utiliser le dernier cours avant l'examen pour effectuer la simulation;
* prendre les deux cours pour effectuer cet exercice et réaliser la simulation en dehors des heures de cours (le Pi du prof sera disponible à partir du réseau Domotique-Pedago).

Vous devez travailler deux par deux pour réaliser cet exercice. Chaque élève aura son propre Home Assistant.

Attention : sur certaines versions de Home Assistant, lorsqu'on entre un modèle dans l'interface graphique, il faut ajouter des guillemets alentour des doubles accolades.

Testez d'abord sans les guillemets puis ajoutez-les seulement si ça ne fonctionne pas.

YAML

"{{ state\_attr('device\_tracker.position\_virtuelle\_annie', 'latitude') }}"

1. Afin de bien faire le suivi de ce qui se passe sur votre système, je vous conseille de bien configurer la date, l'heure et le fuseau horaire.
2. Vous devez utiliser l'agent MQTT fourni par le prof. Les informations de connexion vous seront données en classe.
3. Chacun des membres de l'équipe doit créer un équipement de type device\_tracker. L'un aura un identifiant sous la forme chat\_de\_nomfamille\_prenom et l'autre, chien\_de\_nomfamille\_prenom.
4. Chacun des membres de l'équipe doit connaître en tout temps la position du chat ET celle du chien. Suivez ces étapes pour y parvenir.
   * Utilisez d'abord le menu Paramètres / Appareils et services / onglet Intégrations / clic sur la tuile MQTT / icône d'engrenage pour vérifier si vous êtes capables de publier la position de votre animal et de recevoir la position de l'animal de votre collègue. Vous devez publier vos informations sur un canal au format chatchien3a4/position\_ag où ag représente vos initiales. Assurez-vous d'avoir des initiales uniques dans la classe.
   * Créez une automatisation pour communiquer automatiquement la position de votre animal via MQTT dès qu'il change de position :
     + Puisqu'il faut communiquer la latitude et la longitude, le service devra [apical\_lien\_interne][format\_json\_dans\_un\_modele,envoyer ces informations au format JSON][/apical\_lien\_interne].
     + Avant de poursuivre, vérifiez si votre collègue reçoit automatiquement les coordonnées de votre animal sur la tuile MQTT (icône d'engrenage) quand vous le déplacez.
   * Puisque l'icône d'engrenage de la tuile MQTT ne permet que de faire des tests, vous devez vous abonner au canal MQTT de votre collègue, ce qui permettra de créer une entité pour recevoir ses informations. L'identifiant de l'entité doit être sensor.chat\_chien\_mqtt.
   * Une automatisation permettra d'initialiser un device\_tracker dont le nom est donnees\_recues à partir des données reçues.
     + Attention : vous devrez [apical\_lien\_interne][format\_json\_dans\_un\_modele,extraire du JSON][/apical\_lien\_interne] la latitude et la longitude afin de fournir des coordonnées GPS.
     + Commencez par tester dans les outils de développement le modèle qui récupère la latitude et celui qui récupère la longitude.
     + Une fois que vous obtenez ces informations, l'automatisation devra les utiliser pour déplacer le device\_tracker. Les données devront être fournies au format [modèle\_latitude, modèle\_longitude].
5. Créez sur chaque système un tableau de bord nommé « Chat et chien ». Le tableau doit afficher :
   * la latitude et la longitude du chat
   * la latitude et la longitude du chien
   * données brutes reçues par MQTT (chat ou chien selon le cas)
   * 3 boutons pour déplacer votre animal à 3 endroits de votre choix à l'aide de coordonnées GPS

   Note : si vous obtenez un affichage du genre [Object, Object], essayez d'entourer votre modèle par des apostrophes.
6. Dans votre tableau de bord « Chat et chien », créez un second onglet qui affichera une carte géographique qui prend tout l'espace disponible. Sur la carte, on veut suivre la position du chat et du chien. Faites en sorte que la carte montre les déplacements des derniers 24 heures. À vous de trouver comment faire ;-)
7. Modifiez vos configurations pour qu'aucune communication MQTT n'ait lieu lorsque le soleil est couché (information disponible via l'intégration sun).
8. Poussez maintenant la position du chat et du chien sur le système du prof via MQTT, toujours à l'aide de l'agent fourni par le prof. Utilisez un canal au format chatchien3a4/chat/ag et chatchien3a4/chien/ag où ag représente vos initiales.
9. Ajustez les systèmes pour que lorsque le chat se déplace, le chien le suive après 10 secondes.
10. OPTIONNEL : vous devez instaurer un système pour qu'il y ait un meneur et un suiveur. Si c'est le chat qui est le meneur, le chien le suivra dans ses déplacements et vice-versa.
    1. Chacun des membres de l'équipe doit avoir un équipement virtuel qui permet de dire si c'est le chat ou le chien qui est le meneur.
    2. Faites le nécessaire pour que si les deux disent que c'est eux le meneur ou si les deux disent que c'est l'autre le meneur, c'est nécessairement le chat qui sera le meneur.
    3. Modifiez l'automatisation qui fait en sorte que le chien suive le chat. Plutôt, sur les deux systèmes, faites en sorte que lorsque le meneur se déplace, l'autre le suive après 10 secondes.