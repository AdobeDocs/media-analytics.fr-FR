---
seo-title: Interruption du test 2 Media
title: Interruption du test 2 Media
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Test 2 : Interruption de médias{#test-media-interruption}

Ce script de test est requis dans le cadre du formulaire de demande de certification et valide le comportement de l’interruption mobile.

Download the certification request here: [Certification Request Form.](cert_req_form.docx)

Vous devez effectuer et enregistrer ces tâches dans l’ordre suivant :

1. **Démarrage du lecteur multimédia**

   Lorsque le lecteur multimédia démarre, les appels suivants sont envoyés dans l'ordre suivant :

   1. Démarrage de Media Analytics
   1. Démarrage de Heartbeat
   1. Démarrage de l’analyse Heartbeat
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md)

1. **Lire le média principal pendant au moins 5 minutes sans interruption**

   **Lecture du contenu**

   Lors de la lecture du contenu principal standard, des appels Heartbeat sont envoyés au serveur Heartbeat toutes les 10 secondes.

   Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Déplacer l’application ou le navigateur en arrière-plan**

   Lorsque l’application s’exécute en arrière-plan, seuls les appels main:pause doivent être envoyés au serveur Heartbeat, en commençant par VHL version 1.6.6 et ultérieures.

1. **Amener l’application ou le navigateur au premier plan**

   Au retour depuis l’arrière-plan, la lecture du contenu doit reprendre.

1. **Lire le média principal pendant au moins 5 minutes sans interruption**

   Pour les paramètres d'appel et les métadonnées, voir [Détails de l'appel de test.](/help/sdk-implement/validation/test-call-details.md)

1. **Fermer le lecteur multimédia**

   Aucun appel de suivi supplémentaire ne doit se déclencher après la fermeture du lecteur multimédia.

