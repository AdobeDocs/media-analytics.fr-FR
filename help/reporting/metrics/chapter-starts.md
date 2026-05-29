---
title: Démarrages du chapitre
description: Compte chaque chapitre qui a commencé à être lu au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---


# Démarrages du chapitre

La mesure **Début du chapitre** comptabilise chaque chapitre qui a commencé à être lu au cours d’une session. Associez-le à [Chapitre terminé](chapter-completes.md) pour calculer le taux d’achèvement du chapitre.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur lorsqu’un événement [début du chapitre](/help/implementation/events/chapters/chapter-start.md) est reçu. La mesure est signalée lors de l’appel de fermeture du chapitre.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.chapter.view` de données contextuelles lorsque l’option [[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
