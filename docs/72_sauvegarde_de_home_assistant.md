<a id="fiche-sauvegarde_de_home_assistant"></a>
# 64. Sauvegarde de Home Assistant
<a id="telecharger"></a>

## 64.1 Sauvegarde de Home Assistant

Une sauvegarde Home Assistant permet de remettre le système dans l'état où il était lorsque la sauvegarde a été réalisée.

Cette fonctionnalité portait auparavant le nom snapshot. Ces mots réfèrent donc à la même chose.

Pour créer une sauvegarde, rendez-vous dans le menu Paramètres / Système / Sauvegardes puis cliquez sur Sauvegarder maintenant au bas de l'écran.

Les sauvegardes Home Assistant sont protégées par une clé de chiffrement. Dans l'écran qui suit, cliquez sur Télécharger pour conserver une copie de cette clé. Placez le fichier dans un endroit sûr.

![Clé de chiffrement](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-Sauvegarde-CleDeChiffrement.png)

Le fichier de secours contiendra ceci :

Fichier home_assistant_backup_emergency_kit_jj_mm_aaaa_hh_mm.txt

Kit de secours pour Home Assistant

 

Ce kit de secours contient la clé de chiffrement de vos sauvegardes. Vous avez besoin de cette clé pour pouvoir restaurer les sauvegardes de votre Home Assistant.

 

Date : 8 octobre 2025 à 20:15

 

Instance :  
Maison

 

Adresse :  
http://192.168.1.145:8123

 

Clé de chiffrement :  
DDTV-CESF-QLHM-PM8S-AHHS-BF6M-5044

 

Pour plus d'informations, visitez le site https://www.home-assistant.io/more-info/backup-emergency-kit

Vous devez ensuite choisir entre l'option Sauvegarde automatique et Sauvegarde manuelle.

La sauvegarde automatique qui crée immédiatement une sauvegarde selon les configurations disponibles sur le premier écran de la page de sauvegarde.

La sauvegarde manuelle vous offre de modifier les configurations pour cette fois seulement.

Dans les deux cas, ceci créera un fichier de sauvegarde sur le Raspberry Pi dans le dossier /mnt/data/supervisor/backup.

La liste des sauvegardes existantes est disponible via le menu Paramètres / Système / Sauvegardes.

Elle peut également être affichée via <a href="fiche-la_console_home_assistant.md#la_console_home_assistant">le terminal HassOS</a> à l'aide de cette commande :

Terminal

ha backup list

## Placer la sauvegarde en lieu sûr

Pour vous assurer de pouvoir utiliser la sauvegarde en cas de panne de votre système, le fichier de sauvegarde ne doit pas demeurer uniquement sur le Raspberry Pi.

Il faut donc le copier sur votre ordinateur.

La technique la plus simple consiste à utiliser l'interface graphique. Dans le menuParamètres / Système / Sauvegardes, cliquez sur les trois points à droite dela sauvegarde désirée puis choisissez Télécharger la sauvegarde.

![Télécharger la sauvegarde](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-TelechargerLaSauvegarde.png)

Vous aurez alors une copie du fichier de sauvegarde sur votre ordinateur.

## Pour plus d'information

« Home Assistant OS Common Tasks - Home Assistant OS Snapshots ». Home Assistant. <https://www.home-assistant.io/hassio/haos_common_tasks/#home-assistant-os-snapshots>

« Home Assistant Starter: Backup and Restore ». SuburbanNeerd. <https://suburbannerd.com/hassiobackup/>

## 64.2 Réinstaller Home Assistant à partir d'une sauvegarde

Si vous prenez soin d'effectuer régulièrement <a href="fiche-sauvegarde_de_home_assistant.md#sauvegarde_de_home_assistant">une sauvegarde de Home Assistant</a>, vous pourrez remettre le système en place rapidement en cas de problème avec votre carte micro SD.

Dans le cas où Home Assistant est encore fonctionnel, vous pouvez procéder directement à l'[étape de restauration](https://apical.xyz/formations/pageunique/systeme_domotique_diy#restauration).

S'il ne fonctionne plus du tout, vous devrez d'abord effectuer une [réinstallation](https://apical.xyz/formations/pageunique/systeme_domotique_diy#reinstallation).

## Réinstallation

* Sur votre boîte Home Assistant actuelle, <a href="fiche-sauvegarde_de_home_assistant.md#sauvegarde_de_home_assistant">effectuez une sauvegarde complète</a>.
* <a href="fiche-sauvegarde_de_home_assistant.md#sauvegarde_de_home_assistant">Téléchargez la sauvegarde sur votre ordinateur</a>.
* Sur la carte micro SD qui contiendra une copie intégrale du système, <a href="fiche-installation_de_home_assistant_et_premier_acces.md#installation_de_home_assistant_et_premier_acces">effectuez une nouvelle installation de Home Assistant</a>.
* Une fois l'installation complétée, <a href="fiche-installation_de_home_assistant_et_premier_acces.md#installation_de_home_assistant_et_premier_acces">accédez à l'interface Web de Home Assistant</a>.
* Sur l'écran d'accueil, si Home Assistant réalise que le système n'a pas été initialisé, il vous offre soit de créer votre maison connectée, soit d'effectuer une restauration. Cliquez sur Restaurer depuis une sauvegarde.

  ![Restaurer depuis une sauvegarde](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-RestaurerDepuisUneSauvegarde.png)
* Poursuivez avec [les étapes communes pour la réinstallation et la restauration](https://apical.xyz/formations/pageunique/systeme_domotique_diy#commune).

## Restauration

* Alternativement, si le système avait déjà été initialisé, vous pouvez restaurer une sauvegarde à partir du menu Paramètres / Système / Sauvegardes / clic sur les trois points verticaux dans le coin supérieur droit de l'écran / Téléverser une sauvegarde.

  ![Téléverser une sauvegarde](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-TeleverserUneSauvegarde.png)
<a id="chapitre-exercice_11_005"></a>
* Poursuivez avec [les étapes communes pour la réinstallation et la restauration](https://apical.xyz/formations/pageunique/systeme_domotique_diy#commune).

## Étapes communes pour la réinstallation et la restauration

* Dans tous les cas, retrouvez le fichier de sauvegarde sur votre ordinateur. Il s'agit d'un fichier dont le nom se termine par .tar.

* Home Assistant vous offrira alors de restaurer la sauvegarde complète ou seulement une partie de celle-ci.

  ![Fichier de sauvegarde](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-RestaurerUneSauvegarde.png)
* Si vous ciiquez sur Sauvegarde partielle, Home Assistant vous demandera de choisir quelles parties vous désirez sauvegarder.

  ![Restaurer sauvegarde partielle](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-RestaurerSauvegardePartielle.png)
* Dans tous les cas, vous devrez confirmer avant de poursuivre puisque cette opération écrasera votre installation actuelle de Home Assistant.

  ![Confirmation](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-ConfirmationRestaurationSauvegarde.png)
* Après avoir cliqué sur Restore, vous devez patienter pendant que Home Assistant remet le tout en place. L'opération peut prendre jusqu'à 45 minutes [selon la documentation officielle](https://www.home-assistant.io/common-tasks/os/#estimated-duration).
* Pendant la restauration, il est possible de voir l'avancement des travaux <a href="fiche-la_console_home_assistant.md#la_console_home_assistant">dans une fenêtre Terminal</a> à l'aide de la commande ha supervisor logs.
* À la fin de l'opération, vous aurez votre Home Assistant tel qu'il était au moment où vous avez effectué cette sauvegarde.
* Pour vous assurer que tout soit bien réinitialisé, prenez soin de <a href="fiche-Eteindre_home_assistant_de_facon_securitaire.md#Eteindre_home_assistant_de_facon_securitaire">redémarrer le système</a>.

J'ai déjà vu un système qui plantait quand on tentait de téléverser une sauvegarde, probablement dû à un fichier corrompu.

Pas de problème, il est possible de téléverser la sauvegarde manuellement.

Terminal de l'ordinateur

scp -O -P 22222 chemin/vers/sauvegarde/sur/ordinateur/personnel root@192.168.1.145:/mnt/data/supervisor/backup/

Après un redémarrage de Home Assistant, la sauvegarde est visible dans Paramètres / Système / Sauvegardes. Vous pouvez cliquer sur cette sauvegarde pour accéder aux options de restauration.