---
title: Schémas de validation JSON des services de streaming multimédia
description: Que sont les schémas de validation JSON de streaming multimédia et comment sont-ils utilisés pour déterminer les paramètres corrects du corps de la requête pour chaque type d’événement ?
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ZWKv1LJKc8qLkZYpcNdDFEs8Er70toRCoufarMcgVKQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 84
ht-degree: 71%

---

# Schémas de validation JSON{#json-validation-schemas}

Le serveur principal Collection de médias en flux continu valide les paramètres de requête pour chaque type d’événement à l’aide de schémas de validation JSON. Ces schémas sont à votre disposition et constituent l’autorité actuelle concernant les types de paramètre utilisés dans l’API MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Pour plus d’informations sur l’utilisation des schémas de validation JSON, reportez-vous à la rubrique [Validation des requêtes d’événement.](../mc-api-impl/mc-api-validate-reqs.md)
