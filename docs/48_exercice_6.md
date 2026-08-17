# 43. Exercice 6 {#chapitre-exercice_6_007}

## 43.1 Historique {#fiche-historique}

1. Faites afficher un graphique de l'historique des données pour une commande d'un capteur de votre choix. Prenez une impression d'écran du graphique en vous assurant qu'on voit bien le nom de la commande. Nommez ce fichier au format NomPrenom-Historique.png.
2. Dans la base de données Jeedom, retrouvez la table dans laquelle vos équipements (vos objets connectés) sont stockés. On veut la table dans laquelle le nom de l'équipement apparaît, soit celui que vous voyez sur les tuiles dans le Dashboard.
3. Puisque cette table contient de nombreux enregistrements, effectuez une requête SQL pour afficher l'enregistrement qui correspond à un de vos équipements en utilisant le nom que vous lui avez donné (... WHERE name ...). Prenez cette requête en note dans un fichier texte que vous nommerez au format NomPrenom-Reponses.txt.
4. Chaque équipement contient de nombreuses commandes. Retrouvez la table dans laquelle les commandes sont stockées.
5. Dans cette table, effectuez une requête SQL pour retrouver tous les enregistrements qui correspondent aux commandes de l'équipement ciblé plus haut. Prenez cette requête en note dans votre fichier texte.
6. Les données captées par les commandes des équipements sont stockées dans la table history. Effectuez une requête SQL qui affiche la date, la valeur, l'identifiant et le nom de la commande ainsi que l'identifiant et le nom de l'équipement. Prenez cette requête en note dans votre fichier texte.

   Ex :

   Résultat à l'écran

   | 2021-09-24 07:05:00 | 122.605 | 113 | Voltage 16     | 15 | Prise intelligente Zooz |  
   | 2021-09-24 07:05:00 | 2       | 191 | Burglar 10     | 28 | Neo détecteur 5 en 1    |  
   | 2021-09-24 07:05:00 | 0       | 192 | SourceNodeId 2 | 28 | Neo détecteur 5 en 1    |  
   | 2021-09-24 07:05:00 | 0.012   | 110 | Energy 0       | 15 | Prise intelligente Zooz |  
   | 2021-09-24 07:05:00 | 0       | 189 | Alarm Level 1  | 28 | Neo détecteur 5 en 1    |  
   | 2021-09-24 07:05:00 | 0       | 114 | Current 20     | 15 | Prise intelligente Zooz |  
   | 2021-09-24 07:05:00 | 0       | 188 | Alarm Type 0   | 28 | Neo détecteur 5 en 1    |  
   | 2021-09-24 07:05:00 | 0       | 112 | Power 8        | 15 | Prise intelligente Zooz |  
   | 2021-09-24 07:05:00 | 245.5   | 183 | Luminance 3    | 28 | Neo détecteur 5 en 1    |  
   | 2021-09-24 07:10:00 | 0.012   | 110 | Energy 0       | 15 | Prise intelligente Zooz |  
   | 2021-09-24 07:10:00 | 0       | 112 | Power 8        | 15 | Prise intelligente Zooz |
7. Raffinez cette requête afin qu'elle affiche les unes à la suite des autres les informations de l'équipement tirées de la table history ET les informations tirées de la table historyArch, le tout en ordre de date. Notez que puisque votre système domotique est rarement branché de soir, il se peut que votre table d'archive soit pratiquement vide. Prenez cette requête en note dans votre fichier texte.
8. Copiez le résultat de la requête au bas du fichier texte. Notez que si vous travaillez en ligne de commande MySQL, pour pouvoir copier du texte en provenance du Pi vers votre ordinateur, vous devez travailler en SSH.
9. Créez un nouveau scénario qui <a href="fiche-scenario\_qui\_execute\_une\_requete\_sql.md#scenario\_qui\_execute\_une\_requete\_sql">effectue une requête SQL</a> pour retrouver la plus haute température enregistrée hier et qui <a href="fiche-scenario\_qui\_affiche\_une\_information\_dans\_le\_tableau\_de\_bord.md#scenario\_qui\_affiche\_une\_information\_dans\_le\_tableau\_de\_bord">affiche cette information dans le tableau de bord</a>.

   Ce scénario sera lancé à tous les jours 10 minutes après la tâche d'archivage. Vous devrez retrouver dans la table cron l'heure programmée pour la tâche history archive et entrer cette valeur plus 10 minutes dans le déclencheur du scénario.

   Afin de vous laisser vous concentrer sur le bloc de code PHP plutôt que sur la requête SQL, je vous fournis la requête à utiliser. Vous devrez évidemment ajuster le nom de votre équipement.

   SELECT MAX(historyArch.value) AS max FROM historyArch   
   INNER JOIN cmd ON cmd\_id = cmd.id   
   INNER JOIN eqLogic ON eqLogic\_id = eqLogic.id   
   WHERE eqLogic.name = 'Capteur 5-en-1 Neo'   
   AND cmd.name = 'Température'   
   AND DATE(historyArch.datetime) = CURDATE() - INTERVAL 1 DAY
10. Copiez le code du bloc PHP au bas du fichier texte.
11. Soit la base de données Jeedom dont le script SQL est donné dans ce fichier : [BaseDeDonneesJeedom.txt](https://apical.xyz/medias/fr/ContenuFormation/BaseDeDonneesJeedom.txt). Installez cette base de données sur votre poste de travail puis ouvrez-la dans l'éditeur de bases de données de votre choix (ex : phpMyAdmin, MySQL Workbench).
12. Dans la base de données qui vous a été fournie, indiquez de quelle date à quelle date les données ont été comptabilisées. Vous n'avez pas à fournir les requêtes SQL requises. Inscrivez seulement la réponse au bas du fichier.
13. Toujours dans la base de données Jeedom qui vous a été fournie, trouvez la plus haute température enregistrée par un capteur. Vous n'avez pas à fournir les requêtes SQL requises. Inscrivez seulement la réponse au bas du fichier.
14. Remettez votre fichier texte et votre impression d'écran sur la plateforme électronique du cours.
15. En prévision de l'exercice qui aura lieu après le formatif formel, prévoyez emmener votre matériel électronique : planche de maquettage, DEL, résistances, câbles DuPont.