<a id="fiche-combat_des_pouces_mqtt"></a>
# 110. Exercice 24
<a id="chapitre-pour_le_prochain_cours_054"></a>

## 110.1 Combat des pouces MQTT

Dans cet exercice, vous devez travailler deux par deux. Chaque membre de l'équipe aura sa propre boîte Home Assistant.

Important : un abonnement à un canal MQTT doit absolument être réalisé à l'aide d'une entrée dans le fichier configuation.yaml.  
  
 L'écran que l'on obtient par Paramètres / Appareils et services / onglet Intégrations / Tuile du client MQTT / Icône d'engrenage ne permet que d'effectuer des tests. L'écoute configurée dans cet écran est temporaire. Elle ne sera plus effective lors du redémarrage de Home Assistant.

1. Vous devez faire quelques tests avec l'agent test.mosquitto.org.
   1. Configurez les deux boîtes pour utiliser l'agent MQTT test.mosquitto.org.
   2. Faites un test MQTT pour faire transiger des données entre les deux boîtes. La première boîte enverra « Hello » et la seconde, « World! ».
   3. Afin de vérifier ce qui transige sur l'agent test.mosquitto.org, testez les données qui transigent sur le canal #. Arrêtez d'écouter dès que vous serez convaincus du nombre important de données qui transigent sur cet agent.
2. Vous devez maintenant débuter le combat des pouces. Suivez bien les étapes demandées. À la fin, chaque boîte aura un bouton pour modifier un compteur et chacune aura une carte qui affiche la valeur du compteur.
   1. Si vous le désirez, configurez les deux boîtes pour utiliser un autre agent MQTT.
   2. Choisissez le format du canal MQTT que vous utiliserez afin de ne pas entrer en conflit avec les autres communications MQTT qui se déroulent sur cet agent.
   3. Sur une seule boîte Home Assistant, que l'on appellera boîte A, créez une entrée de type compteur. Elle pourra prendre une valeur entre 0 et 20 avec une valeur initiale de 10. Cette variable simulera un combat de pouces.
   4. Toujours sur la boîte A, ajoutez une carte de type bouton. Un clic sur ce bouton fera une pause de 2 secondes puis s'occupera d'**incrémenter** le compteur.
   5. Sur l'autre boîte, que l'on appellera boîte B, ajoutez une carte de type bouton. Un clic sur ce bouton s'occupera d'envoyer un message MQTT qui demande de décrémenter le compteur (c'est la boîte A qui fera le travail de décrémentation, suivez les étapes!).
   6. Faites le nécessaire pour que la boîte A soit abonnée au canal MQTT utilisé par la boîte B.
   7. Sur la boîte A, ajoutez une automatisation qui se charge de **décrémenter** le compteur (sans pause) dès qu'elle reçoit un message MQTT à cet effet.
   8. Dès que le compteur change de valeur, la boîte A doit envoyer sa valeur sur un autre canal MQTT.
   9. La boîte B doit être abonnée à ce canal et afficher sur son tableau de bord la valeur reçue.
   10. Testez l'effet des deux boutons sur la valeur du compteur. Au besoin, ajustez le délai avant l'incrémentation afin que les deux boîtes aient une chance égale.
   11. Quand le compteur atteint la valeur 20, c'est le joueur de la boîte A qui gagne. Quand il atteint la valeur 0, c'est le joueur de la boîte B qui gagne.
   12. La boîte du joueur qui gagne enverra automatiquement une notification à son application mobile (ou une notification persistante : persistent\_notification.create) pour dire qu'il a gagné.