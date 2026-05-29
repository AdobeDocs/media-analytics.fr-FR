---
title: Pertes avant le démarrage
description: Comptabilise les sessions pour lesquelles la visionneuse s’est arrêtée avant le rendu du contenu principal.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 7%

---


# Pertes avant le démarrage

La mesure **Pertes avant démarrage** comptabilise les sessions pendant lesquelles la visionneuse s’est arrêtée avant le rendu du contenu principal. La mesure signale l’abandon de pré-contenu quel que soit le comportement de l’annonce publicitaire. Il s’agit donc de la meilleure mesure de la déperdition pure de pré-contenu. Associez-la à [démarrages de média](/help/reporting/metrics/media-starts.md) et [démarrages de contenu](/help/reporting/metrics/content-starts.md) pour calculer le nombre de sessions qui n’ont jamais produit d’image de contenu.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur pour les sessions qui se ferment sans jamais produire d’événement [play](/help/implementation/events/playback/play.md) sur le contenu principal. La mesure est signalée lors de l’appel de fermeture. Les scénarios courants sont les suivants : la visionneuse se ferme lors d’une publicité preroll, le lecteur se bloque indéfiniment dans la phase de mise en mémoire tampon initiale ou une erreur se déclenche avant le premier événement de lecture du contenu principal. Dans tous ces cas, la session enregistre un [Début média](/help/reporting/metrics/media-starts.md) mais aucun [Début contenu](/help/reporting/metrics/content-starts.md) ni aucun [Marqueur de progression](/help/reporting/metrics/progress-markers.md) n’est enregistré.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.dropBeforeStart` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
