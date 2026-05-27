---
title: Durée de lecture unique
description: Indique les secondes de contenu distinct visualisé au cours d’une session, ce qui déduplique les relectures de recherche vers l’arrière.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Durée de lecture unique

La mesure **Temps de lecture unique** indique les secondes de contenu distinct visualisé au cours d’une session, dédupliquant les segments qui ont été relus par le biais de la recherche arrière. Par rapport au [Temps passé sur le contenu](content-time-spent.md), le temps de lecture unique est inférieur lorsqu’un utilisateur ou une utilisatrice reregarde une partie du même contenu au cours de la même session.

## Méthode de calcul de cette mesure

Le serveur principal du média suit les intervalles du curseur de lecture qui ont été visionnés au cours de la session et additionne leur union. La lecture du même segment de cinq secondes deux fois compte toujours cinq secondes. La mesure est signalée lors de l’appel de fermeture. La valeur s’affiche sous la forme `HH:MM:SS` dans Analysis Workspace et en secondes dans les flux de données, Data Warehouse et les API de création de rapports.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.uniqueTimePlayed` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
