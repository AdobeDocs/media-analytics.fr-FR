---
title: Temps passé sur le chapitre
description: Indique le nombre total de secondes de lecture active par chapitre.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# Temps passé sur le chapitre

La mesure **Temps passé sur le chapitre** indique le nombre total de secondes de lecture active par chapitre. Associez-le à [Longueur du chapitre](/help/reporting/dimensions/chapter-length.md) pour calculer la part de chaque chapitre consommé.

## Méthode de calcul de cette mesure

Le serveur principal du média additionne le temps d’horloge murale écoulé entre les événements pendant que le lecteur est à l’état `play` sur un chapitre. Le temps pendant les pauses, la mise en mémoire tampon et les blocages est exclu. La mesure est signalée lors de l’appel de fermeture du chapitre. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les flux de données, Data Warehouse et les API de création de rapports.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.chapter.timePlayed` de données contextuelles lorsque l’option [[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
