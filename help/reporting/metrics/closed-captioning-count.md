---
title: Nombre de sous-titres
description: Indique le nombre de fois où la visionneuse a activé les sous-titres au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---


# Nombre de sous-titres

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Nombre de sous-titrages**. Voir [Sous-titrage](/help/implementation/variables/player-state/closed-captioning.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Nombre de sous-titres codés** indique le nombre de fois que la visionneuse a activé les sous-titres au cours d’une session. Chaque événement de début d’état activé pour les légendes incrémente le nombre. Associez aux [Flux impactés par le sous-titrage codé](closed-captioning-streams-impacted.md) pour les cumuls booléens au niveau de la session, et aux [Durée totale du sous-titrage codé](closed-captioning-total-duration.md) pour la durée totale à l’état .

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente ce nombre à chaque événement de début d’état activé pour les légendes. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.closedcaptioning.count` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "closedCaptioning"`, champ `count` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.count` |
