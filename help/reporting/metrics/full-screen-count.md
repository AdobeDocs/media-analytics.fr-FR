---
title: Nombre de pages plein écran
description: Indique le nombre de fois où la visionneuse est entrée en plein écran au cours d’une session.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# Nombre de pages plein écran

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Nombre de pages plein écran**. Voir [Plein écran](/help/implementation/variables/player-state/full-screen.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Nombre de visionneuses en plein écran** indique le nombre de fois que la visionneuse est entrée en plein écran au cours d’une session. Chaque événement de démarrage d’état en plein écran incrémente le nombre. Associez aux [Flux impactés par le plein écran](full-screen-streams-impacted.md) pour les cumuls booléens au niveau de la session, ainsi qu’aux [Durée totale du plein écran](full-screen-total-duration.md) pour le temps total passé en statut.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente ce nombre à chaque événement de démarrage d’état en plein écran. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.fullscreen.count` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "fullscreen"`, champ `count` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
