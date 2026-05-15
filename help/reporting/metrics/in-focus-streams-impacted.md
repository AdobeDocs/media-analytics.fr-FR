---
title: Flux impactés par dans le focus
description: Comptabilise les sessions dans lesquelles le lecteur était ciblé au moins une fois.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Flux impactés par dans le focus

>[!BEGINSHADEBOX]

*Cette page couvre les **flux concernés par la mesure de reporting sur laquelle le focus est**. Voir [En bref](/help/implementation/variables/player-state/in-focus.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Flux affectés par dans le focus** comptabilise les sessions dans lesquelles le lecteur a été ciblé au moins une fois. La mesure est une valeur booléenne au niveau de la session : plusieurs événements ciblés dans le même nombre de sessions sont comptabilisés comme un flux affecté. Pour le volume total d’événement focus, utilisez [Nombre d’événements focus](in-focus-count.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit l’indicateur de `isSet` dans `mediaReporting.states[]` pour que l’entrée `inFocus` `true` la première fois qu’un événement de `media.statesUpdate` avec `inFocus` dans `statesStart` est reçu. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.infocus.set` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "inFocus"`, champ `isSet` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.set` |
