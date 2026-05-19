---
title: Flux impactés par l’image perdue
description: Comptabilise les sessions dans lesquelles au moins une image a été supprimée.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%

---


# Flux impactés par l’image perdue

L’image **supprimée a eu un impact sur les flux** compte les sessions au cours desquelles au moins une image a été supprimée. La mesure est une valeur booléenne au niveau de la session : plusieurs abandons dans le même nombre de sessions qu’un flux affecté. Pour le volume de dépôt total, utilisez [Images perdues](dropped-frames.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur si la valeur `droppedFrames` de l’objet QoE est supérieure à zéro à la fermeture de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.droppedFrames` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
