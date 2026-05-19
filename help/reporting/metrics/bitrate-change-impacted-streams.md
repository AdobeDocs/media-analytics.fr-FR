---
title: Flux impactés par le changement de débit
description: Comptabilise les sessions au cours desquelles au moins un changement de débit s’est produit.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 10%

---


# Flux impactés par le changement de débit

Le **changement de débit a eu un impact sur les flux** la mesure comptabilise les sessions au cours desquelles au moins un changement de débit s’est produit. La mesure est une valeur booléenne au niveau de la session : plusieurs modifications de débit au sein du même nombre de sessions qu’un flux concerné. Pour le volume total de changement de débit, utilisez [Changements de débit](/help/reporting/dimensions/bitrate-changes.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement [changement de débit](/help/implementation/events/playback/bitrate-change.md) est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bitrateChange` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
