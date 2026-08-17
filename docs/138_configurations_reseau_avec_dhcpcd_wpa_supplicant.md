<a id="fiche-configurer_le_reseau_a_l_aide_de_dhcpcd"></a>
# 120. Configurations réseau avec dhcpcd (wpa_supplicant)

## 120.1 Configurer le réseau à l'aide de dhcpcd

Depuis Raspberry Pi OS Bookworm (2023), la gestion du réseau est réalisée avec [NetworkManager](https://networkmanager.dev/). Auparavant, le gestionnaire de réseau par défaut était [dhcpcd](https://github.com/NetworkConfiguration/dhcpcd).

Pour vérifier si le système d'exploitation du Raspberry Pi utilise dhcpcd, entrez cette commande :

Terminal du Pi

systemctl status dhcpcd

Si vous voyez Active: active, c'est que l'OS utilise dhcpcd comme gestionnaire de réseau.

Si vous voyez plutôt Unit dhcpcd.service could not be found, c'est que l'OS utilise un auytre système pour gérer le réseau, possiblement NetworkManager.

Pour configurer le réseau avec NetworkManager, référez-vous à la fiche <a href="fiche-configurer_le_reseau_wi-fi_sur_le_raspberry_pi.md#configurer_le_reseau_wi-fi_sur_le_raspberry_pi">sur NetworkManager</a>.
<a id="surcartedhcpcd"></a>

## Configurer le réseau à l'aide de dhcpcd

Si le système d'exploitation du Raspberry Pi utilise dhcpcd, voici les instructions à suivre pour configurer le réseau sans fil.

Après le démarrage du Raspberry Pi, accédez au Terminal à l'aide d'un écran ou via SSH.

Vous trouverez le fichier wpa_supplicant.conf dans le dossier /etc/wpa_supplicant.

Avant de poursuivre, prenez une copie de sécurité du fichier. De cette façon, vous pourrez remettre les configurations originales en place en cas de problème.

Terminal

sudo cp /etc/wpa_supplicant/wpa_supplicant.conf /etc/wpa_supplicant/wpa_supplicant_backup.conf

Pour éditer le fichier wpa_supplicant.conf, entrez la commande :

Terminal

sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

Copiez les instructions suivantes dans le fichier. Ajustez le nom du réseau et le mot de passe pour y accéder.

Si vous n'êtes pas au Canada, changez CA pour le [code à 2 lettres de votre pays](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes).

Fichier wpa_supplicant.conf

country=CA  
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev  
update_config=1  
  
network={  
    ssid="NOM-DU-RESEAU"  
    psk="MOT-DE-PASSE-DU-RESEAU"  
}

ou, pour pemettre de se brancher à un réseau non sécurisé (sans mot de passe) :

Fichier wpa_supplicant.conf

...  
  
network={  
    ssid="NOM-DU-RESEAU"  
    key_mgmt=NONE  
}

Il est possible de configurer plusieurs réseaux si tel est votre besoin. Simplement ajouter une autre section network. Le système se branchera au réseau le plus puissant à moins que vous ajoutiez une priorité à l'aide de priority=1, priority=2, etc., le plus gros chiffre ayant la plus haute priorité.

Fichier wpa_supplicant.conf

...  
  
network={  
    ...  
}  
  
network={  
    ...  
}

Pour enregistrer le fichier, appuyez sur Ctrl + X puis O (ou Y si votre OS est en anglais).

## Configuration directement sur la carte micro SD alors qu'elle est insérée dans votre ordinateur

Il est possible de configurer le réseau sans fil directement sur la carte micro SD. Cette méthode permet une configuration headless, c'est-à-dire que vous n'avez pas besoin de brancher écran et clavier sur le Pi. Vous n'avez pas non plus besoin de vous brancher au Pi via SSH.

Alors que la carte micro SD est insérée dans votre ordinateur, créez un fichier nommé [wpa_supplicant.conf](https://linux.die.net/man/5/wpa_supplicant.conf) à la racine de sa partition boot (ou bootfs, selon votre système).

Sous Windows, utilisez l'utilitaire de texte de votre choix.

Sous Mac ou Linux, utilisez ces commandes :

Terminal

cd /Volumes/boot  
sudo nano wpa_supplicant.conf

Remarque : ce fichier sera automatiquement déplacé vers le dossier /etc/wpa_supplicant la première fois que le Pi sera démarré.

Entrez les configurations requises dans ce fichier, [comme expliqué plus haut](https://apical.xyz/formations/pageunique/systeme_domotique_diy#dhcpcd).

## Pour plus d'information

« wpa_supplicant ». Arch Linux. <https://wiki.archlinux.org/index.php/Wpa_supplicant>

## 120.2 Connecter le Pi à un autre des réseaux listés dans wpa_supplicant.conf

Il est possible de définir plusieurs réseaux dans le fichier wpa_supplicant.conf.

Ceci est pratique par exemple si vous devez travailler avec le Raspberry Pi à différents endroits, par exemple au travail et à la maison.

C'est également intéressant si un même espace de travail offre plusieurs réseaux, par exemple un réseau 2.4 GHz et un 5 GHz ou encore un réseau ouvert et un autre réseau qui offre des possibilités limitées.

Le Pi se connectera généralement au réseau qui offre le meilleur signal.

Il est possible de connecter le Pi à l'un ou à l'autre de ces réseaux sans avoir à modifier le fichier wpa_supplicant.conf ni à redémarrer le Pi.

## Définir plusieurs réseaux

Pour définir les réseaux, lancez cette commande :

Terminal

sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

Vous pourrez définir dans ce fichier autant de réseaux que désiré :

Fichier wpa_supplicant.conf

country=CA  
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev  
update_config=1  
  
network={  
    ssid="NOM-DU-RESEAU"  
    psk="MOT-DE-PASSE-DU-RESEAU"  
}

 

network={  
    ssid="UN-AUTRE-RESEAU"  
    psk="MOT-DE-PASSE-DU-RESEAU"  
}  
  
network={  
    ssid="UN-RESEAU-NON-SECURISE"  
    key_mgmt=NONE  
}

## Lister les réseaux configurés

Pour vous connecter à un réseau donné, vous aurez besoin de la liste des réseaux configurés et de leur identifiant.

Terminal

wpa_cli list_networks

Résultat à l'écran

pi@raspberrypi:~ $ wpa_cli list_networks  
Selected interface 'p2p-dev-wlan0'  
network id / ssid / bssid / flags  
0      NOM-DU-RESEAU any  
1      UN-AUTRE-RESEAU any   
2      UN-RESEAU-NON-SECURISE any

## Sélectionner le réseau désiré

Vous devez utilisler l'identifiant du réseau afin de le sélectionner.

Terminal

wpa_cli -i wlan0 select_network 1

Le système répondra simplement OK.

## Vérifier si tout a fonctionné

Avant de crier victoire, vous devez effectuer deux vérifications.

### Connexion au réseau

Vous devez d'abord vérifier si le Pi est effectivement connecté au réseau choisi.

Terminal

iwconfig

Résultat à l'écran

pi@raspberrypi:~ $ iwconfig  
lo      no wireless extensions.

 

eth0    no wireless extensions.

 

wlan0   IEEE 802.11 ESSID:"UN-AUTRE-RESEAU"  
        Mode:Managed Frequency:5.18 GHz Access Point: 00:0C:E6:88:DA:13  
        Bit Rate=200 Mb/s Tx-Power=31 dBm  
        Retry short limit:7 RTS thr:off Fragment thr:off  
        Power Management:on  
        Link Quality=70/70 Signal level=-39 dBm  
        Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0  
        Tx excessive retries:0 Invalid misc:0 Missed beacon:0

Notez que la connexion au réseau pourrait prendre un peu de temps. Si vous obtenez ESSID:off/any au lieu du nom du réseau, réessayez dans quelques instants, tout pourrait rentrer dans l'ordre.

Si vous n'arrivez pas à vous connecter à ce réseau, c'est peut-être parce que le nom du réseau ou le mot de passe ne sont pas bien entrés dans wpa_supplilcant.conf ou encore que le réseau n'est pas disponible pour le moment.

### Adresse IP

Une fois que vous avez la confirmation d'être connecté au réseau, vous devez vous assurer d'avoir une adresse IP.

Terminal

hostname -I

Si vous obtenez une ligne blanche, vous devrez redemander une adresse IP au serveur DHCP :

Terminal

sudo dhclient -v wlan0

Résultat à l'écran

pi@raspberrypi:~ $ sudo dhclient -v wlan0  
Internet Systems Consortium DHCP Client 4.4.1  
Copyright 2004-2018 Internet Systems Consortium.  
All rights reserved.  
For info, please visit https://www.isc.org/software/dhcp/

 

Listening on LPF/wlan0/dc:a6:32:67:f4:9b  
Sending on LPF/wlan0/dc:a6:32:67:f4:9b  
Sending on Socket/fallback  
DHCPREQUEST for 192.168.1.145 on wlan0 to 255.255.255.255 port 67  
DHCPNAK from 192.168.1.1  
DHCPDISCOVER on wlan0 to 255.255.255.255 port 67 interval 4  
DHCPOFFER of 192.168.1.6 from 192.168.1.1  
DHCPREQUEST for 192.168.1.6 on wlan0 to 255.255.255.255 port 67  
DHCPACK of 192.168.1.6 from 192.168.1.1  
Too few arguments.  
Too few arguments.  
<a id="surlepiavant2023"></a>
bound to 192.168.1.6 -- renewal in 1880 seconds.

## 120.3 Configurer l'adresse IP statique du Raspberry Pi avec dhcpcd

Depuis Raspberry Pi OS Bookworm (2023), la gestion du réseau est réalisée avec [NetworkManager](https://networkmanager.dev/). Auparavant, le gestionnaire de réseau par défaut était [dhcpcd](https://github.com/NetworkConfiguration/dhcpcd).

Pour vérifier si le système d'exploitation du Raspberry Pi utilise dhcpcd, entrez cette commande :

Terminal du Pi

systemctl status dhcpcd

Si vous voyez Active: active, c'est que l'OS utilise dhcpcd comme gestionnaire de réseau.

Si vous voyez plutôt Unit dhcpcd.service could not be found, c'est que l'OS utilise un auytre système pour gérer le réseau, possiblement NetworkManager.

Pour configurer une adresse IP statique avec NetworkManager, référez-vous à la fiche <a href="fiche-donner_une_adresse_ip_statique_au_raspberry_pi.md#donner_une_adresse_ip_statique_au_raspberry_pi">sur NetworkManager</a>.
<a id="autrereseauavant2023"></a>

Sinon, les configurations avec dhcpcd sont expliquées ici. Continuez votre lecture!

## Configurer l'adresse IP statique du Raspberry Pi à l'aide de dhcpcd

Pour configurer l'adresse IP statique du Pi avec dhcpcd :

* Éditez le fichier dhcpcd.conf.

  Terminal

  sudo nano /etc/dhcpcd.conf
* Le fichier donne un exemple de configuration dans la section Example static IP configuration. Il vous suffit d'enlever les # devant les lignes puis d'entrer les valeurs désirées.
  + interface : eth0 pour le réseau câblé, wlan0 pour le sans fil
  + static ip_address : l'adresse statique désirée. Cette adresse peut être n'importe quoi dans la plage 192.168.1.2 à 192.168.1.254 (la plage disponible peut être différente selon les configurations de votre réseau).

    Important : l'adresse utilisée ne doit pas être déjà attribuée à un autre élément du réseau.

    Souvent, les gestionnaires de réseaux réservent une plage pour les adresses statiques. Adressez-vous au gestionnaire de votre réseau pour connaître les adresses disponibles.

    On ajoutera /24 à la fin pour indiquer que les 3 premiers octets sont le masque de sous-réseau.
  + static routers : adresse IP locale du routeur. Si vous avez utilisé le masque /24, il s'agit des 3 premiers nombres de l'adresse IP avec un 1 comme dernier nombre (ex : 192.168.1.1)
  + static domain_name_servers : entrez l'adresse IP du ou des serveurs de noms de domaine (en anglais : nameserver, DNS) de votre réseau suivie de 8.8.8.8 (serveur DNS de Google). Les différentes adresses doivent être séparées par un espace.

    Pour connaître les serveurs de noms de domaine utilisés par votre ordinateur, <a href="fiche-donner_une_adresse_ip_statique_au_raspberry_pi.md#donner_une_adresse_ip_statique_au_raspberry_pi">suivez ce lien</a>.

    Fichier resolv.conf

    #Example static IP configuration:

     

    interface wlan0  
    static ip_address=192.168.1.145/24  
    static routers=192.168.1.1  
    static domain_name_servers=999.999.999.999 8.8.8.8

Pour enregistrer les modifications au fichier dhcpcd.conf, appuyez sur Ctrl + X puis O (ou Y si votre OS est en anglais) pour enregistrer les modifications.

Redémarrez le Raspberry Pi.

## Utiliser une adresse IP différente selon le réseau actif

Prenons le cas où vous utilisez un Raspberry Pi dans votre établissement scolaire puis vous le ramenez chez vous pour poursuivre vos travaux.

Il pourrait arriver que l'adresse IP statique utilisée à l'école ne soit pas compatible avec les configurations de votre réseau à la maison.

Je vous propose deux techniques pour configurer une adresse IP statique qui ne sera utilisée que lorsque le réseau est disponible.

### Configuration selon le nom du réseau

Il est possible d'utiliser le nom du réseau sans fil pour préciser quelles configurations doivent être réalisées.

Si le Pi n'a accès à aucun des réseaux mentionnés, il obtiendra son adresse par DHCP.

Fichier dhcpcd.conf

interface wlan0  
  
# Configurations pour le réseau nommé ecole  
ssid ecole  
static ip_address=192.168.1.145/24  
static routers=192.168.1.1  
static domain_name_servers=999.999.999.999 8.8.8.8

 

# Configurations pour le réseau nommé maison  
ssid maison  
<a id="dhcpavant2023"></a>
static ip_address=10.0.0.28/24  
static routers=10.0.0.1  
static domain_name_servers=999.999.999.999 8.8.8.8

### Configuration selon l'adresse du routeur

L'astuce consiste à ajouter une configuration arping afin de fournir une adresse IP, généralement l'adresse du routeur, que le Pi tentera d'atteindre. S'il réussit, il exécutera les configurations de la section qui suit la configuration profile correspondante.

Dans le cas où aucune configuration arping ne réussit, l'adresse IP sera fournie par DHCP.

Fichier dhcpcd.conf

interface eth0  
arping 192.168.1.1  
arping 10.0.0.1  
  
# Configurations si l'adresse 192.168.1.1 a été rejointe par arping  
profile 192.168.1.1  
static ip_address=192.168.1.145/24  
static routers=192.168.1.1  
static domain_name_servers=999.999.999.999 8.8.8.8  
  
# Configurations si l'adresse 10.0.0.1 a été rejointe par arping  
profile 10.0.0.1  
static ip_address=10.0.0.28/24  
static routers=10.0.0.1  
static domain_name_servers=999.999.999.999 8.8.8.8

## Revenir à une adresse IP fournie par DHCP

Remarquez que pour revenir à une adresse IP fournie par le serveur DHCP, il suffit de remettre ces lignes en commentaire en ajoutant le symbole # au début de chaque ligne.

Lors du prochain redémarrage, il est fort probable que le Pi aura tout de même la même adresse IP puisque le serveur DHCP se rappellera de la dernière adresse fournie. Cependant, ceci n'est pas garanti alors sans l'adresse IP statique, vous devrez <a href="fiche-trouver_l_adresse_ip_du_raspberry_pi.md#trouver_l_adresse_ip_du_raspberry_pi">vérifier l'adresse IP</a> en branchant un écran sur le Pi.