---
seo-title: Interruption du test 2 Media
title: Interruption du test 2 Media
uuid: eeccd 534-63 fd -4 dd 3-b 096-0431 bc 9 a 11 ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# Test 2 : Interruption de médias{#test-media-interruption}

Ce cas de test valide le comportement d'arrêt mobile. Il s'agit d'un élément obligatoire de votre demande de certification.

## Formulaire de demande de certification

**Téléchargez le formulaire de demande de certification ici : = = &gt;**  [Formulaire de demande de certification.](cert_req_form.docx)

## Procédure de test

Vous devez effectuer et enregistrer ces tâches dans l’ordre suivant :

1. **Démarrage du lecteur multimédia**

   Lorsque le lecteur multimédia démarre, les appels suivants sont envoyés dans l'ordre suivant :

   1. Adobe Analytics (appmeasurement) Start
   1. Démarrage des médias Analytics (pulsations)
   1. Appel d'Adobe Analytics Start (pulsations) Demande de démarrage d'Adobe Analytics
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Le troisième appel ci-dessus indique au serveur Media Analytics que le kit de développement multimédia demande que l'appel Adobe Analytics Start (`pev2=ms_s`) soit envoyé au serveur Adobe Analytics.

1. **Lire le contenu principal pendant au moins 5 minutes sans interruption**

   **Lecture du contenu**

   Lors de la lecture du contenu, le kit de développement multimédia envoie les appels play (pulsations) au serveur Media Analytics toutes les dix secondes.

   Pour les paramètres d'appel et les métadonnées, voir [Test des détails de l'appel.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Déplacer l’application ou le navigateur en arrière-plan**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **Rétablissement de l'application ou du navigateur au premier plan**

   Au retour depuis l’arrière-plan, la lecture du contenu doit reprendre.

1. **Lire le média principal pendant au moins 5 minutes sans interruption**

   Pour les paramètres d'appel et les métadonnées, voir [Détails de l'appel de test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Fermer le lecteur multimédia**

   Aucun appel de suivi supplémentaire ne doit se déclencher après la fermeture du lecteur multimédia.

