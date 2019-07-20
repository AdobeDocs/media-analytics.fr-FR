---
seo-title: Interruption de la vidéo Test 2
title: Interruption de la vidéo Test 2
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Test 2 : Interruption vidéo{#test-video-interruption}

Ce script de test est requis dans le cadre du formulaire de demande de certification et valide le comportement de l’interruption mobile.

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

Vous devez effectuer et enregistrer ces tâches dans l’ordre suivant :

1. **Démarrer le lecteur vidéo**

   Au démarrage du lecteur vidéo, les appels ci-dessous sont envoyés dans l’ordre suivant :

   1. Démarrage de Media Analytics
   1. Démarrage de Heartbeat
   1. Démarrage de l’analyse Heartbeat
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **Lire la vidéo de contenu principal pendant au moins 5 minutes sans interruption**

   **Lecture du contenu**

   Lors de la lecture du contenu principal standard, des appels Heartbeat sont envoyés au serveur Heartbeat toutes les 10 secondes.

   For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](../../sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Déplacer l’application ou le navigateur en arrière-plan**

   Lorsque l’application s’exécute en arrière-plan, seuls les appels main:pause doivent être envoyés au serveur Heartbeat, en commençant par VHL version 1.6.6 et ultérieures.

1. **Amener l’application ou le navigateur au premier plan**

   Au retour depuis l’arrière-plan, la lecture du contenu doit reprendre.

1. **Lire la vidéo de contenu principal pendant au moins 5 minutes sans interruption**

   For call parameters and metadata, see [Test Call Details.](../../sdk-implement/validation/test-call-details.md)

1. **Fermer le lecteur vidéo**

   Aucun autre appel de suivi ne doit être déclenché après la fermeture du lecteur vidéo.

