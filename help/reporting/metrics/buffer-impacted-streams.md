---
title: Flux impactés par la mémoire tampon
description: Comptabilise les sessions dans lesquelles le lecteur est entré en état de mémoire tampon au moins une fois.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

---


# Flux impactés par la mémoire tampon

La mesure **Flux impactés par la mémoire tampon** comptabilise les sessions dans lesquelles le lecteur est entré en état de mémoire tampon au moins une fois. La mesure est une valeur booléenne au niveau de la session : plusieurs événements de mémoire tampon dans le même nombre de sessions qu’un flux affecté. Pour le volume total de tampon, utilisez [Événements de tampon](buffer-events.md).

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.qoeDataDetails.hasBufferImpactedStreams = true` la première fois qu’un événement `media.bufferStart` est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.buffer` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
