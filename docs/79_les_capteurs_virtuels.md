# 70. Les capteurs virtuels {#chapitre-les_capteurs_virtuels}

## 70.1 Configurer un capteur virtuel {#fiche-configurer_un_capteur_virtuel}

Vous souhaitez faire des tests dans Home Assistant sans devoir vous procurer un capteur ou un récepteur réel?

Vous désirez tester une automatisation basée sur la présence et vous ne souhaitez pas devoir courir loin de la maison pour chacun de vos tests?

Ou encore, vous désirez tester une automatisation basée sur la température et vous ne souhaitez pas devoir attendre l'hiver pour la tester?

Les **capteurs virtuels** (entrées) vous permettront de faire vos tests facilement.

Les capteurs virtuels permettent également d'étendre les fonctionnalités de Home Assistant, par exemple [créer une automatisation qui tient compte de l'heure](93_automatisations_qui_tiennent_compte_de_lheure.md#fiche-automatisation_qui_tient_compte_de_l_heure).

Il est possible de créer un capteur virtuel à l'aide de l'interface graphique ou à l'aide du fichier configuration.yaml.

Peu importe la technique utilisée, les capteurs virtuels seront enregistrés avec les autres entités dans le fichier /mnt/data/supervisor/homeassistant/.storage/core.entity_registry.

## Création d'un capteur virtuel à l'aide de l'interface graphique

Les capteurs virtuels peuvent être créés à l'aide de l'interface graphique de Home Assistant.

En plus du fichier core.entity_registry, les capteurs ajoutés via l'interface graphique seront enregistrés dans le dossier /mnt/data/supervisor/homeassistant/.storage, dans un fichier qui porte le nom du type de capteur virtuel (input_boolean, input_datetime, input_number, etc.).

Pour créer un capteur virtuel à l'aide de l'interface graphique :

* Paramètres / Appareils et services / Onglet Entrées (en anglais, ce sera Helpers) / Créer une entrée.
* Sélectionnez le type désiré (faites défiler les options au besoin).

  Un des types très utilisés est l'interrupteur, qui correspond au input_boolean. Ceci crée un virtuel qui peut avoir deux états, par exemple allumé/éteint, ouvert/fermé, levé/baissé, etc.

  ![Ajouter une entrée](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-AjouterUneEntree.png)

Le capteur apparaîtra comme suit dans la page Aperçu et on pourra changer son état afin de faire réagir les automatisations qui l'utilisent.

  ![Porte virtuelle](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-PorteVirtuelleDansApercu.png)

## Création d'un capteur virtuel à l'aide du fichier configuration.yaml

Vous pouvez également créer vos capteurs virtuels en entrant directement des lignes de code dans [le fichier configuration.yaml](77_le_fichier_configurationyaml.md#fiche-Editer_le_fichier_configuration_yaml).

Cette technique vous offre plus d'options.

Notez que seul les capteurs virtuels créés par code apparaîtront dans ce fichier. Ceux créés à l'aide de l'interface graphique n'y apparaîtront pas.

Fichier configuration.yaml


```
# Capteurs virtuels
input_boolean:
  porte_virtuelle:
    name: Porte virtuelle
    icon: mdi:door
```


Comme pour toute modification directement dans le fichier de configuration, un [rechargement](77_le_fichier_configurationyaml.md#fiche-Editer_le_fichier_configuration_yaml) sera nécessaire pour que ce capteur virtuel soit visible dans la liste des Entrées (Helpers). 

> Les capteurs virtuels créés par code ne sont pas visibles dans la page Aperçu initialement.  Vous pouvez allez dans les paramètres de l'entrée (onglet Entrées / Helpers) et sélectionner une pièce pour l'y ajouter.

### Propriétés des capteurs virtuels

Pour chaque capteur, on spécifie :

* son type :
  * [input_boolean](https://www.home-assistant.io/integrations/input_boolean/)
  * [input_select](https://www.home-assistant.io/integrations/input_select/)
  * [input_datetime](https://www.home-assistant.io/integrations/input_datetime/)
  * [input_number](https://www.home-assistant.io/integrations/input_number/)
  * [input_text](https://www.home-assistant.io/integrations/input_text/)
* son identifiant (unique, composé uniquement de lettres minuscules, de chiffres et de barres de soulignement)
* son nom tel qu'il apparaîtra dans Aperçu
* sa valeur initiale au démarrage de Home Assistant (note : les input_boolean utilisent on et off)
* son icône, choisie dans [la bibliothèque Material Design](78_les_icones.md#fiche-icones_material_design_dans_home_assistant)
* autres configurations propres au type de capteur virtuel (ex : liste des options disponibles pour input_select)

Il est possible de définir plusieurs capteurs virtuels du même type en les plaçant dans le même bloc.

Fichier configuration.yaml


```
# Capteurs virtuels
input_boolean:
  porte_virtuelle:
    name: Porte virtuelle
    icon: mdi:door
  presence_jeanne:
    name: Présence de Jeanne
    icon: mdi:face-profile-woman
input_number:
  temperature_virtuelle:
    name: Température virtuelle
    initial: 20
    min: -35
    max: 35
    step: 1
    icon: mdi:thermometer
```
