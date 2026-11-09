# 146. Filtres, lambdas et capteurs template ESPHome {#chapitre-filtres_lambdas_capteurs_template_esphome}

## 146.1 Transformer une mesure avec des filtres

Les filtres transforment les valeurs d'un capteur avant leur publication. Ils ne créent pas un nouveau capteur ni une nouvelle entité : ils changent la valeur publiée par le capteur auquel ils sont attachés. 

Voici quelques filtres fréquemment utilisés :

| Filtre | Rôle |
| --- | --- |
| `offset` | Ajouter ou soustraire une valeur constante, par exemple pour corriger un décalage. |
| `multiply` | Multiplier la mesure par un facteur, par exemple pour changer d'échelle. |
| `calibrate_linear` | Convertir une plage de valeurs à partir de points de calibration. |
| `clamp` | Limiter la valeur à un minimum et un maximum. |
| `round` | Arrondir la valeur à un nombre de décimales choisi. |
| `sliding_window_moving_average` | Lisser les variations en calculant une moyenne sur plusieurs lectures. |

Les filtres sont exécutés dans l'ordre où ils apparaissent dans le YAML. Cet ordre peut changer le résultat. Dans l'exemple ci-dessous, la tension est d'abord convertie en pourcentage, le résultat est ensuite limité à 0–100, puis arrondi à l'unité :

```yaml
sensor:
  - platform: adc
    pin: GPIO4 # Reprendre la broche et le capteur de l'exercice précédent
    attenuation: 12db
    id: lecture_potentiometre
    name: "Position du potentiomètre"
    update_interval: 1s
    filters:
      - calibrate_linear:
          - 0.10 -> 0
          - 3.00 -> 100
      - clamp:
          min_value: 0
          max_value: 100
      - round: 0
    unit_of_measurement: "%"
    accuracy_decimals: 0
```

Les tensions `0.10` et `3.00` sont des exemples : les remplacer par les valeurs minimale et maximale réellement mesurées. Après ces filtres, ce capteur publie un pourcentage, et non plus une tension en volts. Il ne faut donc pas utiliser cette même configuration si un calcul ultérieur s'attend à lire les volts d'origine. Pour cet autre cas, conserver le capteur ADC brut ou ne lui appliquer que des filtres qui préservent l'unité et l'échelle voulues.

Un filtre de lissage, placé avant ou après une conversion linéaire, ne donne pas toujours le même résultat qu'une limitation ou un arrondi placés à un autre endroit. Choisir et tester l'ordre en fonction du but : lisser les lectures, convertir leur échelle, limiter la plage ou simplifier l'affichage.

## 146.2 Écrire une lambda

En informatique, une expression lambda définit une fonction anonyme. Dans ESPHome, elle permet d'écrire une fonction C++ directement dans le YAML. Le fait qu'elle doive retourner une valeur dépend de son usage : un filtre ou un capteur template doit retourner la valeur à traiter ou à publier, tandis qu'une lambda utilisée pour exécuter une action peut se limiter à produire un effet, comme écrire dans les journaux. Une lambda est utile lorsque les filtres disponibles ne suffisent pas, par exemple pour effectuer plusieurs opérations ou appliquer des conditions. 

!!! note
    Dans un filtre lambda, **x** représente la valeur reçue à cette étape de la chaîne. Le résultat retourné devient l'entrée du filtre suivant.

```yaml
    filters:
      - lambda: |-
          return x * 100.0f / 3.3f;
      - clamp:
          min_value: 0
          max_value: 100
```

Cette lambda convertit approximativement une mesure de 0–3,3 V en pourcentage. Pour une mesure réelle, utiliser plutôt les valeurs calibrées observées. Une chaîne `calibrate_linear` suivie de `clamp` peut exprimer la même conversion sans code C++; préférer cette solution plus lisible lorsque les filtres suffisent.

Dans une lambda qui calcule une valeur, `if` permet de traiter des cas particuliers et `return` renvoie le résultat attendu par le composant. Comme les filtres modifient l'état publié, vérifier l'unité et l'échelle de la valeur lue.

## 146.3 Créer un capteur template

Un capteur template crée une nouvelle entité à partir d'une valeur calculée. Contrairement à un filtre, il ne remplace pas l'état publié par le capteur source : il publie un résultat distinct. L'exemple suivant suppose que `lecture_potentiometre` publie encore une tension en volts. Ne pas appliquer au capteur source les filtres précédents qui convertissent déjà cette tension en pourcentage.

Les capteurs numériques ESPHome publient des valeurs de type `float` (nombre décimal), pas des entiers. `accuracy_decimals` règle le nombre de décimales affichées, mais ne change pas le type de la valeur. Pour publier une valeur arrondie, utiliser un filtre comme `round`; elle reste un `float`.

`id(...).state` lit la dernière valeur publiée par un autre capteur ESPHome sur le même appareil. Par exemple, `id(lecture_potentiometre).state` lit l'état de cet identifiant.


```yaml
sensor:
  - platform: template
    name: "Potentiomètre en pourcentage"
    id: potentiometre_pourcentage
    unit_of_measurement: "%"
    accuracy_decimals: 0
    update_interval: 1s
    lambda: |-
      const float tension = id(lecture_potentiometre).state;
      const float minimum = 0.10f; // Remplacer par la tension minimale mesurée
      const float maximum = 3.00f; // Remplacer par la tension maximale mesurée
      if (isnan(tension)) return {};

      float pourcentage = (tension - minimum) * 100.0f / (maximum - minimum);
      if (pourcentage < 0.0f) pourcentage = 0.0f;
      if (pourcentage > 100.0f) pourcentage = 100.0f;
      return pourcentage;
```

`const float` déclare une valeur décimale qui ne sera pas modifiée. La formule ramène la plage mesurée à 0–100; les deux conditions empêchent de dépasser cette plage. Si la lecture n'est pas valide, `return {};` indique de ne pas publier de nouvelle valeur. Les accolades après `lambda: |-` permettent d'écrire le code sur plusieurs lignes; l'indentation YAML doit être respectée.

Un capteur de texte template peut publier une catégorie calculée depuis le pourcentage :

```yaml
text_sensor:
  - platform: template
    name: "Catégorie du potentiomètre"
    id: categorie_potentiometre
    update_interval: 1s
    lambda: |-
      const float pourcentage = id(potentiometre_pourcentage).state;
      if (isnan(pourcentage)) return {};
      if (pourcentage < 33.0f) return {"bas"};
      if (pourcentage < 67.0f) return {"moyen"};
      return {"élevé"};
```

Le capteur numérique et le capteur de texte sont deux nouvelles entités distinctes. Elles sont calculées sur l'ESP32 puis rendues disponibles dans Home Assistant.

## 146.4 Sortie template

Une sortie template est un composant intermédiaire qui reçoit une valeur puis exécute des actions. Contrairement à un capteur, une sortie n'est pas une entité affichée directement dans Home Assistant. Dans l'exemple ci-dessous, une lumière monochrome utilise la sortie template, qui transmet ensuite la moitié du niveau demandé à une sortie PWM physique :

```yaml
output:
  - platform: ledc
    id: sortie_del_pwm
    pin: GPIO5 # Remplacer par une broche compatible et libre

  - platform: template
    id: sortie_pwm_template
    type: float
    write_action:
      - output.set_level:
          id: sortie_del_pwm
          level: !lambda "return state * 0.5f;"

light:
  - platform: monochromatic
    name: "DEL limitée à mi-puissance"
    output: sortie_pwm_template
```

Quand la luminosité de la lumière change, la sortie template reçoit un niveau `state` entre 0 et 1 et l'action `output.set_level` applique la moitié de ce niveau à la sortie LEDC. La lumière paraît donc moins lumineuse que le niveau demandé dans Home Assistant. `type: float` indique que la sortie transmet une valeur décimale; pour un état marche/arrêt, le type serait `binary`. 


## Références

* [Filtres de capteurs ESPHome](https://esphome.io/components/sensor/#sensor-filters)
* [Capteur template ESPHome](https://esphome.io/components/sensor/template/)
* [Capteur de texte template ESPHome](https://esphome.io/components/text_sensor/template/)
* [Sortie template ESPHome](https://esphome.io/components/output/template/)
* [Lambdas ESPHome](https://esphome.io/automations/templates/)