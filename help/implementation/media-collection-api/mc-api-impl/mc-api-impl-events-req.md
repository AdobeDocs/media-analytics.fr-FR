---
title: Mise en œuvre d’une requête events
description: Découvrez comment utiliser le point d’entrée de requêtes Events pour tous les appels de suivi ultérieurs à l’obtention d’un ID de session
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 100%

---

# Mise en œuvre d’une requête events {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilisez la [requête events](../mc-api-ref/mc-api-events-req.md) pour tous les appels de suivi ultérieurs après avoir obtenu un ID de session à l’aide de la [requête sessions.](../mc-api-ref/mc-api-sessions-req.md) Spécifiez l’emplacement du curseur de lecture et l’horodatage, le type d’événement, ainsi que tous les paramètres facultatifs que vous souhaitez inclure, dans le corps JSON de la requête.

Le corps de requête JSON de la [requête events](../mc-api-ref/mc-api-events-req.md) présente la même structure que la requête sessions ; toutefois, vérifiez les [schémas de validation JSON](../mc-api-ref/mc-api-json-validation.md) pour connaître les conditions et les types de paramètre.
