# Examen formatif : tableau de bord de Noël

## Consignes

Vous désirez ajouter une fonctionnalité à votre système Home Assistant : créer un tableau de bord en vue de Noël qui approche.

La grille de correction vous a déjà été fournie sur Apical. Réalisez les opérations suivantes en utilisant seulement les notions vues au cours des trois premières semaines.

Prévoyez suffisamment de temps, soit au moins 5 minutes avant la fin de l'examen, pour faire les impressions d'écran et copier les fichiers demandés.

## Capteurs virtuels

Créez les capteurs virtuels suivants. Ce sont les seuls capteurs virtuels que vous pouvez utiliser pendant l'examen.

- `pere_noel_dans_ma_maison`
  - Identifiez-le avec l'image `examen.png` qui vous a été fournie.
  - Il représente la position du Père Noël. Ses changements d'état déclenchent les automatisations.
- `je_suis_a_la_maison`
  - Aucune image n'est nécessaire.
  - Il représente votre propre position. Il sert à vérifier si vous êtes à la maison lorsque le Père Noël y arrive.
- `texte_examen`
  - Il doit permettre de saisir du texte.
- `date_examen`
  - Il doit permettre de saisir une date, sans l'heure.

## Tableau de bord

Créez un tableau de bord nommé **Noël**. Il doit afficher les éléments suivants :

- `pere_noel_dans_ma_maison`, qui doit afficher son état;
- `je_suis_a_la_maison`, qui doit afficher son état;
- le texte virtuel;
- la date virtuelle;
- un bouton pour déplacer le Père Noël à la maison;
- un bouton pour déplacer le Père Noël à un endroit inconnu;
- une carte Markdown qui affiche `Vrai` si le Père Noël n'est pas à la maison et si la date virtuelle est le 24 décembre 2025. Elle doit afficher `Faux` dans tous les autres cas.

## Automatisations

Créez une ou plusieurs automatisations dont le nom commence par **Examen**. Cette ou ces automatisations doivent être déclenchées automatiquement lorsque `pere_noel_dans_ma_maison` change d'état.

Le comportement attendu est le suivant.

### Père Noël en route

Si `pere_noel_dans_ma_maison` n'est pas à la maison et que la date virtuelle est le 24 décembre, écrivez le message suivant dans le capteur virtuel `texte_examen` :

`Le Père Noël est en route!`

### Père Noël à la maison

Si `pere_noel_dans_ma_maison` entre à la maison et que `je_suis_a_la_maison` est également à la maison, écrivez le message suivant dans le capteur virtuel `texte_examen` :

`Le Père Noël arrive, réveille-toi!`

## Remises

### Fichiers de configuration

Téléchargez sur votre ordinateur les fichiers suivants. Certains fichiers peuvent être vides ou ne pas avoir été modifiés pendant l'examen.

- `configuration.yaml`
- `automations.yaml`
- `scripts.yaml`
- `customize.yaml`
- `known_devices.yaml`

### Impression du tableau de bord

Faites une impression d'écran du tableau de bord. Chaque élément affiché doit être clairement visible. Les deux positions virtuelles doivent également être bien visibles.

Au besoin, déplacez les virtuels. Nommez le fichier :

`NomPrenom-TableauDeBord.png`

### Code YAML du tableau de bord

Copiez le code YAML du tableau de bord dans un fichier texte. Nommez le fichier :

`NomPrenom-Lovelace.txt`
