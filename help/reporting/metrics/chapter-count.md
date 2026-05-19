---
title: Nombre de chapitres
description: Indique le nombre de chapitres ayant démarré au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# Nombre de chapitres

La mesure **Nombre de chapitres** indique le nombre de chapitres ayant démarré au cours d’une session. Utilisez-le pour comparer la consommation des chapitres dans le contenu. Pour les décomptes de début de chapitre pivotés par les dimensions de chapitre (nom du chapitre, position), utilisez la mesure Débuts de chapitre disponible lorsque la catégorie de variable Chapitres est activée.

## Méthode de calcul de cette mesure

Le serveur principal du média est incrémenté `mediaReporting.sessionDetails.chapterCount` chaque événement [début de chapitre](/help/implementation/events/chapters/chapter-start.md) reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapterCount` à un événement personnalisé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (événement personnalisé auquel votre règle de traitement `a.media.chapterCount` mappe ; voir recherche [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | S.O. |
