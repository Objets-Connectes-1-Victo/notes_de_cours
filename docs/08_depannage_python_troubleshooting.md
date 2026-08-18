# 7. Dépannage Python (troubleshooting) {#chapitre-depannage_python_troubleshooting_002}

## 7.1 Erreur « SyntaxError: invalid character in identifier » {#fiche-erreur_syntaxerror_invalid_character_in_identifier}

### Problème :

Lorsque vous lancez un programme Python sur le Raspberry Pi, vous obtenez le message « SyntaxError: invalid character in identifier »

### Contexte :

* Python 3
* Raspberry Pi

### Cause possible :

Vous avez copié du code à partir d'Internet et ceci a ajouté des caractères blancs différents des espaces requis pour indenter le code.

En effet, sur le Web, lorsque le code présente deux espaces d'affilée, le second doit être encodé avec &nbsp;.

### Solution proposée :

D'abord, configurez votre éditeur pour qu'il affiche un point lorsqu'il y a un espace.

Si vous utilisez Geany : Éditer / Préférences / Éditeur / Affichage / Afficher les espaces.

Si vous ne voyez pas les 4 points qui représentent les 4 espaces d'indentation, effacez le blanc et refaites des espaces.

## 7.2 Erreur « ValueError: Channel must be an integer or list/tuple of integers » {#fiche-erreur_valueerror_channel_must_be_an_integer_or_list_tuple_of_integers}

### Problème :

Lorsque vous lancez un script Python qui doit interagir avec le GPIO du Raspberry Pi, vous obtenez le message « ValueError: Channel must be an integer or list/tuple of integers ».

### Contexte :

* RPi.GPIO-0.7.0

### Cause possible :

Vous tentez d'envoyer ou de recevoir un signal à un port du GPIO mais vous utiliez une valeur non numérique pour spécifier son numéro.

Ceci peut arriver, par exemple, si vous utilisez un paramètre en ligne de commande pour spécifier le numéro du port.

Python


```python
port = sys.argv[1]
GPIO.output(port, 1)
```


Solution proposée :

Une valeur reçue par un paramètre à la ligne de commande est toujours considéré comme une chaîne de caractères.

Il faut la convertir en entier pour pouvoir l'utiliser ici.

Python


```python
port = int(sys.argv[1])
GPIO.output(port, 1)
```
