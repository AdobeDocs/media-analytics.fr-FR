---
title: Temps passé sur le média
description: Indique le nombre total de secondes de lecture active par session, publicités comprises.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 7%

---


# Temps passé sur le média

La mesure **Temps passé sur le média** indique le nombre total de secondes de lecture active par session, y compris le contenu principal et les publicités, mais sans les pauses, la mise en mémoire tampon et les blocages. Utilisez-la pour mesurer le temps total pendant lequel la visionneuse a été activement engagée avec le lecteur. Pour le contenu principal uniquement, utilisez [&#x200B; Temps passé sur le contenu &#x200B;](content-time-spent.md).

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps d’horloge murale écoulé entre les événements pendant que le lecteur est à l’état `play`, sur le contenu principal ou les publicités. Le temps pendant les pauses, les événements de mise en mémoire tampon et les blocages est exclu. La mesure est signalée lors de l’appel de fermeture. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les flux de données, Data Warehouse et les API de création de rapports.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.totalTimePlayed` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
