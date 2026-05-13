---
title: Types et descriptions d’événements de streaming multimédia
description: 'Quels sont les types et descriptions d’événements Media Collection ? '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gqlCzqKd3F7N2-7WE727Ygl-4wheVjObgnx-ydLbgZk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 395
ht-degree: 79%

---

# Types et descriptions d’événement{#event-types-and-descriptions}

## sessionStart

Envoyé avec l’appel`sessions`. Lorsque la réponse est renvoyée, vous extrayez l’ID de session de l’en-tête Emplacement et l’utilisez pour les appels d’événement suivants vers le serveur Collection.

## play

Envoyé lorsque le lecteur passe à l’état « lecture » à partir d’un autre état (c’est-à-dire que le rappel `on('Playing')` est déclenché par le lecteur). Les autres états à partir desquels le lecteur passe à « lecture » incluent les suivants : mise en mémoire tampon, l’utilisateur a repris depuis l’état « interrompu », le lecteur a récupéré d’une erreur, lecture automatique, etc.

## ping

* **Contenu principal -** doit être envoyé toutes les 10 secondes pendant la lecture du contenu principal, indépendamment des autres événements API ayant été envoyés. Le premier événement ping doit se déclencher 10 secondes après le démarrage de la lecture du contenu principal.
* **Contenu de la publicité -** doit être envoyé toutes les secondes pendant le suivi publicitaire.

Les événements ping ne doivent *pas* inclure la carte `params` dans le corps de la requête.

## bitrateChange

Envoyé lorsque le débit binaire change.

## bufferStart

Envoyé au démarrage de la mise en mémoire tampon. Il n’existe aucun type d’événement `bufferResume`. Un `bufferResume` est déduit lorsque vous envoyez un événement `play` après un événement `bufferStart`.

## pauseStart

Envoyé lorsque l’utilisateur appuie sur Pause. Il n’existe aucun type d’événement `resume`. Un `resume` est déduit lorsque vous envoyez un événement `play` après un événement `pauseStart`.

## adBreakStart

Indique le début d’une coupure publicitaire.

## adStart

Indique le début d’une publicité.

## adComplete

Indique la fin d’une coupure publicitaire.

## adSkip

Indique qu’une publicité est ignorée.

## adBreakComplete

Indique la fin d’une coupure publicitaire.

## chapterStart

Indique le début d’un segment de chapitre.

## chapterSkip

Indique qu’un chapitre est ignoré.

## chapterComplete

Indique la fin d’un chapitre.

## error

Signale la survenue d’une erreur.

## sessionEnd

Permet d’indiquer au serveur principal Media Analytics de fermer immédiatement la session lorsque l’utilisateur a arrêté de regarder le contenu et ne reviendra probablement pas.

Si aucune `sessionEnd` n’est envoyée, une session abandonnée [expire normalement](../mc-api-impl/mc-api-timeout.md) (soit après qu’aucun événement n’a été reçu pendant 10 minutes, soit lorsqu’aucun mouvement du curseur de lecture ne se produit pendant 30 minutes). En outre, tous les appels multimédia suivants effectués avec cet ID de session seront ignorés.

## sessionComplete

Envoyé lorsque la fin du contenu principal est atteinte.

>[!IMPORTANT]
>
>Vous devez vous référer aux [schémas de validation JSON](mc-api-json-validation.md) pour chaque type d’événement afin de vérifier les types et les exigences de paramètre corrects.

## stateStart

Indique le début du suivi de l’état du lecteur.

Pour plus d’informations, voir [Implémentation et création de rapports](/help/use-cases/player-state-tracking/implementation-and-reporting.md).

## stateEnd

Indique la fin du suivi de l’état du lecteur.

Pour plus d’informations, voir [Implémentation et création de rapports](/help/use-cases/player-state-tracking/implementation-and-reporting.md).
