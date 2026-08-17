# 47. Scripts Python pour envoyer et recevoir du signal sur le GPIO

## 47.1 Langages et bibliothèques pour communiquer avec le GPIO

Il est possible de communiquer avec le [apical\_lien\_interne][qu\_est-ce\_que\_le\_gpio,GPIO][/apical\_lien\_interne] à l'aide de différents langages de programmation, par exemple en C, Python ou même PHP.

Plusieurs bibliothèques permettent d'y arriver. En voici quelques-unes :

* RPi.GPIO : <https://sourceforge.net/p/raspberry-gpio-python/wiki/Examples/> (Python)
* gpiozero : <https://gpiozero.readthedocs.io/en/stable/> (Python)
* pigpio : <http://abyz.me.uk/rpi/pigpio/python.html> (Python)
* Wiring Pi : <http://wiringpi.com/reference/> (peut être utilisé avec plusieurs langages)

La bibliothèque RPi.GPIO sera utilisée dans [apical\_lien\_interne][installation\_de\_la\_bibliotheque\_rpi\_gpio,les fiches qui suivent][/apical\_lien\_interne] pour démontrer comment programmer un script qui interagit avec le GPIO du Raspberry Pi.

## 47.2 Installation de la bibliothèque RPi.GPIO

La bibliothèque [RPi.GPIO](https://pypi.org/project/RPi.GPIO/) est très utilisée pour envoyer et recevoir du signal sur le GPIO du Raspberry Pi.

## Installation de la bibliothèque RPi.GPIO

Cette bibliothèque est installée par défaut sur Raspberry Pi OS.

Pour vérifier quelle version est installée, lancez cette commande sur le Pi, lancez la console Python.

Terminal du Raspberry Pi

python3

Pour charger la bibliothèque et vérifier sa version :

Console Python

import RPi.GPIO as GPIO   
GPIO.VERSION

Et pour refermer la console Python :

Console Python

quit()

Vous obtiendrez ceci :

Résultat à l'écran

pi@raspberrypi:~ $ python3  
Python 3.11.2 (main, Apr 28 2025, 14:11:48) [GCC 12.2.0] on linux  
Type "help", "copyright", "credits" or "license" for more information.  
>>> import RPi.GPIO as GPIO  
>>> GPIO.VERSION  
'0.7.2'  
>>> quit()

## Installer la dernière version de RPi.GPIO

Si vous êtes aux prises avec une vieille version que vous devez mettre à jour, lancez cette commande. Mais attention : ceci peut prendre de longue, longues minutes.

Ne le faites que si la version actuelle pose problème.

Terminal du Raspberry Pi

sudo apt update && sudo apt install python-rpi.gpio python3-rpi.gpio

## 47.3 La base des scripts avec RPi.GPIO

Le script Python qui sera en charge d'envoyer ou de recevoir un signal des [apical\_lien\_interne][qu\_est-ce\_que\_le\_gpio,broches GPIO][/apical\_lien\_interne] du Raspberry Pi peut être écrit :

* directement sur le Pi à l'aide d'un éditeur comme nano.
* sur l'ordinateur à l'aide de l'éditeur de votre choix, par exemple Geany ou PyCharm.

La bibliothèque [apical\_lien\_interne][installation\_de\_la\_bibliotheque\_rpi\_gpio,RPi.GPIO][/apical\_lien\_interne] sera utilisée dans cette démonstration. Elle est installée par défaut sur Raspberry Pi OS.

Notez que si vous utilisez un éditeur comme PyCharm sur votre ordinateur, il vous donnera des erreurs si votre code utilise des bibliothèques qui sont sur le Pi mais pas sur votre ordinateur. Vous pourrez ignorer ces erreurs.

Le script doit être placé directement sur le Raspberry Pi pour être exécuté. Si vous l'avez écrit sur votre ordinateur, vous devrez [apical\_lien\_interne][copier\_un\_fichier\_sur\_une\_machine\_linux\_a\_partir\_d\_un\_autre\_ordinateur,le copier sur le Pi][/apical\_lien\_interne] ![Conseil](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/Ampoule.svg "scp dossierlocal/monfichier.extension pi@192.168.1.145:/dossier/sous-dossier") après l'avoir édité.

## Nom du fichier

Par convention, les scripts Python seront inscrits dans un fichier texte dont le nom se termine par .py.

Le nom du fichier peut :

* être tout en minuscules (ex : monscript.py)

  ou
* utiliser la casse serpent (ex : mon\_script.py)

## Entête du script Python

Lançons-nous dans la programmation!

Tout programme Python doit débuter par une ligne, qu'on appellera shebang ou hash bang.

Le [apical\_lien\_interne][Shebang\_ou\_hash\_bang,shebang][/apical\_lien\_interne] permet de spécifier quel interpréteur doit être utilisé.

Python

#!/usr/bin/env python3

Vient ensuite une ligne qui indique l'encodage du fichier. Cette ligne était nécessaire en Python 2 mais elle est optionnelle en Python 3 puisque l'encodage par défaut est UTF-8.

Python

# -\*- coding:utf-8 -\*-

Tout programme qui se respecte doit contenir un en-tête standard. Cet en-tête indique notamment le but du script, les paramètres attendus, le montage physique requis, la date de création et l'auteur.

En Python, les commentaires de documentation utilisent la syntaxe [DocString](https://www.python.org/dev/peps/pep-0257/) et sont placés entre triples guillemets.

Python

"""  
Fait clignoter une DEL rouge sur le Raspberry Pi  
Paramètres : aucun  
Montage : DEL rouge branchée sur GPIO.BCM 23 et résistance de 330 Ohms  
Auteur : Christiane Lagacé  
Date : 17 septembre 2025  
"""

Vient ensuite le chargement des bibliothèques, ici RPi.GPIO.

Python

import RPi.GPIO as GPIO

## Choisir le type d'adressage

Les broches du GPIO peuvent être référées par leur adresse physique (position de la broche sur le Pi, numérotée de 1 à 40) ou par leur adresse broadcom (numéros de ports).

L'adresse BCM est généralement utilisée. Il faut l'indiquer au script comme suit :

Python

GPIO.setmode(GPIO.BCM)

## Variables pour les numéros de ports

Le script sera plus facile à lire si vous utilisez des variables pour reternir les numéros des ports que vous utilisez.

Attention : del est un mot réservé en Python. Nous allons utiliser led comme nom de variable.

Python

led = 23

 

bouton = 25

## Déterminer le sens du signal

Pour chaque port que vous souhaitez utiliser dans le script, il faut indiquer si le signal sera en entrée ou en sortie.

### GPIO.OUT : le Pi peut envoyer un signal au port

Par exemple, pour que le Pi envoie un signal au port 23 afin d'allumer une DEL :

Python

GPIO.setup(led, GPIO.OUT)

Il est possible de changer l'état (d'envoyer un signal) dans une instruction indépendante (voir plus bas) ou encore de le faire dans la même instruction :

Python

GPIO.setup(led, GPIO.OUT, initial=0)

Attention : si vous faites GPIO.setup(led, GPIO.OUT) sans préciser l'état initial, votre script devra par la suite se charger d'envoyer un signal au port pour allumer ou éteindre la DEL.

Si vous ne le faites pas, le port demeurera dans un état flottant. La DEL pourrait donc s'allumer même si vous ne lui avez envoyé aucun signal.

### GPIO.IN : le Pi peut recevoir un signal du port

Si le programme devait lire la valeur envoyée par un composant branché sur le port 12, par exemple un bouton poussoir :

Python

GPIO.setup(bouton, GPIO.IN)

Et pour éviter un état flottant :

Python

GPIO.setup(bouton, GPIO.IN, pull\_up\_down=GPIO.PUD\_DOWN)

## Envoi d'un signal

Pour les ports qui reçoivent un signal du Pi (GPIO.OUT), le Pi peut envoyer un signal à l'aide de trois systèmes qui sont équivalents :

* GPIO.HIGH, GPIO.LOW
* True, False
* 1, 0

Pour allumer la DEL, on envoie un signal positif :

Python

GPIO.output(led, 1)

Pour l'éteindre, on envoie un signal non positif :

Python

GPIO.output(led, 0)

Pour savoir par programmation dans quel état est le port :

Python

etat = GPIO.input(led)

## Réception d'un signal

Pour les ports qui envoient un signal au pi (GPIO.IN), le Pi peut lire la valeur envoyée :

Python

valeur = GPIO.input(bouton)

### Événements

Pour détecter quand un port reçoit un signal, par exemple quand un bouton est pressé, deux choix s'offrent à nous :

* lire continuellement l'état dans une boucle
* travailler avec les événements

L'événement sera rattaché à une fonction de rappel qui doit être définie dans le haut du programme.

La définition de la fonction commence par le mot-clé def et tout le corps de la fonction doit être décalé de 4 espaces.

Python

def bouton\_presse(channel):  
    print("Le bouton est enfoncé!")

Pour associer l'événement à la fonction de rappel :

Python

GPIO.add\_event\_detect(bouton,GPIO.RISING,callback=bouton\_presse)

ou

Python

GPIO.add\_event\_detect(bouton, GPIO.RISING)  
GPIO.add\_event\_callback(bouton, bouton\_presse)

## Réinitialisation des ports

En terminant, il est conseillé de réinitialiser les ports qui ont été utilisés dans le script. Ceci permet de les protéger d'un bris dû à un court-circuit.

Attention : si un script a pour but d'allumer une lumière et de la laisser allumée, il ne faut pas qu'il réinitialise les ports.

Quand on réinitialise les ports, ils sont de nouveau disponibles pour un autre script Python.

De plus, les DEL allumées seront éteintes dès que la réinitialisation est faite.

Python

GPIO.cleanup()

Pour assurer que la réinitialisation ait lieu même si le programme plante ou s'il se termine quand l'usager appuie sur les touches Ctrl+C, on placera le code dans un try et on fera la réinitialisation dans le finally.

Python

try:   
    ...  
except:  
    ...  
finally:  
    GPIO.cleanup()

Note : le finally ne sera pas exécuté si l'usager termine le programme avec les touches Ctrl+Z. En effet, alors que Ctrl+C émet un signal SIGINT – qui arrête gentiment le programme, Ctrl+Z émet un signal SIGTSTP qui arrête immédiatement le programme.

## Exemple de base : allumer une DEL

Voici un tout petit script qui s'occupe d'envoyer un signal pour allumer une DEL.

Python

#!/usr/bin/env python3  
# -\*- coding:utf-8 -\*-

 

"""  
Allume une DEL rouge sur le Raspberry Pi  
Paramètres : aucun  
Montage : DEL rouge branchée sur GPIO.BCM 23 et résistance de 330 Ohms  
Auteur : Christiane Lagacé  
Date : 17 septembre 2025  
"""  
  
import RPi.GPIO as GPIO    # il faudra mettre GPIO. devant le nom des classes du paquet  
  
GPIO.setmode(GPIO.BCM)    # type d'adressage broadcom (numéros de ports)  
led = 23                   # adresse broadcom du branchement de la DEL  
GPIO.setup(led, GPIO.OUT)  # sens du signal : le Pi peut envoyer un signal à sa broche (ici, au port 23)  
  
print(f'Programme qui allume une DEL branchée au port BCM {led}')  
GPIO.output(led, 1)     # envoie 3.3V au port  
# pas de GPIO.cleanup() ici sinon la DEL serait immédiatement éteinte.

## Exemple complet : faire clignoter une DEL

Pour faire exemple un peu plus complexe, voici un petit script qui fait clignoter une DEL jusqu'à ce que quelqu'un appuie sur Ctrl+C.

Python

#!/usr/bin/env python3  
# -\*- coding:utf-8 -\*-

 

"""  
Fait clignoter une DEL rouge sur le Raspberry Pi  
Paramètres : aucun  
Montage : DEL rouge branchée sur GPIO.BCM 23 et résistance de 330 Ohms  
Auteur : Christiane Lagacé  
Date : 17 septembre 2025  
"""  
  
import RPi.GPIO as GPIO    # il faudra mettre GPIO. devant le nom des classes du paquet  
from time import sleep     # les classes du paquets peuvent être utilisées directement sans le nom du paquet  
  
GPIO.setmode(GPIO.BCM)    # type d'adressage broadcom (numéros de ports)  
led = 23                   # adresse broadcom du branchement de la DEL  
GPIO.setup(led, GPIO.OUT)  # sens du signal : le Pi peut envoyer un signal à sa broche (ici, au port 23)  
  
print('Programme qui fait clignoter une DEL')  
print('Appuyez sur Ctrl+C pour terminer.')  
  
try:  
    while True:  
        GPIO.output(led, 1)     # envoie 3.3V au port  
        sleep(1)  
        GPIO.output(led, 0)     # n'envoie rien au port  
        sleep(1)  
except KeyboardInterrupt:  
    print('Fin du programme, vous avez appuyé sur Ctrl+C.')  
except Exception as e:  
    print('Une exception est survenue.' + str(e))  
finally:  
    GPIO.cleanup()     # réinitialise les ports  
    print('Nettoyage final réalisé avec succès!')

## Lancer le script

Pour exécuter le script, entrez la commande python3 suivie du nom du fichier.

Terminal

python3 monscript.py

## Pour plus d'information

« RasPi.TV - RPi.GPIO Quick Reference ». RasPi.TV. <https://raspi.tv/download/RPi.GPIO-Cheat-Sheet.pdf>

« RPi.GPIO basics 3 – How to Exit GPIO programs cleanly, avoid warnings and protect your Pi ». RasPi.TV. <https://raspi.tv/2013/rpi-gpio-basics-3-how-to-exit-gpio-programs-cleanly-avoid-warnings-and-protect-your-pi>

« RPi.GPIO basics 6 – Using inputs and outputs together with RPi.GPIO – pull-ups and pull-downs ». RasPi.TV. <https://raspi.tv/2013/rpi-gpio-basics-6-using-inputs-and-outputs-together-with-rpi-gpio-pull-ups-and-pull-downs>

## 47.4 Script pour réinitialiser toutes les broches programmables du GPIO

Si vous travaillez avec la bibliothèque [apical\_lien\_interne][installation\_de\_la\_bibliotheque\_rpi\_gpio,RPi.GPIO][/apical\_lien\_interne], vous savez que la méthode GPIO.cleanup() réinitialise les ports que vous avez utilisés.

Il est donc bon de terminer vos scripts par un appel à cette méthode.

Mais si vous avez lancé un script qui allume une DEL sur une planche de maquettage et que ce script ne s'est pas terminé normalement, la DEL restera allumée.

Il vous faut une méthode pour réinitialiser les broches du GPIO.

Puisque GPIO.cleanup() ne travaille que sur les ports qui ont été utilisés dans le même script, je vous ai concocté un petit script qui utilise tous les ports afin de pouvoir bien les réinitialiser.

Python

#!/usr/bin/env python3  
# -\*- coding:utf-8 -\*-  
  
"""  
Réinitialise toutes les broches programmables sur le Raspberry Pi  
Paramètres : aucun  
Montage : aucun  
Auteur : Christiane Lagacé  
Date : 16 septembre 2021  
"""  
  
import RPi.GPIO as GPIO  
  
# Le but du script est justement de libérer les ports alors on ne veut pas voir le message :  
# RuntimeWarning: This channel is already in use, continuing anywa  
GPIO.setwarnings(False)  
  
GPIO.setmode(GPIO.BOARD)  
  
print('Programme qui réinitialise toutes les broches programmables du Raspberry Pi')  
broches = (3,5,7,8,10,11,12,13,15,16,18,19,21,22,23,24,26,29,31,32,33,35,36,37,38,40)  
  
print('Sens actuel des broches (numérotation physique) :')

 

 

 

for i in broches:  
    sens = GPIO.gpio\_function(i)  
  
    # On réassigne le même sens que la broche avait car le cleanup n'a d'effet que pour les broches affectées par le script  
    if sens == 1:  
        GPIO.setup(i, GPIO.IN)  
    else:  
        GPIO.setup(i, GPIO.OUT)  
  
    print(str(i) + ': ' + ('IN' if sens else 'OUT'))  
  
GPIO.cleanup()  
print('Réinitialisation réalisée avec succès!')

## 47.5 Passer un paramètre à un script Python

Il est possible de passer un ou plusieurs paramètres, aussi appelés arguments, à un script Python à partir de la ligne de commande.

Terminal

python3 monscript.py unparametre autreparametre

Pour lire la valeur des paramètres dans le script, il faut d'abord importer le module sys.

Python

import sys

Les paramètres sont contenus dans un tableau nommé sys.argv.

L'élément 0 du tableau est toujours le nom du script.

L'élément 1 est le premier argument, l'élément 2 est le second argument et ainsi de suite.

Python

nom\_script = sys.argv[0]  
premier\_parametre = sys.argv[1]  
deuxieme\_parametre = sys.argv[2]

## Si aucun paramètre n'est passé (paramètre optionnel)

Si le script tente de lire un paramètre alors qu'aucun n'a été passé, le script lèvera une exception de type IndexError.

Il faut donc toujours lire le paramètre dans un try... except.

Lorsqu'aucun paramètre n'est passé, le programme réagira en conséquence. Il pourrait, par exemple, fournir une valeur par défaut.

Python

try:  
    valeur = sys.argv[1]  
 except IndexError:  
    valeur = "x"

## Paramètre numérique

À la base, les paramètres sont tous de type texte.

Si le paramètre doit être utilisé comme un nombre, il faut d'abord le convertir.

Python

try:  
    iterations = int(sys.argv[1])  
...  
  
for i in range(iterations):  
    ...

## Paramètre numérique optionnel

En combinant les deux approches précédentes, on s'assure que dans le cas d'un paramètre numérique, le programme fonctionne s'il n'est pas passé ou si sa valeur n'est pas numérique.

Python

try:  
    iterations = int(sys.argv[1])  
 except IndexError:  
    iterations = 1   # arrivera ici si aucun paramètre n'est passé  
except:  
    iterations = 1   # arrivera ici si le paramètre n'était pas numérique

## Pour plus d'information

« Python Command Line Arguments ». Real Python. <https://realpython.com/python-command-line-arguments/#the-sysargv-array>

## 47.6 La syntaxe Python vs autres langages

Si vous avez déjà travaillé avec quelques langages de programmation, vous savez que la syntaxe varie d'un langage à l'autre. Parfois, les différences sont minimes mais d'autre fois, elles peuvent être déroutantes.

Pour vous aider à vous acclimater à Python, voici quelques éléments de syntaxe à connaître et leur comparaison avec d'autres langages.

|  | Python | JavaScript | PHP | C# |
| --- | --- | --- | --- | --- |
| Chaînes de caractères | nom = "Annie"  ou  nom = 'Annie'  Les deux sont équivalents mais les programmeurs préfèrent généralement les apostrophes.  Les triples apostrophes ou guillemets permettent de générer une chaîne incluant les sauts de ligne et tabulations. Très utile pour générer du HTML ou du JSON.  html = '''      <ul>      <li>Premier élément</li>      <li>Deuxième élément</li>      </ul>  '''  L'ajout d'un b devant une chaîne transformera cette chaîne en une chaîne d'octets, requis dans certains contextes précis.  chaine\_octets = b"Bonjour"  L'ajout d'un f devant une chaîne permet de la formater.  nom = 'Annie'  salutation = f'Bonjour, {nom}!' | nom = "Annie";  ou  nom = 'Annie'; | $nom = "Annie";  ou  $nom = 'Annie';  La version avec guillemets permet d'interpréter des variables dans la chaîne.  $texte = "Bonjour $nom";  La version avec apostrophes est très légèrement plus rapide. | nom = "Annie"; |
| Booléens | True  False    Sensible à la casse | true  false    Sensible à la casse | True ou true ou TRUE  False ou false ou FALSE    Insensible à la casse | true  false    Certaines fonctions C# retournent cependant True ou False...    bool valeur = true;  Console.WriteLine(valeur); // True |
| Opérateurs booléens | and  or  not | &&  ||  ! | && ou and  || ou or  ! | &&  ||  ! |
| Concaténation | nom\_complet = prenom + ' ' + nom\_famille | nomComplet = prenom + ' ' + nomFamille; | $nomComplet = $prenom . ' ' . $nomFamille; | nomComplet = prenom + '" " + nomFamille; |
| Incrémentation | i += 1 | i += 1; ([affectation après addition](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Operators/Addition_assignment))  i++ ([opérateur d'incrémentation en suffixe](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Operators/Increment))  ++i (opérateur d'incrémentation en préfixe) | $i += 1;  $i++ ([post-incrémente](https://www.php.net/manual/fr/language.operators.increment.php))  ++$i (pré-incrémente) | i += 1;  i++  ++i |
| Conversion de type | nombre= int(saisie) | nombre = parseInt(saisie); | $nombre = (int)$saisie;  ou  $nombre = intval($saisie); | nombre = Convert.ToInt32(saisie);  ou  Int32.TryParse(saisie, out nombre); |
| Affichage à l'écran | print(nom)  ou, pour éviter les sauts de ligne :  print(nom, end='')    On peut interpréter des variables dans une chaîne : print(f"Votre score est {score}") | L'affichage se fait à l'aide de manipulations du DOM :  balise.innerHTML = nom;    Si on utilise jQuery :  $(balise).html(nom);    Pour afficher à la console :  console.log(nom);    Pour afficher dans une fenêtre popup :  window.alert(nom); | echo $nom; | Dans une page Web :  Response.Write(nom);    À la console :  Console.WriteLine(nom); |
| Lecture à la console | nombre = input('Veuillez entrer un nombre : ') |  |  | Console.WriteLine("Veuillez entrer un nombre : ");  nombre = Console.ReadLine(); |
| Tableaux | valeurs = ['a', 'b', 'c']  En Python, on dit que c'est une [liste](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) (modifiable, longueur variable)  Il existe également des [tuples](https://docs.python.org/3/tutorial/datastructures.html#tut-tuples) (immuables mais plus performants) :  valeurs = ('a', 'b', 'c')  ou, s'il y a un seul élément dans le tuple :  valeurs = ('a',) | var valeurs = ['a', 'b', 'c']; | $valeurs = ['a', 'b', 'c']; | string[] valeurs = {"a", "b", "c"}; |
| Tableaux associatifs (dictionnaires) | configuration = {      'menu': 'gauche',      'langue': 'fr'  }  ...  valeur = configuration['langue'] | var configuration = {      'menu' : 'gauche',      'langue': 'fr' };  ...  valeur = configuration['langue']; | $configuration = [      'menu' => 'gauche',      'langue' => 'fr',  ];  ...  $valeur = $configuration['langue'] | Dictionary<string, string> configuration = new Dictionary<string, string>()  {      {"menu","gauche"},      {"langue", "fr"}  };  ...  valeur = configuration["langue"]; |
| Vérifier si une valeur fait partie d'une liste de valeurs | if i in (3, 6, 9):      ... |  |  |  |
| Conditions | if nom == 'Annie':      ...  elif nom == 'Toto':      ...  else:      ...    Note : l'indentation (4 espaces) est importante : c'est elle qui indique quand un bloc d'instruction se termine. | if (nom == 'Annie') {      ...  } else if (nom == 'Toto') {      ...  } else {      ...  } | if ($nom == 'Annie') {      ...  } elseif ($nom == 'Toto') {      ...  } else {      ...  } | if (nom == "Annie)  {      ...  }  else if (nom == "Toto")  {      ...  }  else  {      ...  } |
| Boucles while | while x < 10:      ... | while (x < 10) {      ...  } | while (x < 10) {      ...  } | while (x < 10) {      ...  } |
| Boucles sur un nombre déterminé d'itérations | for i in range(10):      ...    La boucle pourrait commencer à une autre valeur que 0, il est possible de spécifier le départ, la fin (exclue de la boucle) et la valeur du saut :  for i in range(1, 10, 1)      ... | for (i = 0; i < 10; i++) {      ...  } | for ($i = 0; $i < 10; $i++) {      ...  } | for (i = 0; i < 10; i++)  {      ...  } |
| Boucles sur les éléments d'un tableau | valeurs = ['a', 'b', 'c']  for valeur in valeurs:      ... | var valeurs = ['a', 'b', 'c'];    for (var valeur in valeurs) {      ...  } | $valeurs = ['a', 'b', 'c'];    foreach ($valeurs as $valeur) {      ...  } | string[] valeurs = {"a", "b", "c"};    foreach (int valeur in valeurs)  {      ...  } |
| Opérateur ternaire (inline if) | valeur\_si\_vrai if condition else valeur\_si\_faux    Remarquez que l'ordre des opérandes est différent des autres langages.  Ex :  majeur = True if age >= 18 else False | condition ? valeurSiVrai : valeurSiFaux | condition ? valeurSiVrai : valeurSiFaux | condition ? valeurSiVrai : valeurSiFaux |
| Exceptions | try:      ...  except TypeException as e:      ... # traitement d'une exception précise  except Exception as e:      ... # traitement des autres exceptions  else:      ... # traitement si pas d'exception  finally:      ... # traitement si exception ou non | try {      ...  } catch (e) {      if (e instanceof TypeException) {          ... // traitement d'une exception précise      } else {          ... // traitement des autres exceptions      }  }  finally {      ... // traitement si exception ou non  } | try {      ...  } catch (TypeException $e) {      ... // traitement d'une exception précise  } catch (Throwable $e) {      ... // traitement des autres exceptions si PHP 7  } catch (Exception $e) {      ... // traitement des autres exceptions si PHP 5.X  } finally {      ... // traitement si exception ou non  } | try  {      ...  }  catch (TypeException)  {      ... // traitement d'une exception précise  }  catch (Exception e)  {      ... // traitement des autres exceptions  }  finally  {      ... // traitement si exception ou non  } |
| Commentaires | # | //  /\* ... \*/ | #  //  /\* ... \*/ | //  /\* ... \*/ |
| Commentaires de documentation | Cette documentation d'appelle [Docstring](https://www.python.org/dev/peps/pep-0257/).    def ma\_fonction(parametre):      """Résumé de la fonction sous forme impérative.        Autres paragraphes pour documenter les paramètres et la valeur de retour.        """      ... | function maFonction(parametre)  {      /// <summary>Résumé de la fonction.</summary>      /// <param name="parametre" type="Number">Description du paramètre.</param>      /// <returns type="Number">Description de la valeur de retour.</returns>      ...  } | Cette documentation s'appelle [phpDocumentor](https://www.phpdoc.org/).    /\*\*   \* Résumé de la fonction.   \*   \* @param int $parametre Description du paramètre.   \*   \* @author Annie Gagnon <anniegagnon@gmail.com>   \* @return int Description de la valeur de retour.   \*   \*/  function maFonction(int $parametre) : int {      ...  } | /// <summary>  /// Résumé de la fonction.  /// </summary>  /// <param name="parametre">Description du paramètre.</param>  /// <returns>Description de la valeur de retour.</returns>  int MaFonction(int parametre)  {      ...  } |
| Constante pour changement de ligne qui vaudra  '\n' (systèmes Unix comme Linux et Mac)  ou  '\r\n' (Windows) | [os.linesep](https://docs.python.org/fr/3/library/os.html?highlight=os%20linesep#os.linesep) |  | [PHP\_EOL](http://php.net/manual/en/reserved.constants.php#constant.php-eol) | [Environment.NewLine](https://msdn.microsoft.com/fr-fr/library/system.environment.newline(v=vs.110).aspx) |
| Valeur nulle | variable = None | let variable = null; | $variable = NULL; | string variable = null; |
|  | Python | JavaScript | PHP | C# |

Pour compléter ce tableau, voici quelques normes de programmation généralement appliquées dans différents langages.

|  | [Python](https://www.python.org/dev/peps/pep-0008/) | [JavaScript](https://google.github.io/styleguide/jsguide.html) | [PHP](http://www.php-fig.org/psr/psr-1/) | [C#](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions) |
| --- | --- | --- | --- | --- |
| Projets | Il n'y a pas de convention officielle pour le nom du projet.  Voici ce que je vous suggère :  touteenminuscules  ou  casse\_serpent  Sous PyCharm, puisque l'environnement de développenent est copié pour chacun des projets, je vous suggère de regrouper dans un même projet tous vos exercices qui utilisent une même base de données.  Ceux qui n'utilisent aucune BD pourront être placés par exemple dans un projet console\_sans\_bd et dans un autre projet graphique\_sans\_bd. |  |  |  |
| Espaces de noms | toutenminuscules |  |  |  |
| Fichiers | toutenminuscules  ou  casse\_serpent | toutenminuscules  ou  minuscules-avec-traits-d-union | Dépend du framework utilisé |  |
| Noms de variables | casse\_serpent | casseChameau | Le guide officiel précise qu'aucune recommandation n'est faite pour le nom des variables.  Cependant, la casseChameau est la plus utilisée.  Les variables débutent obligatoirement par un $. | casseChameau |
| Noms de classes | CassePascal | CassePascal | CassePascal | CassePascal |
| Noms de fonctions | casse\_serpent | casseChameau | casseChameau | CassePascal |
| Noms de constantes | MAJUSCULES\_AVEC\_CASSE\_SERPENT | MAJUSCULES\_AVEC\_CASSE\_SERPENT | MAJUSCULES\_AVEC\_CASSE\_SERPENT | CassePascal |
|  | Python | JavaScript | PHP | C# |

## Pour plus d'information

« Python 3.6.4 documentation ». Python. <https://docs.python.org/3.6/index.html>

« Learning Python: From Zero to Hero ». Medium. <https://medium.freecodecamp.org/learning-python-from-zero-to-hero-120ea540b567>

« PEP 8 -- Style Guide for Python Code ». Python. <https://www.python.org/dev/peps/pep-0008/>

« PEP257: Good Python docstrings by example ». Dolph Mathews. <http://blog.dolphm.com/pep257-good-python-docstrings-by-example/>

## 47.7 Copier un fichier sur une machine Linux à partir d'un autre ordinateur et vice-versa

Dans cette fiche :

* [Commande scp](#scp)
  + [Copie de l'ordinateur vers le Raspberry Pi](#ordiverspi)
  + [Copier du Raspberry Pi vers l'ordinateur](#piversordi)
  + [Copie d'un dossier complet](#dossiercomplet)
  + [Accès qui nécessite un port particulier](#port)
  + [Erreur serveur non trouvé](#nontrouve)
* [Copie à l'aide d'une clé USB](#usb)

## Commande scp

La commande scp (Secure CoPy), est très intéressante pour copier des fichiers d'un ordinateur vers un autre.

Il est possible de l'utiliser, par exemple, pour copier un fichier d'un ordinateur vers un Raspberry Pi ou vice-versa.

On appellera machine locale la machine (l'ordinateur ou le Pi) sur laquelle on entre la commande.

On appellera machine distante l'autre machine impliquée dans l'échange.

Un [apical\_lien\_interne][activer\_ssh\_sur\_le\_raspberry\_pi,le serveur SSH doit être activé][/apical\_lien\_interne] sur la machine distante. C'est généralement le cas sur le Raspberry Pi mais pas sur l'ordinateur.

C'est pourquoi la commande sera entrée sur le terminal de l'ordinateur, peu importe quelle machine contient le fichier à copier.

Le format de la commande scp est :

Syntaxe sur le terminal de l'ordinateur

scp source cible

Pour identifier la machine distante, on fera précéder la source ou la cible, selon le cas, par usager@adresse IP de la machine distante, suivi de deux points. Des exemples sont donnés dans les sections qui suivent.

### Copie de l'ordinateur vers le Raspberry Pi

Pour copier un fichier à partir de l'ordinateur vers le Pi, la machine distante sera la cible.

Entrez cette commande en prenant soin de changer pi pour le nom de votre usager sur Raspberry Pi OS et l'adresse IP pour celle du Pi.

Terminal de l'ordinateur

scp dossierlocal/monfichier.extension pi@192.168.1.145:/dossierdistant/sous-dossier

### Copier du Raspberry Pi vers l'ordinateur

Pour copier un fichier du Pi vers votre ordinateur, la machine distante sera la source.

Terminal de l'ordinateur

scp pi@192.168.1.145:/dossierdistant/sous-dossier/monfichier.extension /dossierlocal

### Copie d'un dossier complet

L'option -r permet de copier un dossier complet entre le Raspberry Pi et l'ordinateur.

Il faut spécifier le nom du dossier à copier sans le faire suivre d'une barre oblique ni d'un astérisque.

Pour copier le dossier de l'ordinateur vers le Pi :

Terminal de l'ordinateur

scp -r /dossierlocal pi@192.168.1.145:/dossierdistant

Pour copier le dossier du Pi vers l'ordinateur :

Terminal de l'ordinateur

scp -r pi@192.168.1.145:/dossierdistant /dossierlocal

### Accès qui nécessite un port particulier

Certains systèmes, par exemple Home Assistant, exigent l'utilisation d'un port particulier pour un accès SSH. Ce port devra lui aussi être utilisé avec scp.

Dans cet exemple, j'ai travaillé avec l'usager root et le port 22222 puisque ce sont ces valeurs qui sont utilisées sous Home Assistant.

Terminal de l'ordinateur

scp -P 22222 root@192.168.1.145:/dossierdistant/sous-dossier/monfichier.extension /dossierlocal

ou, pour copier de l'ordinateur vers le Pi :

Terminal de l'ordinateur

scp -P 22222 /dossierlocal root@192.168.1.145:/dossierdistant/sous-dossier/monfichier.extension

### Erreur serveur non trouvé

Lors de l'utilisation de la commande scp, le serveur SSH pourrait être configuré pour travailler par défaut en mode sécurisé.

Vous le saurez si vous obtenez le message d'erreur suivant :

sh: /usr/libexec/sftp-server: not found  
scp: Connection closed

Vous pourrez régler le problème en ajoutant l'option -O.

Selon la documentation de scp[1](https://man7.org/linux/man-pages/man1/scp.1.html#:~:text=Use%20the%20legacy%20SCP%20protocol) :

> -O : Use the legacy SCP protocol for file transfers instead of the SFTP protocol. Forcing the use of the SCP protocol may be necessary for servers that do not implement SFTP, for backwards-compatibility for particular filename wildcard patterns and for expanding paths with a ‘~’ prefix for older SFTP servers.

Terminal

scp -O -P 22222 root@192.168.1.145:/dossierdistant/sous-dossier/monfichier.extension /dossierlocal

## Copie à l'aide d'une clé USB

Pour effectuer une copie de fichier à l'aide d'une clé USB, suivez ces étapes :

* Copiez le fichier de l'ordinateur sur une clé USB puis insérez la clé dans le Raspberry Pi.
* Accédez à la ligne de commande du Pi soit [apical\_lien\_interne][se\_brancher\_au\_raspberry\_pi\_via\_ssh,via SSH][/apical\_lien\_interne], soit en y branchant un écran et un clavier.
* Vous devez monter la clé pour que son contenu soit accessible.
  + Si c'est la première fois que vous utilisez une clé USB sur le Pi, créez le dossier de montage.

    Terminal

    sudo mkdir /mnt/cleusb
  + Vous pouvez maintenant monter la clé. Généralement, elle est reconnue comme /dev/sda1 mais elle pourrait être autre chose, par exemple /dev/sdb1.

    Terminal

    sudo mount /dev/sda1 /mnt/cleusb
* Copiez le fichier de la clé USB vers le dossier désiré sur le Pi.

  Terminal

  cp /mnt/cleusb/monfichier.extension /dossier/sous-dossier
* Démontez la clé USB avant de la retirer du Pi.

  Terminal

  sudo umount /dev/sda1

## Source

1. « scp(1) — Linux manual page ». man7.org. [https://man7.org/linux/man-pages/man1/scp.1.html](https://man7.org/linux/man-pages/man1/scp.1.html#:~:text=Use%20the%20legacy%20SCP%20protocol)

## Pour plus d'information

« SCP (Secure Copy) ». Raspberry Pi. <https://www.raspberrypi.org/documentation/remote-access/ssh/scp.md>

## 47.8 Tuer un processus Linux

Quand un script Python est lancé, il est associé à un processus dans le système d'exploitation.

Si vous lancez un script Python qui est très long à exécuter ou qui comporte une boucle sans fin, il faudra le tuer pour qu'il se termine et libère les ressources qu'il utilise.

Pour tuer un processus au terminal, vous pouvez utiliser la commande [pkill](https://linuxize.com/post/pkill-command-in-linux/) suivie de -f puis du nom du script Python.

Terminal du Raspberry Pi

sudo pkill -f mon\_script.py

Une autre approche consiste à utiliser le numéro de processus.

Ce numéro peut être trouvé à l'aide de la commande ps.

Terminal du Raspberry Pi

ps -ef mon\_script.py

Notez qu'il est possible de faire afficher les en-têtes de colonnes comme suit :

Terminal du Raspberry Pi

ps -ef | head -1;ps -ef mon\_script.py

Résultat à l'écran

monnom@MacBook-Pro-de-MonNom ~ %ps -ef | head -1;ps -ef mon\_script.py  
UID     PID     PPID   C   TIME   TTY          TIME   CMD  
 501   84833    33164   0   8:49   ttys006   0:00.00   grep mon\_script.py  
 501   84730   80397   0   8:49   ttys007   0:14.34   /.../Python mon\_script.py

Peu importe si on a demandé l'affichage des en-têtes de colonnes ou non, la ligne de résultat dont la commande est grep mon\_script.py correspond à la commande ps elle-même. On peut donc l'ignorer.

La ou les autres lignes correspondent à des scripts en cours d'exécution. Le numéro de processus apparaît dans le seconde colonne.

Il est désormais possible d'arrêter le processus désiré :

Terminal du Raspberry Pi

kill -9 84730