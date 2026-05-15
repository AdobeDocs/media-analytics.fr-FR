---
title: Démarrages du média
description: Compte chaque session multimédia qui a commencé, y compris les sessions qui se sont terminées par des publicités preroll ou une mise en mémoire tampon.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# Démarrages du média

La mesure **Démarrages des médias** comptabilise chaque session de médias qui a démarré. Il est incrémenté dès que le serveur principal reçoit un événement [début de session](/help/implementation/events/session/session-start.md), même si la visionneuse abandonne pendant les publicités preroll, la mise en mémoire tampon ou avant la lecture du contenu principal. Utilisez-la comme mesure supérieure de funnel la plus large pour les rapports multimédia ; associez-la à [démarrages de contenu](content-starts.md) pour mesurer le taux de déperdition des publicités et du tampon.

## Méthode de calcul de cette mesure

Le serveur principal du média se `mediaReporting.sessionDetails.isViewed = true` lorsqu’un événement [début de session](/help/implementation/events/session/session-start.md) est reçu. La mesure signalée est `1` par session. Les démarrages de média sont signalés lors de l’appel de démarrage et non lors de l’appel de fermeture. Il s’agit de la seule mesure de phase 1 qui n’attend pas la fermeture de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.view` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.view` |
