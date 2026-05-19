---
title: Durée du contenu
description: Indique le nombre total de secondes de lecture du contenu principal actif par session.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 6%

---


# Durée du contenu

La mesure **Temps passé sur le contenu** indique le nombre total de secondes de lecture du contenu principal actif par session, à l’exclusion des publicités, des pauses, de la mise en mémoire tampon et des blocages. Utilisez-la comme mesure d’engagement pour l’affichage du contenu ; pour le temps passé, y compris les publicités, voir [Temps passé sur les médias](media-time-spent.md).

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps d’horloge murale écoulé entre les événements pendant que le lecteur est à l’état `play` sur le contenu principal. Le temps pendant les publicités, les pauses, les événements de mise en mémoire tampon et les blocages est exclu. Étant donné que seule la durée de lecture active est comptabilisée, la mesure peut dépasser [Longueur du contenu](/help/reporting/dimensions/content-length.md) lorsqu’une personne regarde un segment à nouveau en arrière. Chaque passage d’un segment donné accumule un temps de lecture supplémentaire et peut s’accumuler aussi longtemps que l’utilisateur consomme et rembobine du contenu dans une session. La mesure est signalée lors de l’appel de fermeture. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les flux de données, Data Warehouse et les API de création de rapports.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.timePlayed` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
