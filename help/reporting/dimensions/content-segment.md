---
title: Segment de contenu
description: Indique la plage de têtes de lecture vue au cours d’une session, en minutes.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---


# Segment de contenu

La dimension **Segment de contenu** indique la plage de têtes de lecture vue au cours d’une session, en minutes (par exemple, `[0-5]` pendant les minutes 0 à 5). Le serveur principal calcule le segment à partir des valeurs minimale et maximale de la tête de lecture signalées lors de la lecture. Utilisez-le avec la mesure [Vues de segments de contenu](/help/reporting/metrics/content-segment-views.md) pour analyser les parties consommées par les visionneuses de contenu de forme longue.

## Mode de remplissage de cette dimension

Le segment de contenu est calculé par le serveur principal du média à partir des valeurs du curseur de lecture rapportées dans les événements de la session. Il n’est pas défini par le client. La valeur signalée est dérivée des valeurs du curseur de lecture affichées pendant la lecture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.segment` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videosegment, post_videosegment` |

>[!IMPORTANT]
>
>Si le curseur de lecture n’est pas signalé correctement pendant la session, le segment calculé peut être inexact. Pour les flux en direct, le segment est calculé à partir des valeurs relatives du curseur de lecture affichées au cours de la session.

## Éléments de dimension

Chaque élément est une plage de chaînes couvrant les valeurs du curseur de lecture affichées au cours d’une session (par exemple, `[0-5]`, `[5-10]`, `[10-15]`). La granularité est fixée à cinq minutes.
