<a id="fiche-explorer_la_base_de_donnees_et_les_statistiques_de_home_assistant"></a>
# 95. Exercice 17 - OPTIONNEL

## 95.1 Explorer la base de données et les statistiques de Home Assistant

## Première partie

1. Installez le module complémentaire SQLite Web.
2. Explorez les différentes tables de la base de données de Home Assistant. Listez deux tables qui sont liées entre elles et fournissez le nom de la clé primiare d'une table qui correspond à la clé étrangère dans l'autre table.
3. <a href="fiche-contenu_de_la_base_de_donnees_de_home_assistant.md#contenu_de_la_base_de_donnees_de_home_assistant">Copiez la base de données de Home Assistant vers votre ordinateur</a>. Faites une impression d'écran qui montre clairement ce fichier sur votre ordinateur. On doit également voir sa date et sa taille. Nommez ce fichier au format NomPrenom-scp.png.
4. Modifiez les configurations pour que les données soient conservées dans la table states pendant 14 jours. Les données doivent être enregistrées au fur et à mesure, plusieurs fois par secondes si requis. Faites une impression d'écran des configurations que vous avez ajoutées pour y parvenir. Nommez le fichier au format NomPrenom-config.png.
<a id="chapitre-exercice_18_005"></a>

## Deuxième partie

Pour cette partie, vous devez travailler à la ligne de commande SQLite. Vous pouvez utiliser à votre choix la fenêtre HassOS ou le Terminal de votre poste de travail.

Notez les réponses aux questions suivantes dans un fichier texte.

Votre nom doit apparaître dans le haut du fichier.

Pour chaque réponse, on doit voir clairement le numéro de la question.

1. À la ligne de commande, faites afficher la date et l'heure actuelle du système à l'aide d'une requête SQLite (à vous de trouver comment!) puis vérifiez si cette heure correspond à l'heure UTC ou à l'heure réelle en comparant avec l'heure de votre poste de travail. Comme réponse, inscrivez la requête ainsi que « heure UTC » ou « heure locale ».
2. Entrez les commandes SQLite pour assurer que les données des requêtes SQL apparaîssent en colonnes et que le nom de chaque champ soit affiché.
3. Pour chacune des tables de la base de données, faites afficher les 10 derniers enregistrements ajoutés (l'identifiant fera foi de l'ordre d'enregistrement).
4. Pour chaque entité du système, on retrouve <a href="fiche-qu_est-ce_qu_une_entite.md#qu_est-ce_qu_une_entite">un identifiant</a> en toutes lettres, par exemple sensor.neo_capteur_5_en_1_illuminance.

   Pour connaître cet identifiant, rendez-vous dans l'onglet Aperçu, cliquez sur l'entité désirée puis sur l'onglet Paramètres. L'identifiant est affiché dans la case ID d'entité.

   Dans quel(s) champ(s) de quelle(s) table(s) retrouve-t-on cet identifiant?
5. Effectuez une requête SQL pour lister seulement les identifiants d'entités. Chaque identifiant ne doit apparaître qu'une seule fois.
6. Effectuez une requête SQL pour sortir toutes les valeurs enregistrées pour une entité de votre choix (par exemple, l'ouverture et la fermeture d'une porte ou la luminosité saisie par un capteur). Ne faites afficher que les champs intéressants afin que le résultat ne prenne pas trop de place en largeur à l'écran.
7. Si vous regardez le contenu de la table statistics, vous ne voyez pas l'identifiant en format texte de l'entité à laquelle chaque statistique appartient. Effectuez une requête SQL pour voir cet identifiant avec chacune des statistiques.
8. Écrivez une requête qui :
   * Si vous travaillez avec un capteur binaire, écrivez une requête qui affiche le nombre de fois où sa valeur était on (ou 1) dans la table states.
   * Si vous travaillez avec un capteur numérique, écrivez une requête qui affiche sa valeur moyenne dans la table states.