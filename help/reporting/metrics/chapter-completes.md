---
title: Lectures complètes du chapitre
description: Compte chaque chapitre lu jusqu’à la fin.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# Lectures complètes du chapitre

La mesure **Chapitre terminé** comptabilise chaque chapitre lu jusqu’à la fin. Associez-le à [Début du chapitre](chapter-starts.md) pour calculer le taux d’achèvement du chapitre.

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.chapterDetails.isCompleted = true` lorsqu’un événement de `media.chapterComplete` est reçu. La mesure est signalée lors de l’appel de fermeture du chapitre. Les chapitres ignorés ou abandonnés pendant la lecture ne sont pas considérés comme terminés.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.chapter.complete` de données contextuelles lorsque l’option [[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
