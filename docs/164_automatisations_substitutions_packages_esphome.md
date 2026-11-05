# 144. Automatisations, substitutions et packages ESPHome {#chapitre-automatisations_substitutions_packages_esphome}

## 144.1 Automatiser localement avec ESPHome {#fiche-automatisations-locales}

Une automatisation réagit à un événement et exécute une ou plusieurs actions. Dans ESPHome, un **déclencheur** repère l'événement, une **condition** décide si les actions doivent être exécutées et les **actions** indiquent le travail à faire.

Dans cet exemple, un appui sur le bouton lance un script seulement si la tension mesurée par le potentiomètre dépasse 2 V. Il reprend les identifiants `bouton`, `lecture_potentiometre` et `signaliser_appui` des fiches précédentes et de la section sur les packages ci-dessous.

```yaml
binary_sensor:
  - id: bouton
    on_press:
      then:
        - if:
            condition:
              sensor.in_range:
                id: lecture_potentiometre
                above: 2.0
            then:
              - script.execute: signaliser_appui
            else:
              - logger.log: "Potentiometre sous le seuil"
```

La déclaration complète du bouton doit déjà exister. On ajoute `on_press` à cette déclaration, sans créer une seconde entrée avec le même `id`. La condition `sensor.in_range` vérifie la mesure au moment de l'appui. La valeur de 2 V est un exemple : vérifier la plage réellement obtenue avec le potentiomètre.

### Réutiliser une séquence avec un script

Un script ESPHome nomme une séquence d'actions pour pouvoir l'appeler à partir d'une automatisation. Cet exemple allume brièvement la lumière `del_variable`, puis l'éteint :

```yaml
script:
  - id: signaliser_appui
    mode: single
    then:
      - light.turn_on: del_variable
      - delay: 500ms
      - light.turn_off: del_variable
```

Un script peut être appelé avec `script.execute`. Le mode `single` évite de lancer une deuxième exécution tant que la première est en cours.

### ESPHome et Home Assistant

Les automatisations ESPHome sont exécutées par le microcontrôleur. Par exemple, le bouton peut encore déclencher une action sur la DEL lorsque Home Assistant est temporairement inaccessible, tant que l'appareil est alimenté et que la logique nécessaire est dans sa configuration.

Une automatisation Home Assistant est exécutée par le serveur. Elle peut utiliser les entités de plusieurs appareils et les fonctions de Home Assistant, mais elle dépend de la disponibilité du serveur et de la communication avec l'appareil. Pendant une perte de connexion, Home Assistant peut ne plus recevoir l'état du bouton ou du potentiomètre et ne peut pas lui envoyer de commande.

!!! note

    Lors d'un test de déconnexion, garder la période courte et rétablir la connexion après l'observation. La configuration de l'API peut redémarrer l'appareil après une longue période sans connexion; un redémarrage n'indique donc pas nécessairement que l'automatisation locale dépend de Home Assistant.

## Substitutions dans le YAML {#fiche-substitutions}

Les substitutions permettent de définir une valeur une fois et de la réutiliser dans le fichier YAML. ESPHome remplace les expressions avant de valider et de compiler la configuration. Elles sont utiles pour adapter un même modèle à plusieurs appareils ou éviter les répétitions; ce ne sont pas des variables modifiables pendant l'exécution.

```yaml
substitutions:
  device_name: "xiao-del-01"
  device_label: "XIAO DEL 01"

esphome:
  name: ${device_name}
  friendly_name: "${device_label}"
```

On peut aussi réutiliser `device_label` dans les noms des entités, par exemple `name: "${device_label} - Bouton"`. Le nom technique de l'appareil doit être unique et respecter les règles de nommage d'ESPHome. Les substitutions sont sensibles à la casse.

Les mots de passe et les clés ne doivent pas être écrits en clair dans le fichier remis. Utiliser `secrets.yaml` pour les informations confidentielles; une substitution ne remplace pas un gestionnaire de secrets.

## Packages pour séparer la configuration {#fiche-packages}

Un package est un fragment de configuration YAML inclus dans le fichier principal de l'appareil. Il permet de regrouper des éléments réutilisables, par exemple des scripts, des capteurs ou des réglages communs. ESPHome fusionne la configuration du package avec celle du fichier principal.

Pour ce cours, créer le fichier `packages/commande_del.yaml` à côté du YAML principal de l'appareil :

```yaml
script:
  - id: signaliser_appui
    mode: single
    then:
      - light.turn_on: del_variable
      - delay: 500ms
      - light.turn_off: del_variable
```

Puis inclure ce fragment dans le YAML principal :

```yaml
packages:
  - !include packages/commande_del.yaml
```

Le chemin de `!include` est relatif au fichier YAML principal. Le fichier inclus contient le fragment `script:` seulement; il ne répète pas la clé `packages:`. L'identifiant `signaliser_appui` reste utilisable dans une automatisation du fichier principal.

Les packages locaux évitent de recopier du YAML et rendent les configurations plus faciles à organiser. Ils ne créent pas un appareil distinct et ne s'exécutent pas séparément.

## Références

* [Automatisations, actions, déclencheurs et conditions ESPHome](https://esphome.io/automations/actions/)
* [Substitutions ESPHome](https://esphome.io/components/substitutions/)
* [Packages ESPHome](https://esphome.io/components/packages/)