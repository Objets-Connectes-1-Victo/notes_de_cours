# 84. Notification par courriel {#chapitre-notification_par_courriel}

## 84.1 Configurer Home Assistant pour l'envoi de courriel {#fiche-configurer_home_assistant_pour_l_envoi_de_courriel}

Home Assistant est capable d'envoyer du courriel à l'aide de l'intégration *SMTP*.

Par exemple, vous pouvez être averti par courriel lorsqu'une porte est ouverte entre minuit et 6h00.

Par contre, plusieurs fournisseurs de courriel (ex : GMail, Hotmail) ne permettent plus l'envoi de courriel par programmation (SMTP). Des services comme MailJet ou SendGrid permettent l'envoi de courriel par programmation, mais si vous n'avez pas de contrôle sur le domaine de votre courriel, vos courriels risquent d'être considérés comme du pourriel par les fournisseurs de courriel des destinataires.

Donc, 2 options s'offrent à vous :

1. Utiliser un domaine de courriel que vous possédez et créer une adresse de courriel pour Home Assistant
2. Utiliser un courriel d'un service de messagerie qui permet l'envoi de courriel par programmation


### Zoho Mail

Service de messagerie gratuit qui permet l'envoi de courriel par programmation (SMTP). Voici comment créez un compte pour l'utiliser avec Home Assistant : 

1. Allez sur le site de Zoho Mail : <https://www.zoho.com/mail/>
1. Cliquez sur le bouton *Sign Up Now*.
1. Choisissez l'option *Personal Email*.
1. Remplissez le formulaire pour créer un compte gratuit.
1. Utilisez votre vrai numéro de téléphone pour la vérification.
1. Prenez bien note de votre mot de passe et de votre nom d'utilisateur (adresse de courriel).
1. Les informations pour configurer la connexion SMTP sont affichées dans le menu *Comptes de courriel* / onglet *SMTP*

Voici les informations pour la configuration SMTP de Zoho Mail (sept. 2026) :

Serveur: smtp.zohocloud.ca
Port: 465
Protocole: SSL/TLS
Nom d'utilisateur: votre adresse de courriel complète
Mot de passe: le mot de passe que vous avez choisi pour votre compte Zoho Mail


### Configuration de Home Assistant pour l'envoi de courriel

1. Paramètres / Intégrations / Ajouter une intégration / SMTP
1. Remplissez les informations demandées (voir ci-dessus pour Zoho Mail)
1. Cliquez sur *Soumettre* pour terminer la configuration.
1. *Ajouter un destinataire* pour ajouter l'adresse de courriel du destinataire.
    1. Je vous conseille d'ajouter votre propre adresse de courriel (cegepvicto.ca) pour tester l'envoi de courriel.
    1. Vous pouvez ajouter plusieurs destinataires si vous le souhaitez.
1. Vous pouvez tester via Outils de développement / Actions / Choisir le service *Envoyer un message*
1. Choisissez une cible (le destinataire que vous avez ajouté)
1. Remplissez le titre et le message du courriel.

Vous pouvez ensuite utiliser l'action *Envoyer un message* dans vos automatisations pour envoyer un courriel à votre destinataire.

>Attention : même avec Zoho Mail, vos courriels risquent d'être considérés comme du pourriel par les fournisseurs de courriel. Vérifiez votre dossier pourriel si vous ne les recevez pas dans votre boîte de réception et marquez-les comme *Non pourriel* pour que les prochains courriels soient reçus dans la boîte de réception.


## Pour plus d'information

« SMTP ». Home Assistant. <https://www.home-assistant.io/integrations/smtp/>

## 84.2 Automatisation qui envoie un courriel {#fiche-automatisation_qui_envoie_un_courriel}

Pour qu'une automatisation envoie un courriel, dans la zone Alors faire , il faut choisir :  Autres actions / Effectuer une action.

Dans la liste déroulante des actions, choisissez celui dont le nom est « Send a notification » suivi du nom que vous avez donné à votre configuration YAML.

Notez que cette action ne sera pas présente si la configuration pour l'envoi de courriel n'est pas correcte ou si Home Assistant n'a pas été redémarré après sa création.

![Send a notification](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-SendANotification.png)

Renseignez ensuite les informations du courriel à envoyer.

Ce courriel sera envoyé automatiquement lorsque le déclencheur que vous avez configuré sera activé (ex : lorsque la porte sera ouverte).

![Automatisation qui envoie un courriel](NotesDeCoursApical-420_3a4_vi_objets_connectes_1_a_2025_files/HomeAssistant-AutomatisationEnvoieCourriel.png)

Si vous préférez travailler directement en YAML, le code du fichier automatisations.yaml ira comme suit :

Fichier automatisations.yaml


```
- id: '1606739413415'
alias: Porte ouverte envoie courriel
description: ''
trigger:
- trigger: state
entity_id:
- input_boolean.porte_virtuelle
from: 'off'
to: 'on'
conditions: []
actions:
- action: notify.courriel_administrateur
data:
message: La porte a été ouverte!
title: Porte ouverte
mode: single
```
