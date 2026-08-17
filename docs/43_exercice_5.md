<a id="fiche-explorer_jeedom_plus_en_profondeur"></a>
# 39. Exercice 5
<a id="chapitre-pour_le_prochain_cours_040"></a>

## 39.1 Explorer Jeedom plus en profondeur

Dans cet exercice, vous êtes appelés à explorer Jeedom : ses fichiers, sa base de données, ses logs. Après tout, vous êtes des développeurs, pas de simples utilisateurs!

1. Modifiez votre scénario dans lequel le capteur de votre choix agit sur le récepteur de votre choix. En plus d'agir sur le récepteur et de vous envoyer un courriel, il doit <a href="fiche-scenario_qui_ajoute_une_entree_dans_le_fichier_journal.md#scenario_qui_ajoute_une_entree_dans_le_fichier_journal">inscrire dans un fichier journal</a> nommé meslogs le texte « Mon premier scénario a été exécuté! ». Pour l'instant, utilisez le <a href="fiche-scenario_qui_ajoute_une_entree_dans_le_fichier_journal.md#scenario_qui_ajoute_une_entree_dans_le_fichier_journal">niveau de gravité</a> ERROR.
2. Une fois l'écriture dans le log fonctionnelle, modifiez le scénario pour que l'inscription utilise le niveau de gravité WARNING. Pour que l'information s'enregistre dans le journal, vous devrez modifier le <a href="fiche-configurer_les_fichiers_journaux.md#configurer_les_fichiers_journaux">niveau de log par défaut</a>.
3. Perfectionnez le scénario pour qu'il inscrive également dans le log le nom du capteur qui l'a déclenché, retrouvé par programmation (chaîne au format #[Cuisine][Porte][État]#).
4. On veut également inscrire dans le log la valeur du déclencheur, retrouvée par programmation. Dans le cas où le scénario est lancé manuellement en cliquant sur le bouton Exécuter dans l'écran d'édition du scénario, on voudra plutôt inscrire dans le log les mots "Déclenchement manuel". Vous aurez donc un if à ajouter dans le bloc de code.
5. Faites une impression d'écran de l'onglet Scénario qui montre les ajouts que vous avez faits. L'impression d'écran doit montrer clairement le nom de la boîte Jeedom qui apparaît dans le coin supérieur droit de l'écran. Nommez votre fichier au format nomprenom-scenario-journal.png.
6. Sur votre Raspberry Pi, <a href="fiche-reinitialiser_le_mot_de_passe_mysql_de_jeedom.md#reinitialiser_le_mot_de_passe_mysql_de_jeedom">modifiez votre mot de passe MySQL</a> pour que ce soit tata.
7. Dans la <a href="fiche-contenu_de_la_base_de_donnees_de_jeedom.md#contenu_de_la_base_de_donnees_de_jeedom">base de données Jeedom</a>, retrouvez l'enregistrement exact où il est dit que votre scénario doit écrire dans le fichier meslogs. Faites une impression d'écran qui montre le SELECT qui vous donne l'information recherchée. Nommez votre fichier au format nomprenom-select-journal.png.
8. <a href="fiche-copie_de_securite_de_jeedom.md#copie_de_securite_de_jeedom">Lancez une sauvegarde de Jeedom manuellement</a>.
9. OPTIONNEL : <a href="fiche-copier_automatiquement_le_fichier_de_sauvegarde_sur_votre_ordinateur.md#copier_automatiquement_le_fichier_de_sauvegarde_sur_votre_ordinateur">Écrivez un fichier bash</a> qui permet de copier sur votre ordinateur un fichier de sauvegarde de Jeedom et configurez votre ordinateur pour qu'il soit lancé automatiquement environ 30 minutes après le moment où Jeedom a fait sa sauvegarde.
   1. Laissez votre système Jeedom branché toute la nuit et constatez le lendemain si le fichier de sauvegarde a correctement été copié sur votre ordinateur.
10. Remettez sur la plateforme électronique du cours vos deux impressions d'écran de même que votre fichier bash (si vous avez fait ce dernier).