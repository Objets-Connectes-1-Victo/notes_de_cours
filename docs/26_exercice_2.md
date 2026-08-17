<a id="fiche-commencer_a_travailler_avec_jeedom"></a>
# 24. Exercice 2
<a id="chapitre-pour_le_prochain_cours_067"></a>

## 24.1 Commencer à travailler avec Jeedom

1. <a href="fiche-donner_une_adresse_ip_statique_au_raspberry_pi.md#donner_une_adresse_ip_statique_au_raspberry_pi">Donnez une adresse IP statique à votre Raspberry Pi</a> pour le réseau câblé seulement. Votre prof vous fournira l'adresse IP statique à utiliser.
2. Une fois le Raspberry Pi démarré, <a href="fiche-trouver_l_adresse_ip_du_raspberry_pi.md#trouver_l_adresse_ip_du_raspberry_pi">assurez-vous que son adresse IP</a> correspond à celle fournie par votre prof.
3. OPTIONNEL : <a href="fiche-configurer_le_reseau_wi-fi_sur_le_raspberry_pi.md#configurer_le_reseau_wi-fi_sur_le_raspberry_pi">Ajoutez une configuration réseau pour le Wi-Fi à votre maison</a>. Vous pouvez, à votre choix, utiliser une adresse IP statique ou non à la maison.
4. Ajustez votre boîte Jeedom afin qu'elle utilise le bon fuseau horaire (à vous de trouver comment). Si jamais, une fois le fuseau horaire configuré et Jeedom redémarré, la date et l'heure qui apparaissent dans le coin supérieur droit de l'écran ne sont pas corrects, <a href="fiche-Ajuster_la_date_et_l_heure_sous_Linux_Ubuntu.md#Ajuster_la_date_et_l_heure_sous_Linux_Ubuntu">ajustez-les manuellement sur le Raspberry Pi</a>.
5. Dans Jeedom, trouvez l'option de menu qui permet d'entrer  les coordonnées de l'endroit où se trouve votre système domotique (ex : votre domicile ou le cégep). Remplissez la latitude, la longitude ainsi que la section Adresse. Notez que vous n'aurez pas à modifier ces informations lorsque vous déplacerez votre Pi entre votre domicile et le Cégep.
6. Donnez votre nom à votre boîte Jeedom. Ce nom apparaîtra dans le coin supérieur droit de l'écran lors du prochain redémarrage de Jeedom. Cette configuration est essentielle pour faciliter le travail de votre prof lors de la correction des épreuve sommatives.
7. <a href="fiche-objets_pour_representer_la_maison.md#objets_pour_representer_la_maison">Ajoutez des objets pour représenter la maison et ses pièces</a>. En devoir, vous devez prendre des photos réelles de votre maison, de votre appartement *ou de tout autre endroit de votre choix* afin de les utiliser pour illustrer les objets.
8. <a href="fiche-configurer_la_cle_usb_z-wave_sur_jeedom.md#configurer_la_cle_usb_z-wave_sur_jeedom">Configurez votre clé Z-Wave</a>.
9. OPTIONNEL : Si vous utilisez une clé USB Z-Wave qui comporte un cercle lumineux, <a href="fiche-arreter_le_clignotement_des_del_sur_la_cle_usb_z-wave.md#arreter_le_clignotement_des_del_sur_la_cle_usb_z-wave">amusez-vous à arrêter et à redémarrer le clignotement de la clé</a>.
10. Effectuez une <a href="fiche-copie_de_securite_de_jeedom.md#copie_de_securite_de_jeedom">sauvegarde manuelle de Jeedom</a> et téléchargez-la sur votre poste de travail.
11. Sur votre seconde carte micro SD, <a href="fiche-copie_de_securite_de_jeedom.md#copie_de_securite_de_jeedom">restaurez le système à partir de la sauvegarde que vous venez de réaliser</a>.