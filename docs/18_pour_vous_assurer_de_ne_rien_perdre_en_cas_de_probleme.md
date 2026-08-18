# 16. Pour vous assurer de ne rien perdre en cas de problème {#chapitre-pour_vous_assurer_de_ne_rien_perdre_en_cas_de_probleme}

## 16.1 Copie de sécurité de Jeedom {#fiche-copie_de_securite_de_jeedom}

Tout bon système informatique doit pouvoir être sauvegardé afin de pouvoir tout remettre en place en cas de problème.

Jeedom a tout ce qu'il faut pour cela.

## Sauvegarde manuelle {#manuelle}

Le système de sauvegarde de Jeedom permet de créer un fichier compressé qui contiendra tout le contenu du dossier /var/www/html ainsi qu'un script SQL de la base de données.

Pour lancer une sauvegarde manuelle, rendez-vous dans le menu Réglages / Système / Sauvegardes puis cliquez sur Lancer une sauvegarde.

![Lancer une sauvegarde](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Jeedom-LancerUneSauvegarde.png)

La fenêtre Informations affichera le résultat de l'opération.

![Informations sur la sauvegarde](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Jeedom-Sauvegarde-Informations.png)

Le fichier de sauvegarde sera enregistré dans le dossier /var/www/html/backup sur le Raspberry Pi.

Pour vous assurer qu'il ne soit pas perdu si jamais la carte micro SD était corrompue, téléchargez-le sur votre poste de travail à l'aide du bouton Télécharger la sauvegarde.

## Contenu d'une sauvegarde

Si vous êtes curieux, vous pouvez examiner le contenu d'un fichier de sauvegarde.

Après avoir téléchargé le fichier sur votre poste de travail à l'aide du bouton Télécharger la sauvegarde dans Jeedom, décompressez-le.

Vous constaterez que la sauvegarde contient de nombreux fichiers qui permettent de réinitialiser toutes vos configurations.

En fait, c'est tout le contenu du dossier /var/www/html qui est présent.

Un script SQL de la base de données est également présent.

![Fichier de sauvegarde](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Jeedom-ContenuFichierSauvegarde.png)

## Sauvegardes automatiques

Par défaut, Jeedom fera une sauvegarde complète du système à chaque nuit.

L'heure de la sauvegarde est établie par Jeedom en fonction de la charge du Market puisqu'il y a possibilité de copier automatiquement le fichier de sauvegarde dans l'infomuagique.

Pour connaître l'heure exacte de la sauvegarde, rendez-vous dans Réglages / Système / Moteur de tâches. Recherchez une tâche dont la classe est Jeedom et la fonction est backup.

On voit ici que la sauvegarde sera lancée à chaque jour à 00h36 ([syntaxe cron](https://www.domo-blog.fr/editer-la-crontab-du-raspberry/) 36 00 \* \* \*).

![cron](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Jeedom-CronSauvegardeAutomatique.png)

Comme pour les sauvegardes manuelles, le fichier de sauvegarde sera enregistré dans le dossier /var/www/html/backup sur le Raspberry Pi.

Résultat à l'écran


```
pi@raspberrypi:~ $ ls /var/www/html/backup
backup-mon\_jeedom-4.1.25-2021-09-04-00h36.tar.gz
backup-mon\_jeedom-4.1.25-2021-09-05-00h36.tar.gz
backup-mon\_jeedom-4.1.25-2021-09-06-00h36.tar.gz
```


## Configurer les sauvegardes

Il est possible d'apporter des précisions sur la façon dont les sauvegardes seront effectuées.

* Rendez-vous dans le menu Réglages / Système / Sauvegardes.

  ![Sauvegardes](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Jeedom-Sauvegarde.png)
* De là, vous pouvez configurer les sauvegardes automatiques.
  + Il est possible de modifier le nom du dossier qui contiendra les sauvegardes par défaut : backup).
  + Le nombre de sauvegardes conservées sur le Pi dépend des configurations Rétention temporelle (jours) et Taille totale maximale (Mo).
  + Il est possible de copier automatiquement les sauvegardes dans l'infonuagique. Cette solution requiert cependant un paiement mensuel de 2 euros. Par contre, [je vous montre ici une technique pour télécharger les sauvegardes sans frais sur votre ordinateur](18_pour_vous_assurer_de_ne_rien_perdre_en_cas_de_probleme.md#fiche-copier_automatiquement_le_fichier_de_sauvegarde_sur_votre_ordinateur).

## Restaurer une sauvegarde {#restaurer}

Votre système Jeedom est défaillant ou encore vous désirez revenir à une configuration antérieure?

Pas de problème, la restauration est très simple si vous avez en main le fichier de sauvegarde.

* Si votre système est encore fonctionnel, vous pouvez travailler directement à partir de votre Jeedom. S'il est défaillant, vous devez installer une nouvelle copie de Jeedom.
* Si votre système était encore fonctionnel, le fichier de sauvegarde pourra être retrouvé directement par l'interface de Jeedom. Passez à l'étape suivante.

  Dans le cas où votre système était défaillant, vous devez, après avoir réinstallé Jeedom, copier le fichier vers le Raspberry Pi.

  Terminal de votre ordinateur

```
  scp /dossierlocal/backup-mon\_jeedom-4.1.25-2021-09-06-00h36.tar.gz pi@192.168.1.145:
```

  Une fois copié sur le Pi, il devra être déplacé dans le dossier /var/www/html/backup.

  Terminal du Raspberry Pi

```
  sudo mv backup-mon\_jeedom-4.1.25-2021-09-06-00h36.tar.gz /var/www/html/backup
```
* Dans Jeedom, rendez-vous dans le menu Réglages / Système / Sauvegardes.
* Dans la zone Sauvegardes locales, section Sauvegardes disponibles, sélectionnez la sauvegarde désirée dans la liste déroulante.
* Cliquez sur Restaurer la sauvegarde. Jeedom affichera l'état d'avancement dans la fenêtre Informations.

  ![Informations sur la restauration](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Jeedom-Sauvegarde-Restauration.png)

## 16.2 Copier automatiquement le fichier de sauvegarde sur votre ordinateur {#fiche-copier_automatiquement_le_fichier_de_sauvegarde_sur_votre_ordinateur}

![Facultatif](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/ico-Facultatif.gif "Facultatif")

Les sauvegardes locales directement sur le Raspberry Pi sont intéressantes mais elles pourraient n'être d'aucun secours si jamais la carte micro SD était défaillante.

C'est pourquoi il est important de copier le fichier de sauvegarde à un autre endroit.

Puisque la sauvegarde dans l'infonuagique via l'interface de Jeedom nécessite des frais mensuels, je vous propose de faire une copie manuelle des fichiers de sauvegarde vers votre ordinateur personnel.

Il y a bien sûr la possibilité d'automatiser le transfert du fichier via Samba, tel que décrit dans cet article : <https://jeedomiser.fr/article/automatiser-et-externaliser-vos-sauvegardes-jeedom/>.

Ce que je vous propose est encore plus simple : une copie vers votre ordinateur personnel, qui sera lancée automatiquement à chaque jour.

* Créez un petit fichier bash pour automatiser cette tâche.
  + Le nom du fichier de sauvegarde est toujours le même à l'exception de la date du jour. L'heure pourra aussi être différente mais si vous vous en tenez aux sauvegardes lancées automatiquement, elle sera toujours la même à une ou deux minutes près.

    Le fichier bash devra donc monter le nom du fichier de sauvegarde à partir de la date du jour. Vous pouvez vous inspirer du <a href="fiche-script_pour_faciliter_la_copie_de_securite.md#script_pour_faciliter_la_copie_de_securite">script pour faciliter la copie de sécurité dans le nuage</a>.

    Je vous conseille de vérifier la présence du fichier de sauvegarde sur le Raspberry Pi (sous Windows : if exist fichier.extension, sous Mac : if [ -e fichier.extension ]). En effet, si la sauvegarde n'a pas pu être effectuée exactement à la minute programmée, le nom du fichier sera légèrement différent (ex : backup-mon\_jeedom-4.1.25-2021-09-06-00h3**7**.tar.gz au lieu de backup-mon\_jeedom-4.1.25-2021-09-06-00h3**6**.tar.gz)
  + Le fichier bash se chargera de lancer [la commande scp pour copier un fichier du Pi vers votre ordinateur,versordi](53_scripts_python_pour_envoyer_et_recevoir_du_signal_sur_le_gpio.md#fiche-copier_un_fichier_sur_une_machine_linux_a_partir_d_un_autre_ordinateur).
  + Puisque la commande scp demande un mot de passe pour accéder au Pi, assurez-vous d'avoir [copié la clé publique SSH sur votre Pi](05_raspberry_pi.md#fiche-permettre_le_branchement_ssh_sans_demander_le_mot_de_passe_a_chaque_fois) afin que le mot de passe ne soit plus demandé.
* Une fois le fichier bash écrit et testé, configurez le système d'exploitation de votre ordinateur pour que le fichier soit lancé automatiquement à la fréquence que vous désirez.
  + Sous Windows :
    - Planificateur de tâches / Action / Créer une tâche de base.
    - Nommer la tâche (ex : copie Jeedom)
    - Déclencheur : tous les jours et préciser l'heure désirée
    - Action : Démarrer un programme
    - Programme/script : Start-process -FilePath "$env:ProgramFiles\Git\bin\bash.exe" -ArgumentList "-l", "-c", '"bash monScript.bash"' -WorkingDirectory "C:\chemin\du\script"

      Prenez soin de remplacer monScript.bash le nom de votre script ainsi que C:\chemin\du\script par le chemin du dosiser qui contient ce script.

      Pour plus d'info : <https://www.pcastuces.com/pratique/astuces/5515.htm>.
  + Sous Mac, j'ai écrit une fiche sur le sujet : <a href="fiche-lancer\_une\_tache\_de\_facon\_automatique\_crontab.md#lancer\_une\_tache\_de\_facon\_automatique\_crontab">lancer\_une\_tache\_de\_facon\_automatique\_crontab</a>.
* Évidemment, votre ordinateur personnel devra être ouvert et branché sur le même réseau que le Raspberry Pi pour que la copie fonctionne.

##