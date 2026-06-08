---
title: Flux impactés par la mémoire tampon
description: Comptabilise les sessions dans lesquelles le lecteur est entré en état de mémoire tampon au moins une fois.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

---


# Flux impactés par la mémoire tampon

La mesure **Flux impactés par la mémoire tampon** comptabilise les sessions dans lesquelles le lecteur est entré en état de mémoire tampon au moins une fois. La mesure est une valeur booléenne au niveau de la session ; plusieurs événements de mémoire tampon dans la même session comptent comme un flux impacté. Pour le volume total de tampon, utilisez [Événements de tampon](buffer-events.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement [début de la mémoire tampon](/help/implementation/events/playback/buffer-start.md) est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.buffer` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/setup/analytics-reporting.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
