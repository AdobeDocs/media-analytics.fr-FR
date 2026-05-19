---
title: Nombre de mises en sourdine
description: Indique le nombre de fois où la visionneuse a coupé l’audio au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%

---


# Nombre de mises en sourdine

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Nombre de messages muets**. Voir [Muet](/help/implementation/variables/player-state/mute.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Nombre de mises en sourdine** indique le nombre de fois que la visionneuse a mis le son en sourdine au cours d’une session. Chaque événement de démarrage d’état de mise en sourdine incrémente le décompte. Associez aux [Flux impactés par le mode muet](mute-streams-impacted.md) pour les cumuls booléens au niveau de la session, ainsi qu’aux [Durée totale du mode muet](mute-total-duration.md) pour le temps total passé dans l’état.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente ce nombre à chaque événement de démarrage avec désactivation du son. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.mute.count` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "mute"`, champ `count` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
