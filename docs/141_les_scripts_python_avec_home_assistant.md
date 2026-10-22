# 122. Les scripts Python avec Home Assistant {#chapitre-les_scripts_python_avec_home_assistant}

Pour qu'une automatisation puisse appeler un script Python, vous devez d'abord ajouter l'intégration [Python Scripts](https://www.home-assistant.io/integrations/python_script/).

Ceci est réalisé en ajoutant cette ligne dans le fichier configuration.yaml.

Fichier configuration.yaml


```
python_script:
```


Un redémarrage du système est requis pour que ce soit disponible mais attendez, un redémarrage sera également requis à une prochaine étape.

## Dossier qui contient les scripts

Pour qu'un script Python puisse être exposé en tant qu'action, vous devez d'abord créer le dossier 'python_scripts' sous /mnt/data/supervisor/homeassistant.

Si vous travaillez à l'aide de File Editor ceci sera réalisé en cliquant sur l'icône New Folder alors que vous êtes dans le dossier config (c'est ce dossier qui représente /mnt/data/supervisor/homeassistant dans l'interface Web).

Vous pouvez également créer le dossier directement au terminal HassOS.


Une fois cette configuration en place, vous devez redémarrer le système pour qu'elle soit prise en compte.

Vous pouvez le faire maintenant puisque toutes les manipulations qui requièrent un redémarrage sont effectuées.

Par la suite, vous pourrez modifier votre script Python et l'automatisation qui l'utilise sans qu'un redémarrage ne soit nécessaire.

## Vérification de l'installation

Pour vérifier que l'intégration Python Scripts est bien installée, rendez-vous dans le menu Paramètres / Outils, puis l'onglet *Actions*,  l'action *python_script.reload* devrait apparaître.

Vous pouvez utiliser cette action pour recharger les scripts Python sans avoir à redémarrer le système.

Il est également possible de faire détecter les scripts Python que vous ajoutez à partir de *Paramètres -> Outils -> YAML -> Python Scripts*

## Écriture du script

Important : l'intégration Python Scripts ne permet pas aux script d'utiliser l'instruction *import*.

Le script peut être écrit directement dans File Editor ou encore être écrit sur votre ordinateur puis copié dans le dossier python_scripts sur le Pi [à l'aide de scp](53_scripts_python_pour_envoyer_et_recevoir_du_signal_sur_le_gpio.md#fiche-copier_un_fichier_sur_une_machine_linux_a_partir_d_un_autre_ordinateur).

Son nom doit se terminer par l'extension .py.

Fichier *hello_world.py*


```python
# Lit paramètre "name", default to "world"
name = data.get("name", "world")

# `logger`, 'datetime' `time` are available as builtin without the need of explicit import.
now = datetime.datetime.now()
iso_time = now.isoformat()

logger.warn(f"Hello {name} at {iso_time}")
```

# Appeler une action depuis un script Python

La commande pour appeler une action est `hass.services.call()`. Les actions sont définies par un domaine et un nom. 
* Le domaine est le nom de l'intégration, par exemple light, switch, input_number, etc.
* Le nom est le nom de l'action, par exemple turn_on, turn_off, set_value, etc.

Les actions s’appelaient auparavant des services dans Home Assistant, de là le nom de la classe `hass.services`.

Par exemple, pour allumer une lumière, vous pouvez utiliser le code suivant dans votre script Python.

```python
hass.services.call("light",                      # Domaine/intégration
                   "turn_on",                    # Nom de l'action
                   {"entity_id": "light.salon",  # Paramètres
                    "brightness": 255})
```

# Accéder aux états et attributs

```python
state_obj = hass.states.get("input_number.target_temperature")

if state_obj is not None:
    # La valeur des états est un chaîne de caractères 
    val = float(state_obj.state)
    logger.warn(f"input_number: {val}")

    min_val = state_obj.attributes.get("min")
    if min_val is not None:
        logger.warn(f"input_number min: {min_val}")
```

## Automatisation

Il est désormais possible d'utiliser votre script Python dans une automatisation, elle apparaîtra dans la liste des actions.

## Exercice 1 - intro

* Configurer votre Home Assistant pour qu'il puisse exécuter un script Python.
    * Référez-vous à la documentation officielle de [Python Scripts](https://www.home-assistant.io/integrations/python_script/) si vous rencontrez des difficultés.
* Tester l'exécution du script hello_world.py en utilisant l'action *python_script.hello_world* dans le menu Paramètres / Outils, puis l'onglet *Actions*.
* Vérifier que le message "Hello world at ..." apparaît dans le journal de Home Assistant.
* Assurez-vous que Z-Wave est fonctionnel et que vous pouvez contrôler vos appareils Z-Wave à partir de Home Assistant.
* Écrivez un script Python qui allume un appareil Z-Wave et l'exécutez-le à partir d'une automatisation.
    * (retrouver l'entity_id de votre appareil Z-Wave dans le menu Paramètres / Appareils et services / Entités)

## Exercice 2 - hystérésis

Une hystérésis est un mécanisme qui permet de ne pas déclencher une action tant que la valeur d'une variable n'a pas dépassé un certain seuil, puis de ne pas arrêter l'action tant que la valeur n'est pas redescendue en dessous d'un autre seuil.  Les hystérésis sont souvent utilisées pour éviter que des actions ne soient déclenchées trop fréquemment, par exemple démarrer et arrêter un système de chauffage.

![Exemple d'hystérésis](https://blogs.egu.eu/wp-content/uploads/sites/17/2020/12/Figure1.webp)

* Mise en situation : vous gérez un entrepôt et vous souhaitez que le chauffage se déclenche lorsque la température descend en dessous de 18°C et qu'il s'arrête lorsque la température remonte au-dessus de 20°C (hystérésis).  Vous avez 2 thermomètres pour mesurer la température: comme certains équipements dégagent parfois de la chaleur à proximité d'un thermomètre, vous utilisez la moyenne des 2 thermomètres pour déterminer la température de l'entrepôt.
* Écrivez un script Python qui calcule la moyenne de 2 thermomètres et qui active votre prise intelligente si la température est inférieure à 18°C et qui l'arrête si elle est supérieure à 20°C.
* Vous pouvez utiliser 2 capteurs de température virtuels pour tester votre script Python.