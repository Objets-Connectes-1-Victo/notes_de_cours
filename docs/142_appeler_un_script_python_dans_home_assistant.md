<a id="fiche-travailler_avec_l_integration_python_scripts"></a>
# 123. Appeler un script Python dans Home Assistant

<a id="fiche-le_dashboard_jeedom"></a>
## 123.1 Travailler avec l'intégration Python Scripts

PAS TERMINÉ...

L'intégration [Python Scripts](https://www.home-assistant.io/integrations/python_script/) permet de créer des services dans Home Assistant qui consistent à appeler un script Python.

Le code Python pourra manipuler les objets connectés (ex : allumer une lumière), écrire dans un fichier journal, effectuer des calculs, modifier l'état d'un capteur virtuel, etc.

Mais attention : il n'est pas possible d'importer des bibliothèques Python externes. Donc, pas d'instruction import.

## Activer Python Scripts

Pour permettre à Home Assistant d'utiliser l'intégration Python Scripts, il suffit d'ajouter ceci dans le fichier configuration.yaml :

Fichier configuration.yaml

python_script:

## Création du script Python

Les scripts Python doivent être sur le Rapsbery Pi. Vous pouvez les créer à partir d'une fenêtre SSH ou encore directement dans le <a href="fiche-travailler_avec_le_module_complementaire_file_editor.md#travailler_avec_le_module_complementaire_file_editor">module complémentaire File Editor</a>.

Dans le dossier /mnt/data/supervisor/homeassistant/, là où se trouve le fichier configuration.yaml, vous devez créer un sous-dossier nommé python_scripts. C'est dans ce dossier que vous placerez les fichiers qui contiennent le code Python.

## Lancer le script Python

Le script Python sera appelé comme un service, par exemple comme action dans une automatisation.

Dans le code YAML qui fera appel à ce service, par exemple dans le code YAML d'une automatisation, sur la ligne service, vous devez entrer le nom du fichier Python, sans l'extension .py.

Le service peut travailler avec une entité en particulier et il peut recevoir des paramètres sous forme clé-valeur ou, si vous préférez, variable-donnée.

YAML

- id: ...  
  alias: ...  
  trigger:  
  - ...  
  action:  
  - service: python_script.nom_du_fichier_python  
    target:  
      entity_id: sensor.cleaning_ladies_time_at_house  
    data:  
      variable: donnee  
<a id="chapitre-les_themes_dans_home_assistant"></a>
  mode: single

## Code Python

Le code Python récupérera le entity_id comme suit :

Python

entity_id = data.get("entity_id")

Si vous avez passé des variables dans la zone data, elle seront récupérées comme suit :

Python

ma_variable = data.get("variable", valeur_par_defaut)

Le code Python peut appeler différents services dans Home Assistant.

Pour appeler un service :

Python

service_data = {"variable": donnee, "variable2": donnee2}  
hass.services.call("domaine", "service", service_data, False)

Le domaine est la partie avant le point dans le nom du service. Par exemple, pour le service input_text.set_value, le domaine est input_text.

Le service est la partie après le point, par exemple set_value.

...

Vous devez redémarrer Home Assistant pour que le tout soit fonctionnel.