---
title: Démarrages du chapitre
description: Compte chaque chapitre qui a commencé à être lu au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---


# Démarrages du chapitre

La mesure **Début du chapitre** comptabilise chaque chapitre qui a commencé à être lu au cours d’une session. Associez-le à [Chapitre terminé](chapter-completes.md) pour calculer le taux d’achèvement du chapitre.

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.chapterDetails.isStarted = true` lorsqu’un événement de `media.chapterStart` est reçu. La mesure est signalée lors de l’appel de fermeture du chapitre.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.chapter.view` de données contextuelles lorsque l’option [[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
