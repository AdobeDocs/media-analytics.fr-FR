---
title: Flux affectés par le sous-titrage
description: Comptabilise les sessions dans lesquelles la visionneuse a activé les légendes au moins une fois.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# Flux affectés par le sous-titrage

>[!BEGINSHADEBOX]

*Cette page couvre les **flux affectés par les mesures de reporting de sous-titrage**. Voir [Sous-titrage](/help/implementation/variables/player-state/closed-captioning.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Flux affectés par le sous-titrage** comptabilise les sessions dans lesquelles la visionneuse a activé les sous-titres au moins une fois. La mesure est une valeur booléenne au niveau de la session : plusieurs bascules de légende dans le même nombre de sessions qu’un flux affecté. Pour obtenir le volume total de sous-titrage, utilisez [Nombre de sous-titres codés](closed-captioning-count.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement de début d’état d’activation des sous-titres est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.closedcaptioning.set` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "closedCaptioning"`, champ `isSet` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.set` |
