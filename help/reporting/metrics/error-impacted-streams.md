---
title: Flux impactés par l’erreur
description: Comptabilise les sessions dans lesquelles au moins une erreur s’est produite.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# Flux impactés par l’erreur

La mesure **Erreur impactée par les flux** comptabilise les sessions dans lesquelles au moins une erreur s’est produite (`trackError` a été appelée ou un événement [erreur](/help/implementation/events/error.md) a été déclenché). La mesure est une valeur booléenne au niveau de la session : plusieurs erreurs dans le même nombre de sessions sont comptabilisées comme un flux affecté. Pour le volume total d’erreurs, utilisez [Erreurs](/help/reporting/dimensions/errors.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement [error](/help/implementation/events/error.md) est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.error` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
