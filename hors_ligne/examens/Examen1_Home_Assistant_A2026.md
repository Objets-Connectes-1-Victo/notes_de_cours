# OBJETS CONNECTÉS 1 – Examen 1

Nom : _________________________________________________________________

- Cet examen pratique compte pour 25% de la note finale.
- La grille de correction est fournie séparément.
- Vous disposez de deux (2) périodes consécutives de 50 minutes pour effectuer le travail demandé.
- Dans tout le code que vous écrirez, vous devez respecter les techniques, les pratiques et les normes enseignées. Plusieurs sont implicites, par exemple respecter la nomenclature.
- Vous devez réaliser seul les étapes demandées.
- Vous avez droit à toutes vos notes, exercices et à la consultation de documents sur Internet, incluant recherches via *udm14.org*
- Vous n’avez pas droit aux outils de communication ni à l'IA.
- La surveillance d'écran via Exam.net est obligatoire - le lien à suivre est fourni via Teams. Déconnectez-vous seulement après avoir remis votre travail sur Teams.
-    Ne fermez pas l'onglet du navigateur contenant la surveillance d'écran. Faire `Alt-Tab` pour passer aux autres applications sur votre portable.

## Énoncé

Vous désirez ajouter une fonctionnalité à votre système Home Assistant : veiller à ce que votre colocataire Olaf (le bonhomme de neige) ne fonde pas en sortant de la maison.

## Instructions

La liste des remises est présentée plus bas. Veuillez prévoir suffisamment de temps avant la fin de l'examen pour effectuer les impressions d'écran ainsi que la copie des fichiers demandés.  Truc: vous pouvez faire les captures d'écran au fur et à mesure que vous configurez les éléments demandés.

- Créez une personne appelée **olaf_examen**, elle doit être identifié par l’image à l’adresse suivante : [https://static.wikia.nocookie.net/disney/images/5/53/Profile_-\_Olaf.jpeg](https://static.wikia.nocookie.net/disney/images/5/53/Profile_-_Olaf.jpeg) (les URL des images sont disponibles dans le devoir Teams pour l’examen)
- Créez des capteurs virtuels avec les identifiants suivants :
    - **position_olaf_examen** (device_tracker - suivi de personne). Doit être basé sur un modèle (*template*) et associé à la personne *olaf_examen*.
    - **temperature_exterieure_examen** (température entre -50 et 50 Celsius)
    - **texte_examen** (permettra de saisir du texte)
- Ajoutez une zone « **Chambre froide** » aux coordonnées géographiques de votre choix qui permettra de savoir si Olaf est réfugié dans une chambre froide. La zone doit utiliser l’icône _snowflake_. Votre zone **Maison** établie à l’installation de Home Assistant sera aussi utilisée.
- Créez un tableau de bord nommé « **Olaf** ». Vous devez fournir des titres et des icônes appropriés aux éléments du tableau.

Le tableau de bord doit afficher :

- La position d’Olaf (sa zone courante – l’affichage de base des _device_tracker_)
- La température extérieure en Celsius
- Le texte virtuel
- Un bouton pour déplacer Olaf à la maison
- Un bouton pour déplacer Olaf dans la chambre froide
- Un bouton pour déplacer Olaf en dehors des zones connues
- Une carte qui montre les zones Maison et Chambre Froide de même que la position d’Olaf
- Dans le même tableau de bord, ajoutez une carte de type Markdown qui affichera les images suivantes selon la position d’Olaf :
    - Maison : [https://static.wikia.nocookie.net/gtawiki/images/8/84/ClintonResidence-GTAVe.png](https://static.wikia.nocookie.net/gtawiki/images/8/84/ClintonResidence-GTAVe.png)
    - Chambre froide : [https://static.wikia.nocookie.net/gtawiki/images/b/b4/AGLRefrigeratedStorageInc-GTAV.png](https://static.wikia.nocookie.net/gtawiki/images/b/b4/AGLRefrigeratedStorageInc-GTAV.png)
    - Ailleurs : [https://static.wikia.nocookie.net/fictional-cities/images/2/24/Dowtown.png](https://static.wikia.nocookie.net/fictional-cities/images/2/24/Dowtown.png)
- Créez une ou plusieurs automatisations dont le nom débute par « Suivi Olaf » qui est (ou sont) lancée(s) automatiquement lorsqu’Olaf se déplace. Le comportement attendu est le suivant :
    - Si Olaf entre à la maison et qu’il est plus que 22h :
        - Écrire ce message dans le fichier journal : « Olaf est rentré tard à la maison! ».
        - Écrire ce message dans le virtuel texte_examen : « Maison tard le soir ».
    - Si Olaf entre dans la chambre froide et qu’il fait au-dessus de 5 degrés :
        - Écrire ce message dans le virtuel texte_examen : « En sûreté dans la chambre froide : » suivi de la température extérieure.
    - Lorsque Olaf entre à la maison avant 22h ou s’il entre dans la chambre froide lorsqu’il fait 5 degrés ou moins à l’extérieur, ou s’il se déplace à un endroit inconnu :
        - Le texte virtuel texte_examen sera à blanc (entrez simplement un espace).
        - ATTENTION : les automatisations peuvent tomber en conflit quand on déménage directement Olaf de la maison à la chambre froide et vice-versa – faites vos tests en faisant passer Olaf en dehors des zones connues.

Remises :

- Impressions d’écrans
    - Montrer la liste des personnes de votre Home Assistant avec les images associées. Nommez l’image **_NomPrenom_\-Olaf-personne.png**.
    - Configuration réalisée pour créer le capteur virtuel pour la température extérieure. On doit voir son ID d’entité, sa valeur minimale et sa valeur maximale. Nommez le fichier **_NomPrenom_‑Temperature.png**.
    - Configuration réalisée pour créer le texte virtuel. On doit voir son ID d’entité. Nommez le fichier **_NomPrenom_‑Texte.png**.
    - Zones configurées. On doit y voir clairement une carte de la ville avec la zone définie, son nom et son icône. Nommez le fichier **_NomPrenom_‑NomZone.png**.
    - Carte (tuile) Markdown. On doit y voir clairement le code qui détermine quelle image doit être affichée. Nommez le fichier **_NomPrenom_\-Markdown.png**.
    - Tableau de bord. On doit y voir clairement chaque élément affiché ainsi que le nom du tableau de bord. Assurez-vous que la photo d’Olaf de même que les zones Maison et Chambre froide soient bien visibles sur la carte. Au besoin, déplacez Olaf ailleurs et jouez avec le zoom. Nommez le fichier **_NomPrenom_‑TableauDeBord.png**.
- Copiez le code YAML du tableau de bord dans un fichier texte. Nommez le fichier **_NomPrenom_‑Lovelace.txt** (peut être obtenu de *Modifier le tableau de bord -> ⋮ -> Éditeur de configuration brute*).
- Téléchargez vos fichiers **configuration.yaml**, **automatisations.yaml**, **scripts.yaml**, et **known_devices.yaml**, (certains pourraient être vides ou ne pas avoir été modifiés pendant l’examen) sur votre ordinateur. **Assurez-vous qu’on y voit les ajouts que vous avez faits pendant l’examen, c’est parfois la seule façon de montrer ce que vous avez configuré**. Renommez les fichiers pour que leur nom débute par votre nom de famille suivi de votre prénom.
- Une fois votre travail terminé, remettez sur Teams un .zip qui contient toutes les remises demandées. Nommer le fichier **_NomPrenom_\-Examen1.zip**. **Un fichier non remis donnera 0 pour toutes les vérifications qui ne pourront pas être faites.**
- Terminer votre examen exam.net (*Soumettre*)
- Remettez cette feuille d’examen à votre professeur après y avoir écrit votre nom.