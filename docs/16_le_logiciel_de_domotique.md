# 14. Le logiciel de domotique {#chapitre-le_logiciel_de_domotique}

## 14.1 Quelques logiciels de domotique intéressants {#fiche-quelques_logiciels_de_domotique_interessants}

Les boîtes domotiques commerciales incluent un logiciel de domotique. Chaque compagnie a son propre logiciel et généralement, il n'est pas possible de le changer.

Si vous montez votre boîte domotique avec un Raspberry Pi, vous pouvez y installer un logiciel que vous aurez codé ou encore travailler avec un des nombreux logiciels libres (Open Source) sur le marché. Une communauté active travaille sur chacun d'entre eux et contribue à leur amélioration au niveau des fonctionnalités, de la convivialité et de la sécurité.

## Jeedom

Jeedom peut être installé gratuitement sur un Raspberry Pi en version DIY. Il est également possible d'acheter une boîte domotique Jeedom prête à l'emploi.

Dans la version DIY, en plus des modules existants, vous pouvez programmer vos propres modules Jeedom en PHP : <https://www.jeedom.com/site/fr/dev.html>.

Jeedom vous intéresse? Commencez ici : [installation\_de\_jeedom\_et\_premier\_acces](17_jeedom_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_jeedom_et_premier_acces).

## Home Assistant

Home Assistant est un excellent logiciel domotique à code source ouvert qui peut être installé sur un Raspberry Pi.

Il peut tourner par-dessus le système d'exploitation de votre choix (on parlera alors de [Home Assistant Supervised](https://github.com/home-assistant/supervised-installer)), par-desssus Raspberry Pi OS (on parlera de [Home Assistant Core](https://www.home-assistant.io/docs/installation/raspberry-pi/)) ou, selon la technique recommandée, par-dessus le système d'exploitation Home Assistant Operating System, aussi appelé HassOS ou Hass.io. Ce système d'exploitation est basé sur resinOS.

Pour vous lancer avec Home Assistant, suivez le guide : [installation\_de\_home\_assistant\_et\_premier\_acces](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_home_assistant_et_premier_acces).

## Autres logiciels

OpenNetHome : <http://opennethome.org/>

openHAB : <https://www.openhab.org/>

Node-RED : <https://nodered.org/>

WebThings : <https://webthings.io/>

Domoticz : <https://www.domoticz.com/>

etc.

## 14.2 IFTTT {#fiche-ifttt}

IFTTT signifie IF This, Then That. Traduction libre : Si ceci alors cela.

Mais IFTTT, c'est quoi exactement?

C'est un service Web gratuit qui permet d’automatiser des tâches pour des objets connectés Wi-Fi entre eux — par exemple un capteur de mouvement et une prise intelligente — ou entre les objets et des services Web — par exemple Gmail, Facebook, Google Assistant.

IFTTT fonctionne avec le principe d'un déclencheur (trigger), le this et d'une action, le that. Par exemple, le déclencheur pourrait être l'envoi d'un courriel dont le titre est « J'ai froid » et l'action serait de démarrer le chauffage.

## IFTTT vs boîte domotique

Dans la plupart des boîtes domotiques, par exemple [Jeedom](17_jeedom_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_jeedom_et_premier_acces) ou [Home Assistant](66_home_assistant_au_coeur_de_votre_systeme_domotique.md#fiche-installation_de_home_assistant_et_premier_acces), le système de scénarios, parfois appelés automatisation, est plus puissant que IFTTT.

Cependant, IFTTT n'est pas sans intérêt puisqu'il peut être utililisé par-dessus une boîte domotique via une extension ou encore de façon autonome, appuyé par une application du genre de [Smart Life](https://ifttt.com/smartlife).

Grâce à IFTTT, il est plus facile d'intégrer à une boîte domotique des objets connectés Wi-Fi à prime abord non compatibles.

## Pour plus d'information {#soumettreauthentification}

« IFTTT - Every thing works better together ». IFTTT. <https://ifttt.com/>

« IFTTT et Domotique : Comment automatiser les interactions entre les périphériques wifi? ». Domo Blog. <https://www.domo-blog.fr/ifttt-et-domotique-comment-automatiser-les-interactions-entre-les-peripheriques-wifi/>

« Using IFTTT with the Raspberry Pi ». The Pi Hut. <https://thepihut.com/blogs/raspberry-pi-tutorials/using-ifttt-with-the-raspberry-pi>

« IFTTT et Jeedom : Comment utiliser les périphériques wifi avec le système domotique ». Domo Blog. <https://www.domo-blog.fr/ifttt-et-jeedom-comment-utiliser-les-peripheriques-wifi-avec-le-systeme-domotique/#:~:text=IFTTT%20permet%20%C3%A0%20Jeedom%20de,largement%20dans%20toute%20la%20maison.>

« Smart Life : comment dompter le « couteau Suisse » de la maison connectée ? ». Les Alexiens. <https://www.lesalexiens.fr/tutoriels/tutoriel-comment-dompter-smart-life-le-couteau-suisse-de-la-maison-connectee/>