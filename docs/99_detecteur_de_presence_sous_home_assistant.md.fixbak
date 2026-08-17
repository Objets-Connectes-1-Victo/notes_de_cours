# 89. Détecteur de présence sous Home Assistant {#chapitre-detecteur_de_presence_sous_home_assistant}

## 89.1 Les zones dans Home Assistant {#fiche-les_zones_dans_home_assistant}

Par défaut, Home Assistant a créé une zone lors de sa configuration initiale. Elle porte le nom que vous avez donné à votre boîte (ex : Maison).

Pour tirer profit des fonctionnalités de localisation de Home Assistant, vous devez définir les autres zones d'importance pour votre système : École, Travail, Centre commercial, etc.

Comme pour plusieurs configurations, les zones peuvent être définies à l'aide de l'interface graphique ou encore dans le fichier configuration.yaml.

## Interface graphique {#graphique}

Lorsque vous définissez des zones dans Home Assistant, elles sont enregistrées dans le fichier /mnt/data/supervisor/homeassistant/.storage/zone.

Pour configurer l'emplacement de votre maison (l'endroit où se trouve Home Assistant) :

* Rendez-vous dans le menu Paramètres / Pièces, étiquettes et Zones / Onglet Zones.
* L'icône de maison devrait apparaître dans votre zone initiale. Déplacez-la à l'endroit désiré.

Pour ajouter d'autres emplacements :

* Rendez-vous dans le menu Paramètres / Pièces, étiquettes et Zones / Onglet Zones.
* Cliquez sur Ajouter une zone.
* Donnez un nom à l'emplacement.
* Optionnel : choisissez une icône de <a href="fiche-icones\_material\_design\_dans\_home\_assistant.md#icones\_material\_design\_dans\_home\_assistant">la bibliothèque Material Design</a>.
* Sur la carte, placez le marqueur vis-à-vis l'emplacement souhaité.
* Il est possible de définir un rayon pour les zones. Faites glisser le point blanc pour agrandir ou rapetisser la zone.
* Cliquez sur Ajouter pour enregistrer vos modifications.

  ![Zone école](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-ZoneEcole-SurOrdi.png)
* Une fois les configurations terminées, vous devez redémarrer Home Assistant afin qu'elles soient prises en compte.

## Fichier configuration.yaml

Il est également possible de définir les zones dans le fichier configuration.yaml.

Fichier configuration.yaml

zone:  
  - name: Cégep  
    icon: mdi:school  
    latitude: 46.059284365916156  
    longitude: -71.94339343404864  
    radius: 190

 

  - name: Centre commercial  
    latitude: 46.059869287591276  
    longitude: -71.92660569775728

##

## 89.2 Travailler avec l'application Home Assistant {#fiche-travailler_avec_l_application_home_assistant}

L'application mobile Home Assistant, à installer sur le téléphone de chacune des personnes dont vous désirez connaître la position, permet de créer des automatisations qui tiennent compte de l'endroit où chaque personne se trouve.

Elle ajoute un gros plus à votre système domotique mais le prix à payer est que les données de vos déplacements se retrouveront dans le nuage alors qu'un des avantages d'un système domotique DIY est justement que les données demeurent locales.

Mais considérant que plusieurs applications nous suivent déjà sur nos téléphones, ça ne me pose pas problème.

En recherchant l'application dans l'App Store ou dans Google Play, si vous voyez plusieurs applications qui parlent de Home Assistant, choisissez celle qui utilise le logo de Home Assistant.

![Application Home Assistant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-AppStore.png)

Grâce à l'application mobile Home Assistant, vos automatisations peuvent être plus éclatées qu'avec une simple <a href="fiche-detecter\_la\_presence\_grace\_au\_wi-fi.md#detecter\_la\_presence\_grace\_au\_wi-fi">détection de présence avec le Wi-Fi</a>.

Vous pouvez, par exemple, démarrer le chauffage dès que vous quittez le bureau, recevoir une notification lorsqu'un de vos enfants arrive au centre commercial, allumer une lumière tamisée lorsque votre amoureux ou votre amoureuse atteint le coin de la rue pour rentrer à la maison.

La seule limite est votre imagination!

## Autoriser l'utilisation des données de localisation {#autoriser}

Pour que Home Assistant puisse savoir à quel endroit une personne se situe, il faut que l'application mobile soit autorisée à utiliser les données de localisation du téléphone.

Il est possible que pendant l'installation, l'application vous en demande l'autorisation.

Les autorisations peuvent par la suite être modifiées en tout temps.

Sur iPhone, rendez-vous dans Réglages / Confidentialité et sécurité / Service de localisation. Donnez le droit Toujours à l'application Home Assistant.

Sur Android, rendez-vous dans Paramètres / Sécurité et confidentialité / Paramètres de confidentialité / Gestionnaire des autorisations / Localisation. Assurez-vous que l'application Home Assistant ait l'autorisation Toujours autorisée.

## Configurer l'application

Lors du premier démarrage de l'application mobile Home Assistant, cliquez sur Connect to my Home Assistant.

![App mobile Home Assistant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-ApplicationMobile.png)

Si votre serveur est détecté, cliquez dessus pour le sélectionner.

![Application Home Assistant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-ApplicationMobile-2.png)

Sinon, cliquez sur Enter address manually puis entrez l'adresse IP de votre serveur, incluant le protocole (ici : http://) et le port (ici : 8123).

![Application Home Assistant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-ApplicationMobile-3.png)   ![Application Home Assistant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-ApplicationMobile-4.png)

La personne en possession de ce téléphone a désormais la possibilité de contrôler votre Home Assistant à partir de celui-ci, <a href="fiche-gerer\_les\_personnes.md#gerer\_les\_personnes">dans les limites des privilèges que vous aurez accordé à l'utilisateur correspondant</a>.

![Application Home Assistant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-ApplicationMobile-5.png)

## Définir les zones {#zones}

Pour que l'application puisse indiquer à Home Assistant à quel endroit vous vous trouvez, vous devez <a href="fiche-les\_zones\_dans\_home\_assistant.md#les\_zones\_dans\_home\_assistant">définir les zones d'importance pour votre système</a> : Maison, École, Travail, Centre commercial, etc.

## Pour plus d'information {#soumettrerecherche}

« Setting up presence detection ». Home Assistant. <https://www.home-assistant.io/getting-started/presence-detection/>

## 89.3 Envoyer une notification à l'application mobile {#fiche-envoyer_une_notification_a_l_application_mobile}

L'intégration [notify](https://www.home-assistant.io/integrations/notify/) permet d'envoyer une notification à l'application mobile associée à votre Home Assistant.

Pour l'utiliser dans une automatisation ou dans les outils de développement, il faut exécuter l'action Notifications: Send a notification via mibile\_app\_... (notify.mobile\_app\_...), où les points de suspension sont remplacés par le nom du téléphone.

![Notification app mobile](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-NotificationAppMobile.png)

Si cette action n'apparaît pas, ouvrez l'application mobile puis rendez-vous dans le menu Paramètres / Application Companion / Notifications. Assurez-vous que la case Autorisation est à Activé.

Vous devez ensuite renseigner le titre et le message.

La notification apparaîtra à l'écran comme les autres notifications du téléphone.

![Notification](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-NotificationSurCellulaire.png)

## 89.4 Gérer les personnes {#telephone}

Home Assistant vous permet de définir les personnes qui peuvent être « suivies », par exemple celles que le système pourra identifier comme présentes dans la maison ou pas.

Pour gérer les personnes :

* Rendez-vous dans le menu Paramètres / Personnes.
* Cliquez le nom de la personne à éditer ou sur Ajouter une personne pour ajouter une personne.

  ![Ajouter une personne](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-NouvellePersonne.png)
* Téléchargez une photo de la personne.
* Remplissez les informations demandées.
* Si la personne a déjà installé <a href="fiche-travailler\_avec\_l\_application\_home\_assistant.md#travailler\_avec\_l\_application\_home\_assistant">l'application Home Assistant</a> sur son téléphone, choisissez le téléphone qui lui correspond dans la liste déroulante.
* Vous pouvez également lui assigner une <a href="fiche-simuler\_la\_position\_gps\_d\_une\_personne\_avec\_device\_tracker\_see.md#simuler\_la\_position\_gps\_d\_une\_personne\_avec\_device\_tracker\_see">position virtuelle</a> afin de faciliter les tests de vos automatisations.

Si <a href="fiche-les\_zones\_dans\_home\_assistant.md#les\_zones\_dans\_home\_assistant">l'emplacement de la maison</a> a été correctement configuré et que les personnes sont correctement associées à leur application mobile sur leur téléphone, l'écran Aperçu indiquera clairement qui est à la maison (on verra le nom de votre boîte Home Assistant) et qui est absent.

![Présent](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-Personne-Present.png) ![Absent](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-Personne-Absent.png)

Dans le cas où la personne se trouve dans une <a href="fiche-les\_zones\_dans\_home\_assistant.md#les\_zones\_dans\_home\_assistant">zone connue</a>, Home Assistant affichera le nom de cette zone.

![Personne dans la zone travail](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-Personne-Travail.png)

Si une personne apparaît comme absente alors qu'elle est à la maison :

* Assurez-vous que <a href="fiche-les\_zones\_dans\_home\_assistant.md#les\_zones\_dans\_home\_assistant">l'emplacement de la maison</a> a été correctement configuré.
* Redémarrez Home Assistant pour vous assurer que toutes les configurations sont prise en compte.

Si une personne montre le statut Inconnu (en anglais, Unknown ou Unk), c'est qu'il y a un problème avec son téléphone.

![Personne au statut inconnu](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-Personne-Inconnu.png)

Pour régler ce problème :

* Assurez-vous d'abord que la personne est [associée à son téléphone](https://apical.xyz/formations/pageunique/systeme_domotique_diy#telephone).
* Assurez-vous ensuite que <a href="fiche-travailler\_avec\_l\_application\_home\_assistant.md#travailler\_avec\_l\_application\_home\_assistant">l'application Home Assistant détient les droits pour accéder aux données de localisation du téléphone</a>.
* Parfois, un redémarrage du téléphone est nécessaire.

## Pour plus d'information

« Person ». Home Assistant. <https://www.home-assistant.io/integrations/person/>

## 89.5 Automatisation qui tient compte de la présence {#fiche-automatisation_qui_tient_compte_de_la_presence}

J'aime configurer Home Assistant pour que les lumières s'allument automatiquement quand une personne arrive à la maison après une heure donnée.

Ceci peut être réalisé à l'aide d'une automatisation qui utilise <a href="fiche-gerer\_les\_personnes.md#gerer\_les\_personnes">le détecteur de présence</a>.

Pour créer une telle automatisation :

* Paramètres / Automatisations et scènes / Créer une automatisation.
* Le type de déclencheur sera Heure et lieu / Zone.
* Dans la liste déroulante, choisissez la personne, le téléphone associé à la personne ou encore <a href="fiche-simuler\_la\_position\_gps\_d\_une\_personne\_avec\_device\_tracker\_see.md#simuler\_la\_position\_gps\_d\_une\_personne\_avec\_device\_tracker\_see">le virtuel</a> qui doit déclencher l'action.

  ![Automation Zone](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-AutomatisationZone.png)
* Choisissez la zone désirée puis précisez si le déclenchement doit avoir lieu quand la personne entre ou sort de la zone.
* Vous pouvez finalement ajouter, selon vos besoins, les autres déclencheurs ou conditions, par exemple pour <a href="fiche-automatisation\_qui\_tient\_compte\_de\_l\_heure.md#automatisation\_qui\_tient\_compte\_de\_l\_heure">tenir compte de l'heure</a>, puis de spécifier les actions à réaliser.

## Pour plus d'information

« Setting up presence detection ». Home Assistant. <https://www.home-assistant.io/getting-started/presence-detection/>

« Making Home Assistant’s Presence Detection not so Binary ». Phil Hawthorne. <https://philhawthorne.com/making-home-assistants-presence-detection-not-so-binary/>

## 89.6 Simuler la position GPS d'une personne avec device\_tracker.see {#fiche-simuler_la_position_gps_d_une_personne_avec_device_tracker_see}

Lorsque vous désirez que Home Assistant puisse <a href="fiche-automatisation\_qui\_tient\_compte\_de\_la\_presence.md#automatisation\_qui\_tient\_compte\_de\_la\_presence">réagir selon la position d'une personne</a> en utilisant <a href="fiche-travailler\_avec\_l\_application\_home\_assistant.md#travailler\_avec\_l\_application\_home\_assistant">l'application Home Assistant</a>, il devient difficile de tester les automatisations sans devoir vous déplacer physiquement dans la ville.

Par chance, la position géographique d'une personne peut être simulée grâce au service [device\_tracker.see](https://www.home-assistant.io/integrations/device_tracker/#device_trackersee-service).

Ce service peut modifier la position d'un système de suivi GPS réel ou virtuel.

## Créer un device\_tracker

Le fonctionnement d'une entité de type device\_tracker est passablement différent de celui des autres types de <a href="fiche-configurer\_un\_capteur\_virtuel.md#configurer\_un\_capteur\_virtuel">virtuels</a>, par exemple input\_boolean ou encore input\_text.

D'abord, pour créer une entité de type device\_tracker, il suffit d'appeler le service (exécuter l'action) device\_tracker.see.

Ensuite, la valeur de l'entité ainsi créée sera perdue au redémarrage de Home Assistant.

Voici donc comment créer un device\_tracker :

Entrez ceci dans Outils de développement /  Actions :

* Action : Voir (device\_tracker.see).

  ![device_tracker.see](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-DeviceTracker-See.png)

  Notez que selon les configurations de votre système, il pourrait arriver que le service ne soit pas reconnu. Si c'est votre cas, ajoutez cette ligne dans le fichier configuration.yaml :

  Fichier configuration.yaml

  device\_tracker:

  Vous devrez ensuite redémarrer Home Assistant (un rechargement des configurations n'est pas suffisant).
* ID de l'appareil : entrez l'identifiant de l'objet à modifier. Si aucune entité ne correspond à cet identifiant, une entité virtuelle sera créée.

  Attention : lorsqu'on fait appel au service device\_tracker.see, il faut préciser l'identifiant de l'objet et non l'identifiant de l'entité. Donc, il ne faut pas entrer le domaine device\_tracker, seulement l'identifiant de l'objet.

  Par exemple, ceci ne fonctionnera pas : device\_tracker.position\_virtuelle\_annie.

  il faut plutôt entrer position\_virtuelle\_annie.
* Emplacement : si vous désirez travailler avec les zones, entrez le nom d'une zone définie dans votre système Home Assistant ou home pour simuler que la personne est à la maison.

  Notez que le travail avec des zones offre moins de possibilités que le travail avec une position GPS.

  ![Service device_tracker.see](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-TesterDeviceTrackerSee.png)
* Pour tirer tout le potentiel du positionnement, if faut travailler avec des coordonnées GPS. Deux syntaxes sont disponibles :
  + sur une ligne, le tout entre crochets carrés :   
    [46.058476616659746, -71.94362640380861]
  + sur deux lignes, chaque valeur précédée d'un trait d'union puis d'un espace :   
    - 46.058476616659746  
    - -71.94362640380861

  ![Service device_tracker.see](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-TesterDeviceTrackerSeeGPS.png)

Une fois le service appelé, si l'entité n'existait pas, elle est créée. Sinon, sa position est simplement mise à jour.

## Retrouver l'identifiant d'un device\_tracker

Vous pouvez confirmer que l'entité existe et retrouver son nom à partir du menu Paramètres / Appareils et services / Onglet Entités.

Suggestion : utilisez la case Filtre pour retrouver les entités plus rapidement.

![Entité device_tracker](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-EntiteDeviceTracker.png)

Les informations sur le device\_tracker sont enregistrées dans le fichier /mnt/data/supervisor/homeassistant/known\_devices.yaml.

Ce fichier peut être visualisé à l'aide du <a href="fiche-travailler\_avec\_le\_module\_complementaire\_file\_editor.md#travailler\_avec\_le\_module\_complementaire\_file\_editor">module complémentaire File editor</a>.

Fichier known\_devices.yaml

position\_virtuelle\_annie:  
  name: position\_virtuelle\_annie  
  mac:  
  icon:  
  picture:  
  track: true

## device\_tracker dans une automatisation qui travaille avec une zone

Voici un problème qui peut survenir ou non selon votre version de Home Assistant.

Lorsqu'une <a href="fiche-automatisation\_qui\_tient\_compte\_de\_la\_presence.md#automatisation\_qui\_tient\_compte\_de\_la\_presence">automatisation doit réagir quand une personne virtuelle entre ou sort d'une zone donnée</a>, elle doit être en mesure de retrouver les coordonnées GPS du device\_tracker.

Si vous avez utilisé un nom de zone pour spécifier la position d'un device\_tracker, vous pourriez obtenir un message du genre « Message malformed: Entity is neither a valid entity ID nor a valid UUID for dictionary value » lorsque vous enregistrez l'automatisation.

![Message malformed: Entity is neither a valid entity ID nor a valid UUID for dictionary value](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-DeviceTracker-MessageMalformed.png)

Et même si vous n'obtenez pas ce message, le changement de position à l'aide d'un nom de zone pourrait ne pas être pris en compte par l'automatisation.

Si vous rencontrez ce problème, vous pouvez le contourner en utilisant des coordonnées GPS pour spécifier la position du device\_tracker.

## Voir la position d'un device\_tracker sur une carte

Vous pouvez voir la position virtuelle dans le tableau de bord sur une carte de type Carte ou encore directement dans l'option de menu Map.

Pour que la position du virtuel apparaisse il faut donner à l'entité une position GPS et non une position à partir d'une zone.

Par défaut, la carte affichera la première lettre de <a href="fiche-qu\_est-ce\_qu\_une\_entite.md#qu\_est-ce\_qu\_une\_entite">l'identifiant de l'objet</a>.

![device_tracker sur une carte](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-DeviceTrackerSurCarte.png)

## Changer l'image d'un device\_tracker

Le fichier customize.yaml permet d'apporter des personnalisations à différentes entités, notamment l'image utilisée pour représenter un device\_tracker.

Si le fichier n'existe pas encore, créez-le dans le même dossier que configuration.yaml, c'est-à-dire /mnt/data/supervisor/homeassistant.

Ceci peut être réalisé <a href="fiche-la\_console\_home\_assistant.md#la\_console\_home\_assistant">dans le terminal HassOS</a> ou encore à l'aide de <a href="fiche-travailler\_avec\_le\_module\_complementaire\_file\_editor.md#travailler\_avec\_le\_module\_complementaire\_file\_editor">le module complémentaire File editor</a>.

Dans configuration.yaml, vous devez avoir une référence à ce fichier.

Fichier configuration.yaml

homeassistant:  
  customize: !include customize.yaml

Dans le fichier customize.yaml, vous pouvez désormais préciser l'image à utiliser pour le device\_tracker.

Pour utiliser vos propres images, vous devez <a href="fiche-utiliser\_vos\_propres\_images\_dans\_un\_tableau\_de\_bord\_lovelace.md#utiliser\_vos\_propres\_images\_dans\_un\_tableau\_de\_bord\_lovelace">les téléverser sur le Pi dans un dossier précis</a>.

L'image à utliiser peut ensuite être configurée comme suit :

Fichier customize.yaml

device\_tracker.position\_virtuelle\_annie:  
  entity\_picture: /local/annie.png

Redémarrez Home Assistant pour que les configurations soient actives.

Désormais, l'image apparaît sur la carte plutôt que la première lettre de l'identifiant de l'entité.

![device_tracker avec images](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-DeviceTrackerSurCarte-Photos.png)

Source des images : <http://clipart-library.com/clip-art/kid-transparent-background-22.htm>

## Retrouver la latitude et la longitude d'un device\_tracker

Grâce aux <a href="fiche-les\_modeles\_dans\_home\_assistant.md#les\_modeles\_dans\_home\_assistant">modèles</a>, il est possible de retrouver spécifiquement la latitude et la longitude d'un device\_tracker.

D'abord, comme avec n'importe quelle entité, il est possible de connaître les attributs disponibles à partir du menu Outils de développement / Modèle.

Entrez dans la zone de gauche une chaîne au format {{ states.id\_de\_l\_entite }}.

Modèle

{{ states.device\_tracker.position\_virtuelle\_annie }}

Voici le résultat à l'écran lorsque la position a été définie à l'aide de coordonnées GPS.

J'ai ajouté des sauts de ligne pour que les attributs soient plus visibles.

Résultat à l'écran

<template TemplateState(<  
    state device\_tracker.position\_virtuelle\_annie=Travail;  
    source\_type=gps,  
    latitude=46.05123588418276,  
    longitude=-72.00332701206209,  
    gps\_accuracy=0,  
    friendly\_name=position\_virtuelle\_annie  
    @ 2025-11-03T11:04:01.874055-05:00>  
)>

Si la position a été définie à l'aide du nom d'une zone, il y aura moins d'attributs disponibles.

Résultat à l'écran

<template TemplateState(<  
    state device\_tracker.position\_virtuelle\_annie=Travail;  
    source\_type=gps,  
    friendly\_name=position\_virtuelle\_annie  
    @ 2025-11-03T11:15:01.874055-05:00>  
)>

Voici un autre exemple où la position de l'entité n'a pas été redéfinie après un redémarrage de Home Assistant.

Résultat à l'écran

<template TemplateState(<  
    state device\_tracker.position\_virtuelle\_annie=not\_home;  
    source\_type=None,  
    friendly\_name=position\_virtuelle\_annie  
    @ 2025-11-03T11:04:55.752248-05:00>  
)>

Une fois que vous connaissez les attributs disponibles, vous pouvez retrouver spécifiquement la latitude et la longitude si elles sont disponibles.

Modèle

{{ state\_attr('device\_tracker.position\_virtuelle\_annie', 'latitude') }}

Modèle

{{ state\_attr('device\_tracker.position\_virtuelle\_annie', 'longitude') }}