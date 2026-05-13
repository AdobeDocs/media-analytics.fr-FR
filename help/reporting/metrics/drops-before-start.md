---
title: Pertes avant le démarrage
description: Comptabilise les sessions pour lesquelles la visionneuse s’est arrêtée avant le rendu du contenu principal.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 8%

---


# Pertes avant le démarrage

La mesure **Pertes avant démarrage** comptabilise les sessions pendant lesquelles la visionneuse s’est arrêtée avant le rendu du contenu principal. La mesure signale l’abandon de pré-contenu quel que soit le comportement de l’annonce publicitaire. Il s’agit donc de la meilleure mesure de la déperdition pure de pré-contenu. Associez-la à [démarrages de média](/help/reporting/metrics/media-starts.md) et [démarrages de contenu](/help/reporting/metrics/content-starts.md) pour calculer le nombre de sessions qui n’ont jamais produit d’image de contenu.

## Méthode de calcul de cette mesure

Le serveur principal du média définit les `mediaReporting.qoeDataDetails.isDroppedBeforeStart = true` pour les sessions qui se ferment sans jamais produire d’événement `media.play` sur le contenu principal. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.dropBeforeStart` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
