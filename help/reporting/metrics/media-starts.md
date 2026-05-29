---
title: Démarrages du média
description: Compte chaque session multimédia qui a commencé, y compris les sessions qui se sont terminées par des publicités preroll ou une mise en mémoire tampon.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 6%

---


# Démarrages du média

La mesure **Démarrages des médias** comptabilise chaque session de médias qui a démarré. Il est incrémenté dès que le serveur principal reçoit un événement [début de session](/help/implementation/events/session/session-start.md), même si la visionneuse abandonne pendant les publicités preroll, la mise en mémoire tampon ou avant la lecture du contenu principal. Utilisez-la comme mesure supérieure de funnel la plus large pour les rapports multimédia ; associez-la à [démarrages de contenu](content-starts.md) pour mesurer le taux de déperdition des publicités et du tampon.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur lorsqu’un événement [début de session](/help/implementation/events/session/session-start.md) est reçu. La mesure signalée est `1` par session. Les démarrages de média sont signalés lors de l’appel de démarrage et non lors de l’appel de fermeture ; il s’agit de la seule mesure qui n’attend pas la fermeture de la session. Toutes les autres mesures multimédia, y compris [Débuts du contenu](/help/reporting/metrics/content-starts.md), [Temps passé sur le contenu](/help/reporting/metrics/content-time-spent.md) et [Marqueurs de progression](/help/reporting/metrics/progress-markers.md), sont signalées lors de l’appel de fermeture et ne sont pas disponibles en temps réel pendant la lecture. [Les démarrages d’annonce publicitaire](/help/reporting/metrics/ad-starts.md) est la mesure supplémentaire signalée sur son événement déclencheur plutôt qu’à la fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.view` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.view` |
