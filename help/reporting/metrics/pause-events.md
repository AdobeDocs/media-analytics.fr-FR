---
title: Événements Pause
description: Compte chaque pause distincte qui s’est produite au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 12%

---


# Événements Pause

La mesure **Événements de pause** comptabilise chaque événement distinct [début de pause](/help/implementation/events/playback/pause-start.md) reçu au cours d’une session, y compris plusieurs pauses au cours de la même session. Associez-la à [ Durée totale de pause ](total-pause-duration.md) pour obtenir la durée moyenne de pause, ainsi qu’à [ Flux impactés par la pause ](paused-impacted-streams.md) pour compter les sessions qui se sont interrompues au moins une fois.

## Méthode de calcul de cette mesure

Le serveur principal du média est incrémenté `mediaReporting.sessionDetails.pauseCount` chaque événement [début de pause](/help/implementation/events/playback/pause-start.md). La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pauseCount` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | S.O. |
