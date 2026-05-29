---
title: Événements Pause
description: Compte chaque pause distincte qui s’est produite au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# Événements Pause

La mesure **Événements de pause** comptabilise chaque événement distinct [début de pause](/help/implementation/events/playback/pause-start.md) reçu au cours d’une session, y compris plusieurs pauses au cours de la même session. Associez-la à [&#x200B; Durée totale de pause &#x200B;](total-pause-duration.md) pour obtenir la durée moyenne de pause, ainsi qu’à [&#x200B; Flux impactés par la pause &#x200B;](paused-impacted-streams.md) pour compter les sessions qui se sont interrompues au moins une fois.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente ce nombre à chaque événement [début de la pause](/help/implementation/events/playback/pause-start.md). Une seule pause continue génère un incrément, quelle que soit sa durée. Les pulsations [pings](/help/implementation/events/playback/ping.md) envoyées alors que le lecteur reste en pause appartiennent toutes à la même période de pause et n’incrémentent pas à nouveau le nombre. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pauseCount` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | S.O. |
