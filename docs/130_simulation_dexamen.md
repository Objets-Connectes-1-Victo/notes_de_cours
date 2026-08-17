# 115. Simulation d'examen

## 115.1 Simulation d'examen final

Vous désirez ajouter une fonctionnalité à votre système Home Assistant : réagir à des nombres aléatoires générés à peu près à toutes les 30 secondes par un autre système (nommé système B) et publiés par MQTT sur le canal simulation3a4/nombre.

Vous aurez aussi à interagir avec un système nommé système C.

Vous n’avez pas accès à ces autres systèmes.

Votre prof vous fournira l’adresse de l’agent MQTT à utiliser ainsi que les autres informations requises.

Voici les opérations à réaliser.

* Tout d’abord, assurez-vous que votre Raspberry Pi est au bon fuseau horaire, à la bonne date et à la bonne heure. Vous devez effectuer ces manipulations à la ligne de commande. Faites une impression d’écran qui montre clairement la ou les commandes effectuées. Nommez ce fichier au format NomPrenom-Date.png.
* Configurez l’agent MQTT selon les coordonnées fournies par votre prof. Faites une impression d’écran qui montre clairement votre travail. Nommez ce fichier au format NomPrenom-AgentMQTT.png.
* À chaque fois qu’un nombre est reçu via MQTT, à condition qu’il soit différent du précédent, ajoutez automatiquement une entrée dans le fichier journal de Home Assistant, celui qu’on retrouve directement à partir du menu Activité dans la colonne de gauche. L’entrée doit avoir comme nom « Simulation » et le message doit être « Nombre reçu : » suivi du nombre. Faites une impression d’écran du journal qui montre au moins deux entrées qui indiquent le nombre reçu. Nommez ce fichier au format NomPrenom-Journal.png.
* Ajoutez un tableau de bord nommé simulation. Ajoutez-y :
  + la valeur du nombre aléatoire reçu par MQTT. La carte aura une icône qui montre des dés.
  + une carte géographique qui montre un device\_tracker nommé simulation.
  + une carte qui affiche clairement sa latitude et sa longitude.
  + une carte qui affiche l'état d'une lumière virtuelle nommée simulation\_lumiere.Vous ferez une impression d’écran de ceci plus tard.
* Lorsque le nombre généré est 1, vous devez déplacer le device\_tracker simulation aux coordonnées GPS du Cégep pendant 3 secondes puis le déplacer à l’intersection du boulevard Labbé et de la rue Notre-Dame Est. Ajoutez un bouton nommé « Simuler 1 » qui pourra lui aussi lancer l’automatisation.
* Lorsque le nombre généré est 2, vous devez publier sur un canal dont le nom est au format simulation3a4/ag (remplacez ag par vos initiales) les coordonnées GPS du device\_tracker simulation. Ajoutez un bouton nommé « Simuler 2 » qui pourra lui aussi faire ce travail.
* Lorsque le nombre généré est 3, vous devez lancer une automatisation qui allume la lumière virtuelle simulation\_lumiere mais seulement s’il fait noir dehors. Ajoutez un bouton nommé « Simuler 3 » qui pourra lui aussi faire ce travail.
* Vous devez récupérer l'information tirée du système C à partir de l'URL fourni par votre prof. Ajoutez une carte au tableau de bord pour afficher cette valeur.
* En prévision de l’examen au prochain cours, créez copie de sécurité de votre Home Assistant. Assurez-vous que votre seconde carte micro SD contienne un Home Assistant initialisé avec cette copie.

## Remises

Vous n’aurez rien à remettre puisque c’est une simulation, mais voici ce qui pourrait être demandé en examen :

* Les impressions d’écran identifiées à chacun des numéros concernés.
* Une impression d’écran du tableau de bord.
* Le fichier qui contient le code YAML du tableau de bord de la simulation d'examen. Son nom exact dépend de votre version de Home Assistant. Ce sera quelque chose du genre /mnt/data/supervisor/homeassistant/.storage/lovelace.simulation ou /mnt/data/supervisor/homeassistant/.storage/lovelace.dashboard\_simulation. À vous d'ouvrir le fichier et de vérifier qu'il contient bien tout le code du tableau que vous venez de créer. Vous devez le télécharger sur votre ordinateur. Renommez-le pour que son nom débute par votre nom de famille suivi de votre prénom.
* Les fichiers configuration.yaml, scripts.yaml et automations.yaml que vous aurez téléchargés sur votre ordinateur (certains pourraient être vides). Assurez-vous qu’on y voit les ajouts que vous avez fait pendant l’examen. Renommez-les pour que leur nom débute par votre nom de famille suivi de votre prénom.
* Le fichier /mnt/data/supervisor/homeassistant/.storage/core.entity\_registry qui contient toutes les entités.
* Notez que lors d’une évaluation sommative, l’élève est responsable de ses remises. Un fichier non remis ou illisible ou encore la remise d’un mauvais fichier ne permettra pas d’obtenir les points associés.