---
title: Nombre d’éléments ciblés
description: Indique le nombre de fois que le lecteur a obtenu la cible d’action au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# Nombre d’éléments ciblés

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Nombre de focus**. Voir [En bref](/help/implementation/variables/player-state/in-focus.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Nombre de focus** indique le nombre de fois où le lecteur a accédé au focus au cours d’une session. Chaque événement de début d’état de focus incrémente le nombre. Associez aux [Flux impactés par dans le focus](in-focus-streams-impacted.md) pour les cumuls booléens au niveau de la session et aux [Durée totale dans le focus](in-focus-total-duration.md) pour la durée totale dans l’état.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente ce nombre à chaque événement de début d’état de focus. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.infocus.count` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "inFocus"`, champ `count` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
