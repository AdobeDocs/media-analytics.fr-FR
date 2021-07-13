---
title: Mise en œuvre d’une requête events
description: Découvrez comment utiliser le point de terminaison de requête events pour tous les appels de suivi suivants après avoir obtenu un ID de session
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 81%

---

# Mise en œuvre d’une requête events{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilisez la [requête events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) pour tous les appels de suivi ultérieurs après avoir obtenu un ID de session à l’aide de la [requête sessions.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Spécifiez l’emplacement du curseur de lecture et l’horodatage, le type d’événement, ainsi que tous les paramètres facultatifs que vous souhaitez inclure, dans le corps JSON de la requête.

Le corps de requête JSON de la [requête events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) présente la même structure que la requête sessions ; toutefois, vérifiez les [schémas de validation JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) pour connaître les conditions et les types de paramètre.
