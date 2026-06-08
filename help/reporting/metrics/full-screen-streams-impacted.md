---
title: Flux impactés par le plein écran
description: Comptabilise les sessions au cours desquelles la visionneuse est entrée en plein écran au moins une fois.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Flux impactés par le plein écran

>[!BEGINSHADEBOX]

*Cette page couvre les mesures de reporting **Flux affectés par le plein écran**. Voir [Plein écran](/help/implementation/variables/player-state/full-screen.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Flux affectés par le plein écran** comptabilise les sessions au cours desquelles la visionneuse est entrée en plein écran au moins une fois. La mesure est un booléen au niveau de la session ; plusieurs entrées en plein écran au sein d’une même session comptent comme un flux affecté. Pour le volume d’entrée plein écran total, utilisez [Nombre de pages plein écran](full-screen-count.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement de démarrage d’état plein écran est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.fullscreen.set` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "fullscreen"`, champ `isSet` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.set` |
