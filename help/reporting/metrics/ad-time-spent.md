---
title: Temps passé sur la publicité
description: Indique le nombre total de secondes de lecture de publicité active par session.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%

---


# Temps passé sur la publicité

La mesure **Temps passé sur l’annonce publicitaire** indique le nombre total de secondes de lecture active de l’annonce publicitaire par session, à l’exclusion des pauses, de la mise en mémoire tampon et des blocages. Associez-le à [ Temps passé sur le contenu ](/help/reporting/metrics/content-time-spent.md) pour comparer la charge publicitaire à l’engagement sur le contenu.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps d’horloge murale écoulé entre les événements pendant que le lecteur est à l’état `play` sur une publicité. Le temps pendant les pauses, la mise en mémoire tampon et les recherches est exclu, conformément à la manière dont le [temps passé sur le contenu](/help/reporting/metrics/content-time-spent.md) est calculé pour le contenu principal. La mesure est signalée lors de l’appel de fermeture de la publicité. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les flux de données, Data Warehouse et les API de création de rapports.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.timePlayed` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
