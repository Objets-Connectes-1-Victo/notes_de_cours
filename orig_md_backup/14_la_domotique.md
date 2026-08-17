# 12. La domotique

## 12.1 En r�sum�...

Voici un r�sum� des informations essentielles du ou des prochains chapitres.

Notez que certaines fiches, qui font partie int�grante du cours, pourraient ne pas figurer dans ce r�sum�.

Je vous recommande d'effectuer une lecture de l'ensemble des fiches de ces chapitres afin de bien saisir les enjeux.

## [apical\_lien\_interne]qu\_est-ce\_qu\_un\_objet\_connecte[/apical\_lien\_interne]

Un objet connect�, parfois appel� appareil connect� ou appareil intelligent, c'est un objet de tous les jours dans lequel on a ajout� des composantes qui lui permettent d'envoyer ou de recevoir des donn�es au serveur auquel il est connect�.

Les objects connect�s font partie d'une grande famille qu'on appelle Internet des Objets ou, en anglais, Internet of Things (IoT).

![Apple Watch](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/AppleWatch.png) ![Prise intelligente Wi-Fi](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/PriseIntelligenteWiFi.png) ![Penne dormant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/PenneDormantIntelligent.png)

## [apical\_lien\_interne]qu\_est-ce\_qu\_un\_systeme\_domotique[/apical\_lien\_interne]

Un syst�me domotique, c'est diff�rent d'une s�rie d'objets connect�s. Avec un syst�me domotique, on a un contr�le centralis� alors qu'avec une s�rie d'objets connect�s, on aura souvent une application pour chacun des objets.

![Sch�ma syst�me domotique](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/SystemeDomotique.png)

## [apical\_lien\_interne]systeme\_domotique\_cle\_en\_main\_vs\_diy[/apical\_lien\_interne]

Lorsque les donn�es sont transmises dans l'infonuagique, attention aux�[apical\_lien\_interne][systeme\_domotique\_cle\_en\_main\_vs\_diy,trous de s�curit�,securite][/apical\_lien\_interne].

## [apical\_lien\_interne]un\_raspberry\_pi\_comme\_unite\_centrale[/apical\_lien\_interne]

Vous aurez besoin de�:

* Un Raspberry Pi 3 ou 4
* Un bloc d'alimentation d'au moins 2.5A
* Une carte micro SD (classe 10, min. 16 Go) - pour la phase de test (un disque dur est plus robuste qu'une carte micro SD)
* Un bo�tier
* Un syst�me d'exploitation
* Possiblement un �cran et un clavier

![Mon bo�tier Raspberry Pi en Lego](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/BoitierRaspberryPiLegos-1.png)

## [apical\_lien\_interne]bien\_traiter\_son\_raspberry\_pi[/apical\_lien\_interne]

Prot�ger le Pi avec un bo�tier.

![Bo�tiers](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/RaspberryPi-Boitiers.png)

Installer des dissipateurs thermiques.

![dissipateurs sur le Raspberry Pi](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/RaspberryPi-Heatsink.png)

Installer un ventilateur.

![Ventilateur](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/RaspberryPi-VentilateurBoitier.png)

Ne pas enrouler le fil du bloc d'alimentation.

![Fil du bloc d'alimentation roul� sur lui-m�me](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/RaspberryPi-FilEnroule.png)

Attention quand il faut retirer la carte micro SD.

![Compartiment de la carte micro SD bris�](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/RaspberryPi-CompartimentCarteBrise.png)

Arr�ter le Pi de la bonne fa�on.

![sudo halt](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/RaspberryPi-SudoHalt.png)

![�teindre Jeedom](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Jeedom-EteindreDeFaconSecurisee.png)

## [apical\_lien\_interne]quelques\_logiciels\_de\_domotique\_interessants[/apical\_lien\_interne]

Jeedom

![Sch�ma installation Jeedom](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/InstallationJeedom.png)

Home Assistant

![Installation Home Assistant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/InstallationHomeAssistant.png)

## [apical\_lien\_interne]ifttt[/apical\_lien\_interne]

IFTTT signifie IF�This, Then That.

Service Web gratuit qui permet d'automatiser des t�ches pour des objets connect�s Wi-Fi entre eux - par exemple un capteur de mouvement et une prise intelligente - ou entre les objets et des services Web - par exemple Gmail, Facebook, Google Assistant.

Il peut �tre utililis� par-dessus une bo�te domotique via une extension ou encore de fa�on autonome.

IFTTT fonctionne avec le principe d'un d�clencheur (trigger), le�this�et d'une action, le�that. Par exemple, le d�clencheur pourrait �tre l'envoi d'un courriel dont le titre est ��J'ai froid�� et l'action serait de d�marrer le chauffage.

## [apical\_lien\_interne]installation\_de\_jeedom\_et\_premier\_acces[/apical\_lien\_interne]

Suivez bien les �tapes!

Je vous les r�sume ici.

* Ins�rer la carte micro SD dans l'ordinateur.
* Installer Raspberry Pi OS Lite sur la carte micro SD � l'aide de Raspberry Pi Imager. Prendre soin de configurer le nom et le mot de passe de l'usager Linux, le r�seau sans fil et l'activation SSH.
* Je vous conseille d'attendre au prochain cours pour configurer l'adresse IP statique.
* Ins�rer la carte micro SD dans le PI, brancher un �cran au Pi puis d�marrer.
* Id�alement, brancher un c�ble r�seau (plus stable que le Wi-Fi).
* V�rifier l'acc�s au r�seau.

  Terminal du Raspberry Pi

  ping google.com
* Mettre le syst�me � jour (ceci pourrait �tre fait au prochain cours pour gagner un peu de temps).

  Terminal du Raspberry Pi

  sudo apt update  
  sudo apt upgrade
* V�rifier l'adresse IP du Pi.

  Terminal du Raspberry Pi

  hostname -I
* Lancez la commande suivante pour installer Jeedom :

  Terminal du Raspberry Pi

  wget -O- https://raw.githubusercontent.com/jeedom/core/master/install/install.sh | sudo bash
* Red�marrez le Pi.

  Terminal du Raspberry Pi

  sudo reboot
* Acc�der � Jeedom � partir de l'ordinateur en entrant l'adreses IP dans un navigateur. L'ordinateur doit �tre connect� au r�seau Domotique-Pedago si le Pi est configur� pour communiquer en Wi-Fi ou sur CEGEPVICTO si le Pi est c�bl� vers le commutateur d�di�.

## [apical\_lien\_interne]copie\_de\_securite\_de\_jeedom[/apical\_lien\_interne]

La sauvegarde permet de remettre rapidement Jeedom en �tat de marche si un probl�me survenait.

Pour lancer une sauvegarde manuelle, rendez-vous�dans le menu�R�glages�/�Syst�me�/�Sauvegardes�puis cliquez�sur�Lancer une sauvegarde.

Il existe aussi un syst�me de sauvegarde automatique mais ce n'est pas ce qui nous int�resse pour l'instant.

Important : que ce soit une sauvegarde manuelle ou automatique, il faut la t�l�charger sur notre ordinateur pour pouvoir la r�utiliser en cas de crash de Jeedom.

## 12.2 Qu'est-ce qu'un objet connect� ?

Un objet connect�, parfois appel� appareil connect� ou appareil intelligent, c'est un objet de tous les jours dans lequel on a ajout� des composantes qui lui permettent d'envoyer ou de recevoir des donn�es au serveur auquel il est connect�.

C'est ainsi que les objets sont devenus intelligents.

L'Office qu�b�cois de la langue fran�aise d�finit un objet connect� comme suit[1](http://gdt.oqlf.gouv.qc.ca/ficheOqlf.aspx?Id_Fiche=26544584)�:

> Objet qui est capable, outre sa fonction principale, d'envoyer ou de recevoir des informations par l'interm�diaire d'un r�seau de t�l�communication.

![Apple Watch](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/AppleWatch.png) ![Prise intelligente Wi-Fi](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/PriseIntelligenteWiFi.png) ![Penne dormant](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/PenneDormantIntelligent.png)

## Objets connect�s pr�ts-�-porter

Les objets connect�s pr�ts-�-porter (en anglais�: wearables ou smartwear) forment un sous-ensemble des objets connect�s. Il s'agit d'objets qu'une personne porte sur elle, par exemple une montre, une ceinture, des boucles d'oreille et m�me le tissus d'un v�tement, qui permettent de capter puis de transmettre des informations sur la condition physique de la personne.

## Internet des objets

Les objects connect�s font partie d'une grande famille qu'on appelle Internet des Objets ou, en anglais, Internet of Things (IoT).

Voici une d�finition int�ressante de l'Internet des Objets[2](https://jpdias.me/hardware/iot/2018/12/19/indoorsensing.html)�:

> The Internet-of-Things can be seen as the result of the interconnection via the Internet of computing devices embedded in everyday objects, enabling them to send and receive data. This paradigm-shift provoked a ripple effect transforming everyday objects into smart objects [...].

## Source

1. ��objet connect頻. Office qu�b�cois de la langue fran�aise. <http://gdt.oqlf.gouv.qc.ca/ficheOqlf.aspx?Id_Fiche=26544584>

2. ��Indoor Sensing Hub powered by Mozilla Things Framework��. Jo�o Pedro Dias. <https://jpdias.me/hardware/iot/2018/12/19/indoorsensing.html>

## 12.3 Qu'est-ce qu'un syst�me domotique ?

La domotique est un ensemble de composantes et de techniques qui permettent d'automatiser et de contr�ler � distance diff�rents syst�mes dans une maison.

Mais attention�: un syst�me domotique, c'est diff�rent d'une s�rie d'[apical\_lien\_interne][qu\_est-ce\_qu\_un\_objet\_connecte,objets connect�s][/apical\_lien\_interne]. Avec un syst�me domotique, on a un contr�le centralis� alors qu'avec une s�rie d'objets connect�s, on aura souvent une application pour chacun des objets.

## La bo�te domotique (hub)

Pour qu'on parle de domotique il faut que le contr�le soit centralis�.

L'endroit o� le contr�le centralis� s'op�re s'appelle bo�te domotique ou syst�me de gestion domotique.

En France, les gens l'appellent�box domotique. Et en anglais, on parle de hub, smart hub ou encore smart home hub.

La bo�te domotique sera compos�e de :

* Une unit� centrale
* Un logiciel de domotique
* Une passerelle (gateway)

## Le syst�me domotique

Le syst�me domotique complet comprendra�:

* Une bo�te domotique (unit� centrale, logiciel de domotique et passerelle)
* Des appareils connect�s
* Un ou plusieurs appareils pour contr�ler le syst�me � distance

Diff�rents protocoles de communication seront utilis�s pour assurer la communication entre la bo�te domotique et les appareils connect�s.

![Sch�ma syst�me domotique](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/SystemeDomotique.png)

## 12.4 Syst�me domotique cl� en main vs DIY

De nombreux acteurs sur le march� offrent des solutions domotiques cl� en main. Ces solutions sont g�n�ralement stables, efficaces et s�curitaires. Cependant, elles sont co�teuses � l'achat et plusieurs n�cessitent par la suite des frais mensuels.

Si vous �tes le moindrement�[apical\_lien\_interne][pourquoi\_effectuer\_une\_veille\_technologique,geek,geek][/apical\_lien\_interne], vous aimerez certainement monter votre propre syst�me domotique. Certains ne n�cessitent aucune programmation, seulement de la configuration. D'autres doivent �tre programm�s de toutes pi�ces alors qu'une troisi�me cat�gorie utilise des modules existants et vous permet d'y ajouter vos propres modules.

Attention : lors du choix du logiciel de domotique � utiliser, v�rifiez bien les frais encourus. Certains sont compl�tement libres (Open Source) alors que d'autres vous demanderont de sortir votre porte feuille, mais � moindre co�t que pour une solution cl� en main.

Dans tous les cas, vous devrez apporter une attention quasi maladive pour la s�curit� de votre syst�me afin de ne pas compromettre votre maison face aux personnes malveillantes. Saviez-vous que des images de cam�ras de surveillance dont le mot de passe n'avait pas �t� chang� sur la plateforme Web [se sont retrouv�es sur des sites pirates](https://ici.radio-canada.ca/nouvelle/1805366/webcam-camera-vie-privee-diffusion-iot)? Le fait qu'un objet connect� diffuse des informations dans l'infonuagique est certainement un facteur de risque � consid�rer.

Quoi qu'il en soit, la domotique est un monde fascinant qui offre une infinit� de possibilit�s.

Si la domotique vous interpelle, suivez-moi�!
