---
title: Durée du contenu
description: Indique le nombre total de secondes de lecture du contenu principal actif par session.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 7%

---


# Durée du contenu

La mesure **Temps passé sur le contenu** indique le nombre total de secondes de lecture du contenu principal actif par session, à l’exclusion des publicités, des pauses, de la mise en mémoire tampon et des blocages. Utilisez-la comme mesure d’engagement pour l’affichage du contenu ; pour le temps passé, y compris les publicités, voir [Temps passé sur les médias](media-time-spent.md).

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps d’horloge murale écoulé entre les événements pendant que le lecteur est à l’état `play` sur le contenu principal. Le temps pendant les publicités, les pauses, les événements de mise en mémoire tampon et les blocages est exclu. La mesure est signalée lors de l’appel de fermeture. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les flux de données, Data Warehouse et les API de création de rapports.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.timePlayed` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
