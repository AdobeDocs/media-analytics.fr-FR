---
title: Mise en œuvre d’une requête events
description: null
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Mise en œuvre d’une requête events {#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilisez la [requête events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) pour tous les appels de suivi ultérieurs après avoir obtenu un ID de session à l’aide de la [requête sessions.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Spécifiez l’emplacement du curseur de lecture et l’horodatage, le type d’événement, ainsi que tous les paramètres facultatifs que vous souhaitez inclure, dans le corps JSON de la requête.

Le corps de requête JSON de la [requête events](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) présente la même structure que la requête sessions ; toutefois, vérifiez les [schémas de validation JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) pour connaître les conditions et les types de paramètre.
