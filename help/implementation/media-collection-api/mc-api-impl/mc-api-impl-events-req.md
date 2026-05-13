---
title: Mise en œuvre d’une requête events
description: Découvrez comment utiliser le point d’entrée de requêtes Events pour tous les appels de suivi ultérieurs à l’obtention d’un ID de session
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/xJntEcDm5sCGoCeuCjl9x51EOaYcOO2FzFAtK8mbt38
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 99
ht-degree: 56%

---

# Mise en œuvre d’une requête events{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Utilisez la [requête Events](../mc-api-ref/mc-api-events-req.md) pour tous les appels de suivi suivants après avoir obtenu un ID de session à l’aide de la [requête Sessions](../mc-api-ref/mc-api-sessions-req.md). Spécifiez l’emplacement et l’horodatage du curseur de lecture, le type d’événement et les paramètres facultatifs que vous souhaitez inclure dans le corps JSON de la requête.

Le corps de requête JSON de la [requête events](../mc-api-ref/mc-api-events-req.md) présente la même structure que la requête sessions ; toutefois, vérifiez les [schémas de validation JSON](../mc-api-ref/mc-api-json-validation.md) pour connaître les conditions et les types de paramètre.
