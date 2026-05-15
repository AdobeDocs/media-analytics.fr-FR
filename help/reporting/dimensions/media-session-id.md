---
title: ID de session multimédia
description: Identifie de manière unique chaque session de lecture.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# ID de session multimédia

La dimension **ID de session multimédia** identifie de manière unique chaque session de lecture. Elle est générée par le serveur principal et marquée sur chaque événement de la session. Utilisez-la pour isoler les événements d’une seule session à des fins de débogage ou pour dédupliquer les sessions dans des analyses personnalisées.

## Mode de remplissage de cette dimension

L’ID de session est généré automatiquement lorsque le serveur principal reçoit un événement [début de session](/help/implementation/events/session/session-start.md). Les implémentations de Web SDK et de Mobile SDK capturent et conservent l’ID pour vous ; les implémentations d’API directes doivent lire l’ID de session à partir de la réponse `sessionStart` (l’en-tête `Location` pour l’API Media Collection ou l’identificateur `media-analytics:new-session` pour l’API Media Edge) et l’inclure dans les événements suivants.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.vsid` à un eVar. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## Éléments de dimension

Chaque élément est un ID de session unique généré par le serveur principal (généralement une chaîne alphanumérique de 22 caractères). Utilisez le champ Filtrer ou Rechercher pour rechercher une session spécifique.
