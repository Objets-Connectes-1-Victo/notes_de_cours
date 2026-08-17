# 85. Dépannage sur l'envoi de courriel (troubleshooting)

## 85.1 Erreur « Unable to find service notify »

### Problème :

Lorsque vous utilisez le menu Outils de développement / Services afin de tester votre configuration SMTP pour envoyer du courriel avec Home Assistant, vous obtenez le message « Échec d'appel du service "notify/courriel\_administrateur". Unable to find service notify/courriel\_administrateur ».

![Échec d'appel du service ](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-UnableToFindServiceNotify.png)

### Contexte :

* Home Assistant 0.118.4
* HassOS 4.16
* Raspberry Pi 3B

### Cause possible :

Vous n'avez pas redémarré le Raspberry Pi après avoir entré les configurations du service SMTP dans le fichier configuration.yaml.

### Solution proposée :

Redémarrez le Pi puis refaites le test d'envoi de courriel.

### Autre cause possible :

Il y a une erreur dans les configurations du service SMTP.

### Solution proposée :

Assurez-vous que les configurations utilisent les bonnes données. Par exemple, l'encryption pour la plupart des serveurs SMTP doit être starttls (notez la présence des deux t : START Transport Layer Security).

N'oubliez pas de redémarrer le Raspberry Pi après avoir modifié les configurations.

### Autre cause possible :

L'adresse de courriel que vous tentez d'utiliser ne permet pas l'envoi de courriel à partir d'une application.

Ceci est parfois le cas avec les adresses de fournisseurs génériques, par exemple gmail.

### Solution proposée :

Créez-vous une adresse de courriel avec un nom de domaine qui vous appartient (voir <).