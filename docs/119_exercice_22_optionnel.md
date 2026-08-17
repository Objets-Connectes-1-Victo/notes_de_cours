# 105. Exercice 22 - OPTIONNEL {#chapitre-exercice_22_optionnel}

## 105.1 La guerre des notes! {#fiche-la_guerre_des_notes}

CET EXERCICE EST OPTIONNEL.

Sur le Jeedom de votre professeur, un équipement virtuel porte un nom au format eleve9 où 9 est le numéro de votre Raspberry Pi par exemple eleve1, ..., eleve 10, etc. Cet équipement contient une commande nommée note. Votre professeur vous fournira l'id de la commande ainsi que la clé d'API.

1. À partir de votre Home Assistant, entrez dans cette commande la note que vous désirez obtenir pour le cours d'objets connectés. La note doit être un chiffre entre 0 et 100.
2. À partir de votre Home Assistant, créez une automatisation qui vous envoie un courriel (ou une notification, ou une écriture dans un fichier journal) dès qu'un collègue de votre choix entre une note inférieure à 60 dans son objet sur Jeedom.
3. À partir de votre Home Assistant, créez une automatisation qui augmente votre note dès qu'un collègue de votre choix entre une note supérieure à la vôtre dans son objet sur Jeedom. Votre note sera 1 de plus que la sienne. Les notes sont plafonnées à 100.