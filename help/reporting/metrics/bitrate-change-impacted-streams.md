---
title: Flux impactés par le changement de débit
description: Comptabilise les sessions au cours desquelles au moins un changement de débit s’est produit.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 9%

---


# Flux impactés par le changement de débit

Le **changement de débit a eu un impact sur les flux** la mesure comptabilise les sessions au cours desquelles au moins un changement de débit s’est produit. La mesure est une valeur booléenne au niveau de la session : plusieurs modifications de débit au sein du même nombre de sessions qu’un flux concerné. Pour le volume total de changement de débit, utilisez [Changements de débit](/help/reporting/dimensions/bitrate-changes.md).

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true` la première fois qu’un événement `media.bitrateChange` est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bitrateChange` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
