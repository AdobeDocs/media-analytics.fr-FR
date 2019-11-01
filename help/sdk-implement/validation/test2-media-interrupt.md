---
title: Test 2 Interruption du média
description: Cette rubrique décrit le test d’interruption de média utilisé dans la validation.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Test 2 : Interruption du média{#test-media-interruption}

Ce cas de test valide le comportement d’interruption de téléphonie mobile. Il s’agit d’un élément obligatoire de votre demande de certification.

## Formulaire de demande de certification

**Téléchargez le formulaire de demande de certification ici : ==&gt;** Formulaire de demande de [certification.](cert_req_form.docx)

## Procédure d'essai

Vous devez effectuer et enregistrer ces tâches dans l’ordre suivant :

1. **Démarrage du lecteur multimédia**

   Lorsque le lecteur multimédia démarre, les appels suivants sont envoyés dans l’ordre suivant :

   1. Démarrage d’Adobe Analytics (AppMeasurement)
   1. Media Analytics (pulsations) Start
   1. Appel Adobe Analytics Start demandé pour Media Analytics (pulsations)
   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   Le troisième appel ci-dessus indique au serveur Media Analytics que le SDK Media a demandé que l’appel Adobe Analytics Start (`pev2=ms_s`) soit envoyé au serveur Adobe Analytics.

1. **Lire le contenu principal pendant au moins 5 minutes sans interruption**

   **Lecture du contenu**

   Pendant la lecture du contenu, le SDK multimédia envoie des appels de lecture (pulsations) au serveur Media Analytics toutes les dix secondes.

   Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **Déplacer l’application ou le navigateur en arrière-plan**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **Ramener l’application ou le navigateur au premier plan**

   Au retour depuis l’arrière-plan, la lecture du contenu doit reprendre.

1. **Lire le média de contenu principal pendant au moins 5 minutes sans interruption**

   Pour plus d’informations sur les paramètres d’appel et les métadonnées, voir Détails de l’appel de [test.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **Fermer le lecteur multimédia**

   Aucun appel de suivi supplémentaire ne doit se déclencher une fois le lecteur multimédia fermé.

