---
title: Flux impactés par le mode silencieux
description: Comptabilise les sessions dans lesquelles la visionneuse a coupé l’audio au moins une fois.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---


# Flux impactés par le mode silencieux

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de création de rapports **Flux affectés par le mode silencieux**. Voir [Muet](/help/implementation/variables/player-state/mute.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Flux affectés par le mode muet** comptabilise les sessions dans lesquelles la visionneuse a coupé l’audio au moins une fois. La mesure est une valeur booléenne au niveau de la session : plusieurs bascules de désactivation du son dans le même nombre de sessions qu’un flux affecté. Pour le volume muet total, utilisez [Nombre de muets](mute-count.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement de démarrage d’état de mise en sourdine est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.mute.set` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "mute"`, champ `isSet` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
