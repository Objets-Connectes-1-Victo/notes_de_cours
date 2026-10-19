# 122. Les scripts Python avec Home Assistant {#chapitre-les_scripts_python_avec_home_assistant}

## 122.1 Automatisation qui appelle un script Python {#fiche-automatisation_qui_appelle_un_script_python}

![Facultatif](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/ico-Facultatif.gif "Facultatif")

Pour qu'une automatisation puisse appeler un script Python, vous devez d'abord ajouter l'intégration [Python Scripts](https://www.home-assistant.io/integrations/python_script/).

Ceci est réalisé en ajoutant cette ligne dans le fichier configuration.yaml.

Fichier configuration.yaml


```
python_script:
```


Un redémarrage du système est requis pour que ce soit disponible mais attendez, un redémarrage sera également requis à une prochaine étape.

## Dossier qui contient les scripts

Pour qu'un script Python puisse être exposé en tant que service, vous devez d'abord créer le dossier 'python_scripts' sous /mnt/data/supervisor/homeassistant.

Si vous travaillez à l'aide de File Editor ceci sera réalisé en cliquant sur l'icône New Folder alors que vous êtes dans le dossier config (c'est ce dossier qui représente /mnt/data/supervisor/homeassistant dans l'interface Web).

Vous pouvez également créer le dossier directement au terminal HassOS.


Une fois cette configuration en place, vous devez redémarrer le système pour qu'elle soit prise en compte.

Vous pouvez le faire maintenant puisque toutes les manipulations qui requièrent un redémarrage sont effectuées.

Par la suite, vous pourrez modifier votre script Python et l'automatisation qui l'utilise sans qu'un redémarrage ne soit nécessaire.

## Vérification de l'installation

Pour vérifier que l'intégration Python Scripts est bien installée, rendez-vous dans le menu Paramètres / Outils, puis l'onglet *Actions*,  l'action *python_script.reload* devrait apparaître.

Vous pouvez utiliser cette action pour recharger les scripts Python sans avoir à redémarrer le système.

## Écriture du script

Important : l'intégration Python Scripts ne permet pas aux script d'utiliser l'instruction import.

Le script peut être écrit directement dans File Editor ou encore être écrit sur votre ordinateur puis copié dans le dossier python_scripts sur le Pi [à l'aide de scp](53_scripts_python_pour_envoyer_et_recevoir_du_signal_sur_le_gpio.md#fiche-copier_un_fichier_sur_une_machine_linux_a_partir_d_un_autre_ordinateur).

Son nom doit se terminer par l'extension .py.

Fichier hello_world.py


```python
name = data.get("name", "world")

# `logger` and `time` are available as builtin without the need of explicit import.
logger.warn("Hello {} at {}".format(name, time.time()))
```



## Automatisation

Il est désormais possible d'utiliser votre script Python dans une automatisation, elle apparaîtra dans la liste des actions.

## Exercice

* Configurer votre Home Assitant pour qu'il puisse exécuter un script Python.
  * Référez-vous à [Python Scripts](https://www.home-assistant.io/integrations/python_script/) si vous rencontrez des difficultés.
* Tester l'exécution du script hello_world.py en utilisant l'action *python_script.hello_world* dans le menu Paramètres / Outils, puis l'onglet *Actions*.
* Vérifier que le message "Hello world at ..." apparaît dans le journal de Home Assistant.
* Assurez-vous que Z-Wave est fonctionnel et que vous pouvez contrôler vos appareils Z-Wave à partir de Home Assistant.
* Écrivez un script Python qui allume un appareil Z-Wave et l'exécutez-le à partir d'une automatisation.
  * (retrouver l'entity_id de votre appareil Z-Wave dans le menu Paramètres / Appareils et services / Entités)


