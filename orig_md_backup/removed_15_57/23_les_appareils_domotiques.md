# 21. Les appareils domotiques

## 21.1 Les appareils de la maison intelligente

Une maison intelligente peut comprendre de nombreux appareils contr�l�s par l'unit� centrale du syst�me domotique.

La plupart sont vendus tels quels et ont besoin de peu de configuration pour fonctionner.

Il est �galement possible de cr�er nos propres appareils domotiques gr�ce � des cartes �lectroniques munies d'une puce pour communiquer avec un protocole de communication compatible. Parmi les cartes disponibles, notons le Arduino Nano IoT, l'ESP32 et la carte Z-Wave Z-Uno.

Les appareils peuvent �tre des capteurs, des r�cepteurs ou les deux.

Les capteurs (en anglais�: sensors) r�coltent des donn�es sur l'environnement et les envoient � la bo�te domotique. Par exemple, un d�tecteur de mouvement pourra envoyer un signal d�s qu'il d�tecte un mouvement. Un thermom�tre enverra la temp�rature actuelle d�s qu'un changement de temp�rature survient.

Les r�cepteurs (en anglais : receivers) fonctionnent � l'inverse�: ils effectuent une op�ration en fonction des donn�es qu'ils re�oivent de la bo�te domotique. On pourra par exemple avoir une ampoule qui s'allume � une intensit� donn�e, change de couleur ou s'�teint. Une prise de courant peut s'ouvrir ou se refermer. Un moteur peut se mettre en marche ou s'arr�ter.

Voici un �chantillon d'appareils domotiques int�ressants qui communiquent en Z-Wave.

## Prise de courant

* [Prise Z-Wave Plus Fruugo](https://www.fruugo.ca/z-wave-plus-smart-plug-us-power-socket-home-automation-system-9084mhz-frequency-energy-efficie/p-333650810-735358798)�(environ CDN $55)
* [PRISE Z-Wave Zooz](https://www.aartech.ca/zen04-800lr)�(environ CDN $40)

## Interrupteur de lumi�re

* [Interrupteur Z-Wave Zooz](https://www.aartech.ca/zen77-800lr)�(environ CDN $50)
* [Interrupteur Z-Wave Leviton](https://www.homedepot.ca/produit/leviton-interrupteur-decora-smart-z-wave-serie-800-en-blanc-fil-neutre-requis-/1001898914) (environ CDN $60)

## D�tecteur de mouvements

* [D�tecteur de mouvements Z-Wave Zooz](https://www.aartech.ca/zse18-800lr)�(environ CDN $50)
* [D�tecteur de mouvement Z-Wave Homeseer](https://www.aartech.ca/ms100-g8)�(environ CDN $60)

## D�tecteur de fuites d'eau

* [HomeSeer G8 Z-Wave Plus Long Range Water Leak Sensor](https://www.aartech.ca/ls100-g8) (environ CDN $60)

## Relais

Un relais est en fait un interrupteur. Il permet de faire passer le courant ou de l'arr�ter de fa�on � faire tourner un moteur ou non.

En domotique, le relais pourra �tre contr�l� � distance.

Le relais sera branch� dans une prise de courant, dans un interrupteur mural ou encore directement dans une bo�te �lectrique.

* [Shelly Qubino Wave i4 DC ZWave 800 4 Input Module](https://www.aartech.ca/shelly-wave-i4-dc) (environ CDN $25)

## Localisateurs d'objets

Les localisateurs d'objets (trackers) permettent au syst�me domotique de r�agir, par exemple, lorsque le sac d'�cole auquel un localisateur d'objet est attach� arrvie � la maison.

Le protocole de communication n'est pas Z-Wave mais bien Bluetooth low energy (BLE).

Parmi les fabricants de localisateurs d'objets, notons�:

* [Tile](https://www.thetileapp.com/en-us/store/tiles/sticker)
* [Cube](https://cubetracker.com/collections/all)
* [Nut](https://www.nutfind.com/collections/all)

## Pour plus d'information

��Top 15 Sensor Types Being Used in IoT��. Finoit. <https://www.finoit.com/blog/top-15-sensor-types-used-iot/>

## 21.2 Pr�cautions avant l'achat d'un objet connect�

Il existe une multitude d'objets connect�s mais tous ne peuvent pas n�cessairement communiquer avec votre bo�te domotique.

Il faut donc effectuer quelques v�rifications avant de proc�der � l'achat d'un tel appareil.

## Protocole de communication

Le�[apical\_lien\_interne][passerelle\_et\_protocoles\_de\_communication,protocole de communication][/apical\_lien\_interne] utilis� par l'objet connect� est un des principaux facteurs � consid�rer.

En effet, les objets peuvent communiquer dans diff�rentes normes ou protocoles de communication�: Z-Wave, Zigbee, Wi-Fi, Bluetooth, RFXcom, etc.

La bo�te domotique, de son c�t�, peut inclure diff�rentes passerelles pour communiquer dans ces protocoles.

Les protocoles support�s par les bo�tes domotiques commerciales sont pr�-d�termin�s et vous devez v�rifier les sp�cifications techniques pour les conna�tre.

Les bo�tes domotiques DIY, quant � elles, peuvent communiquer dans n'importe quel protocole pour autant que vous leur ajoutiez la passerelle ad�quate, g�n�ralement sous forme de cl� USB ou de carte d'extension.

Par exemple, la cl� USB Z-Wave permettra � une bo�te domotique DIY de communiquer avec des objets connect�s � l'aide du protocole Z-Wave.

## Fr�quence

La fr�quence utilis�e par un protocole peut diff�rer selon le pays d'origine de l'appareil. C'est le cas par exemple avec les appareils Z-Wave.

Avant d'acheter un appareil domotique avec une puce Z-Wave, il faut s'assurer qu'il utilise la bonne fr�quence. Par exemple,�au Canada et aux �tats-Unis, Z-Wave utilise une fr�quence de 908.4 MHz.

Si vous projetez d'acheter un objet connect� Wi-Fi, il faut �galement v�rifier s'il utilise la fr�quence 2.4 GHz ou 5 GHz ou les deux de m�me que quelles fr�quences sont disponibles sur votre r�seau. G�n�ralement, les objets connect�s Wi-Fi communiquerons en 2.4 GHz puisque cette fr�quence offre une plus grande port�e.

Si l'appareil ne peut communiquer qu'en 2.4 GHz alors que la seule fr�quence disponible est le 5 GHz, aucune communication ne sera possible.

## Compatibilit� avec le logiciel de domotique

Il faut �galement v�rifier la compatibilit� de l'objet avec [apical\_lien\_interne][quelques\_logiciels\_de\_domotique\_interessants,la bo�te domotique][/apical\_lien\_interne] que vous avec choisie.

Avec certains logiciels de domotique, il faut utiliser une extension (plugin, add-on) pour permettre le pairage avec un appareil connect�. Ces extension sont parfois �crites sp�cifiquement pour une marque donnn�e.

Par exemple, le logiciel Jeedom n�cessite l'extension [document�e ici](https://jeedom-plugins-extra.github.io/plugin-Wifi-Smartplug/fr_FR/) pour contr�ler les prises intelligentes TP Link HS100 et HS110. Mais au moment d'�crire ces lignes, aucune extension ne permettait de communiquer avec les prises intelligentes de marque Teckin. V�rifiez donc la disponibilit� des extensions avant d'acheter vos appareils connect�s.

## 21.3 Construire son propre objet connect�

Information � venir...

Carte Z-uno�: <https://www.amazon.ca/Z-Uno-Universal-Z-Wave-Create-Devices/dp/B01IRBDBZY> (environ CDN $95)

## Pour plus d'information

��Z-Uno Z-Wave IoT Development Board��. hackaday.io. <https://hackaday.io/project/26903-z-uno>

��Indoor Sensing Hub powered by Mozilla Things Framework��. Jo�o Pedro Dias. <https://jpdias.me/hardware/iot/2018/12/19/indoorsensing.html>

## 21.4 Prises Wi-Fi vs Z-Wave vs ZigBee

Les prises intelligentes Wi-Fi sont tr�s populaires et plus abordables que les prises Z-Wave ou ZigBee.

Mais il y a un mais.

Je vous pr�sente ici quelques grandes lignes pour guider votre choix sur la prise intelligente � acheter.

|  |  |  |  |
| --- | --- | --- | --- |
|  | Wi-Fi | Z-Wave | ZigBee |
| Co�t | Plus abordable, souvent aux alentours de 10$ | Plus cher, souvent aux alentours de 50$ | Moyennement cher, souvent aux alentours de 20$ |
| Bo�te domotique | Aucune bo�te domotique � installer, se branche � un serveur externe et est contr�l� par un t�l�phone intelligent | Boite domotique � installer, par exemple Jeedom ou Home Assistant | Boite domotique � installer, par exemple Jeedom ou Home Assistant.  Est aussi support� par Amazon Echo Plus. |
| Confidentialit� des donn�es | Transitent sur un serveur externe | Sont conserv�es chez vous sur votre bo�te domotique | Sont conserv�es chez vous sur votre bo�te domotique |
| Consid�rations techniques | Doit �tre pr�s de votre routeur sans fil, selon sa port�e th�orique.  Le t�l�phone doit pouvoir se brancher sur un r�seau 2.4 GHz pour la configuration initiale de la prise. | Port�e th�orique de 100 � 200 m�tres selon la version, port�e pratique aux alentours de 30 m�tres pour la plus ancienne version.  D'autres appareils Z-Wave peuvent servir de relai | Port�e th�orique de 10 � 100 m�tres selon la version.  D'autres appareils ZigBee peuvent servir de relai |
| Ind�pendance | La prise ne pourra pas �tre contr�l�e � distance si le serveur externe est en panne. Vous �tes donc d�pendant de l'infonuagique. | --- | --- |

## Pour plus d'information

��nRF52840-DK Range Testing With BLE, ZigBee and Thread Protocols at 0, 4 and 8dBm Transmit Power Settings��. DevZone. <https://devzone.nordicsemi.com/nordic/nordic-blog/b/blog/posts/nrf52840-dk-range-testing-with-ble-zigbee-and-thread-protocols-at-0-4-and-8dbm-transmit-power-settings>
