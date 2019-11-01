---
title: Types et descriptions d’événement
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Types et descriptions d’événement{#event-types-and-descriptions}

## sessionStart

Envoyé avec l' `sessions` appel. Lorsque la réponse est renvoyée, vous extrayez l’ID de session de l’en-tête Emplacement et l’utilisez pour les appels d’événement suivants vers le serveur Collection.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). Les autres états à partir desquels le lecteur passe à « lecture » incluent les suivants : mise en mémoire tampon, l’utilisateur a repris depuis l’état « interrompu », le lecteur a récupéré d’une erreur, lecture automatique, etc.

## ping

* **Contenu principal** : Doit être envoyé toutes les 10 secondes pendant la lecture du contenu principal, indépendamment des autres événements API ayant été envoyés. Le premier événement ping doit se déclencher 10 secondes après le démarrage de la lecture du contenu principal.
* **Contenu de la publicité** : Doit être envoyé toutes les secondes pendant le suivi publicitaire.

Les événements ping ne doivent *pas* inclure la carte `params` dans le corps de la requête.

## bitrateChange

Envoyé lorsque le biage change.

## bufferStart

Envoyé au démarrage de la mise en mémoire tampon. Il n’existe aucun type d’événement `bufferResume`. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

Envoyé lorsque l’utilisateur appuie sur Pause. Il n’existe aucun type d’événement `resume`. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

Signale le début d’une coupure publicitaire

## adStart

Indique le début d’une publicité

## adComplete

Signale la fin d’une coupure publicitaire

## adSkip

Signale un saut de publicité

## adBreakComplete

Signale la fin d’une coupure publicitaire

## chapterStart

Signale le début d’un segment de chapitre

## chapterSkip

Signale un saut de chapitre

## chapterComplete

Signale la fin d’un chapitre

## error

Signale une erreur.

## sessionEnd

Elle permet d’avertir le serveur principal d’Analytics de la fermeture immédiate de la session lorsque l’utilisateur a abandonné l’affichage du contenu et qu’il est peu probable qu’il y retourne.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

Envoyé lorsque la fin du contenu principal est atteinte

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

