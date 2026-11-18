# 150. Bus I²C : principe, adresses et balayage ESPHome {#chapitre-bus_i2c_esphome}

## 150.1 Comprendre le bus I²C

I²C (« Inter-Integrated Circuit ») est un bus série synchrone qui permet à un microcontrôleur de communiquer avec plusieurs composants en utilisant deux lignes communes :

* **SDA** transporte les données;
* **SCL** fournit le signal d'horloge qui synchronise leur transfert.

L'ESP32-C3 joue le rôle de contrôleur : il initie les échanges. Les périphériques, comme un afficheur ou un capteur, sont raccordés aux mêmes lignes SDA et SCL. Les fils peuvent être distribués en parallèle ou d'un module au suivant. Tous les composants doivent partager une masse commune.

Les lignes I²C sont de type « collecteur ouvert » : les appareils peuvent ramener une ligne à l'état bas, mais ne la forcent pas à l'état haut. Des résistances de rappel (*pull-up*) ramènent donc SDA et SCL à l'état haut lorsqu'aucun appareil ne les maintient à l'état bas. Elles sont souvent déjà présentes sur les modules. Vérifier le montage avant d'en ajouter, et vérifier que les résistances ramènent les lignes à une tension compatible avec l'ESP32-C3.

!!! Attention
    Certains modules alimentés en 5 V peuvent aussi tirer SDA et SCL vers 5 V, ce qui n'est pas sécuritaire pour les entrées de l'ESP32-C3.

## 150.2 Adresses des périphériques

Quand le contrôleur veut communiquer avec un périphérique, il envoie une adresse sur SDA, synchronisée par SCL. Tous les périphériques du bus observent cette adresse, mais seul celui qui la reconnaît répond par un acquittement (*ACK*). Les données sont ensuite échangées; le bit de lecture ou d'écriture indique le sens de l'opération.

La plupart des configurations et des outils présentent l'adresse I²C sur 7 bits, en hexadécimal, par exemple `0x27` ou `0x3C`. Le bit de lecture/écriture (bit 8) fait partie du transfert sur le fil; il ne faut pas l'ajouter à l'adresse fournie à ESPHome.

Un appareil peut parfois offrir plusieurs adresses sélectionnables par des cavaliers (*jumpers*) ou des broches. Deux appareils ayant la même adresse sur un même bus peuvent entrer en conflit; il faut alors changer l'adresse d'un des modules, utiliser un multiplexeur I²C ou les placer sur des bus distincts.

Pour un LCD1602 équipé d'un adaptateur I²C PCF8574, les adresses courantes sont `0x27` et `0x3F`. Il s'agit de l'adresse de l'adaptateur, pas de l'écran à caractères lui-même. Ne pas choisir une adresse au hasard : vérifier celle détectée par le balayage et la documentation du module.

## 150.3 Balayer le bus au démarrage avec ESPHome

La section `i2c:` configure le bus et les broches. Avec `scan: true`, ESPHome recherche au démarrage les adresses qui répondent et inscrit celles trouvées dans les journaux. Le balayage est activé par défaut, mais le préciser rend l'intention claire :

```yaml
i2c:
  sda: GPIO6
  scl: GPIO7
  scan: true
```

Pour le XIAO ESP32-C3 utilisé dans le cours, le diagramme de brochage associe SDA à `GPIO6` et SCL à `GPIO7`. ESPHome permet de choisir d'autres broches compatibles, mais conserver ce câblage et cette configuration facilite le suivi du montage. Vérifier que GPIO6 et GPIO7 ne sont pas déjà utilisées par un autre composant. Si la configuration contient déjà une section `i2c:`, compléter celle-ci plutôt que d'en créer une deuxième.

Au démarrage, le scanner essaie des adresses sur le bus. Lorsqu'un périphérique répond, les journaux ESPHome affichent son adresse, par exemple `0x27`. Chaque module relié au bus peut apparaître avec sa propre adresse. Ces résultats permettent de vérifier qu'un appareil répond et de connaître l'adresse à configurer dans son composant ESPHome.

Le balayage n'identifie **pas** le type de périphérique et ne vérifie pas que son pilote, son écran ou son capteur fonctionne correctement. Il indique seulement qu'une adresse a répondu. L'absence d'adresse peut venir des broches, des fils, de l'alimentation, de la masse commune, des résistances de rappel, d'une incompatibilité de tension ou d'un module défectueux. Corriger le branchement, redémarrer l'appareil et consulter de nouveau les journaux.

## 150.4 Contrôler d'abord le LCD1602 depuis Home Assistant

Un LCD1602 est un écran à caractères de 16 colonnes × 2 lignes. Lorsqu'il est muni d'un adaptateur I²C PCF8574, il demande deux niveaux de configuration : la section `i2c:` pour le bus, puis la plateforme d'affichage. On commence par créer une entité texte ESPHome que Home Assistant peut modifier. L'écran affiche cette valeur; il n'est pas lui-même une entité de commande Home Assistant.

Dans cet exemple, le scanner a trouvé `0x27`. `text:` avec `platform: template` crée une entité texte virtuelle et modifiable depuis Home Assistant. On l'utilise pour recevoir le texte saisi dans Home Assistant et le transmettre à la lambda de l'écran. Ce n'est pas un texte lu depuis un capteur physique; `text_sensor:` sert plutôt à publier du texte en lecture seule vers Home Assistant.

```yaml
i2c:
  sda: GPIO6
  scl: GPIO7
  scan: true

text:
  - platform: template
    name: "Texte du LCD"
    id: texte_lcd
    mode: text
    optimistic: true
    max_length: 16
    initial_value: "Bonjour"

display:
  - platform: lcd_pcf8574
    dimensions: 16x2
    address: 0x27
    update_interval: 1s
    lambda: |-
      it.print(0, 0, id(texte_lcd).state.c_str());
      it.print(0, 1, "Controle par HA");
```

La plateforme `text.template` crée une entité de type texte dans Home Assistant. Dans cet exemple, `name` fournit son nom visible (« Texte du LCD »); Home Assistant génère son identifiant d'entité à partir du nom de l'appareil et de ce nom. La valeur exacte de l'identifiant est à vérifier dans Home Assistant.

| Clé ou section YAML | Visible comme entité dans Home Assistant? | Rôle |
| --- | --- | --- |
| `text:` avec `platform: template` et `name` | Oui, comme entité texte « Texte du LCD » | Permet à Home Assistant de modifier le texte |
| `id: texte_lcd` | Non | Identifiant interne utilisé dans les lambdas ESPHome |
| `mode`, `optimistic`, `max_length`, `initial_value` | Non | Options de configuration de l'entité texte |
| `i2c:` et `display:` | Non | Configurent le bus et l'affichage physique; le LCD n'est pas lui-même une entité Home Assistant |

`optimistic: true` permet à ESPHome de prendre immédiatement la valeur saisie comme nouvel état. La longueur maximale de 16 caractères correspond à une ligne du LCD1602. Après avoir installé la configuration et ajouté l'entité à une carte de type **Entité** ou **Texte** dans Home Assistant, modifier le texte et vérifier qu'il apparaît à l'écran.

Dans la lambda d'affichage, `it` représente l'écran; ses méthodes permettent d'y écrire. `it.print` écrit du texte. La lambda est exécutée à chaque rafraîchissement, ici chaque seconde. Le contenu affiché est rendu par ESPHome sur l'appareil : Home Assistant commande le texte via l'entité, plutôt que de communiquer directement avec le LCD.

Dans `id(texte_lcd).state.c_str()`, `id(texte_lcd)` désigne l'entité texte déclarée plus haut et `.state` lit sa valeur courante. Cette valeur est une chaîne de caractères C++; `.c_str()` en fournit une représentation terminée par le caractère nul, que `it.print` peut recevoir pour afficher le texte.

## 150.5 Ajouter ensuite une mesure au LCD

Une fois la commande du texte vérifiée, remplacer le bloc `display:` par cette version complète. Elle conserve le texte contrôlé par Home Assistant sur la première ligne et affiche la température ambiante sur la deuxième. Les sections `i2c:` et `text:` précédentes sont conservées. L'identifiant `temperature_ambiante` doit correspondre à celui du capteur déjà configuré :

```yaml
display:
  - platform: lcd_pcf8574
    dimensions: 16x2
    address: 0x27
    update_interval: 1s
    lambda: |-
      it.print(0, 0, id(texte_lcd).state.c_str());
      if (isnan(id(temperature_ambiante).state)) {
        it.print(0, 1, "Temp: --.- C");
      } else {
        it.printf(0, 1, "Temp: %.1f C", id(temperature_ambiante).state);
      }
```

Si le scanner trouve `0x3F` plutôt que `0x27`, utiliser `address: 0x3F`. Remplacer aussi l'identifiant du capteur par celui de la configuration. Les LCD à caractères ont un jeu de caractères limité; les accents peuvent ne pas être disponibles.

Cette configuration concerne seulement un LCD à caractères avec un adaptateur PCF8574. Un écran graphique I²C, un écran relié directement en parallèle ou un module utilisant un autre circuit demande une autre plateforme, un autre câblage et parfois une configuration différente. Lire le marquage du module et sa documentation avant de reprendre l'exemple. Certains écrans alimentés en 5 V nécessitent aussi une vérification attentive de la tension logique et des résistances de rappel.

!!! warning

    Couper l'alimentation avant de modifier le câblage. Ne jamais appliquer 5 V à une entrée du XIAO ESP32-C3. Confirmer que SDA et SCL ne peuvent pas être tirées à 5 V par l'afficheur ou son adaptateur.

## Références

* [Bus I²C ESPHome](https://esphome.io/components/i2c/)
* [Écrans LCD à caractères ESPHome](https://esphome.io/components/display/lcd_display/)
* [Texte template ESPHome](https://esphome.io/components/text/template/)
* [Brochage du XIAO ESP32-C3 (Seeed Studio)](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)
