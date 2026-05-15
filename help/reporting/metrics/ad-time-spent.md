---
title: Temps passé sur la publicité
description: Indique le nombre total de secondes de lecture de publicité active par session.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 9%

---


# Temps passé sur la publicité

La mesure **Temps passé sur l’annonce publicitaire** indique le nombre total de secondes de lecture active de l’annonce publicitaire par session, à l’exclusion des pauses, de la mise en mémoire tampon et des blocages. Associez-le à [&#x200B; Temps passé sur le contenu &#x200B;](/help/reporting/metrics/content-time-spent.md) pour comparer la charge publicitaire à l’engagement sur le contenu.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps d’horloge murale écoulé entre les événements pendant que le lecteur est à l’état `play` sur une publicité. Le temps pendant les pauses et la mise en mémoire tampon est exclu. La mesure est signalée lors de l’appel de fermeture de la publicité. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les flux de données, Data Warehouse et les API de création de rapports.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.timePlayed` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
