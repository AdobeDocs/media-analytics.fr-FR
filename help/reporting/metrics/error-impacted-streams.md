---
title: Flux impactés par l’erreur
description: Comptabilise les sessions dans lesquelles au moins une erreur s’est produite.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 9%

---


# Flux impactés par l’erreur

La mesure **Erreur affectée par les flux** comptabilise les sessions dans lesquelles au moins une erreur s’est produite (`trackError` a été appelée ou un événement de `media.error` a été déclenché). La mesure est une valeur booléenne au niveau de la session : plusieurs erreurs dans le même nombre de sessions sont comptabilisées comme un flux affecté. Pour le volume total d’erreurs, utilisez [Erreurs](/help/reporting/dimensions/errors.md).

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.qoeDataDetails.hasErrorImpactedStreams = true` la première fois qu’un événement `media.error` est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.error` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
