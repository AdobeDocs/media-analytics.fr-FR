---
title: Flux impactés en pause
description: Compte les sessions pendant lesquelles la visionneuse s’est arrêtée au moins une fois.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 11%

---


# Flux impactés en pause

La mesure **Flux impactés en pause** comptabilise les sessions au cours desquelles la visionneuse s’est arrêtée au moins une fois. Il s’agit d’une valeur booléenne au niveau de la session. Plusieurs pauses dans la même session comptent comme un flux impacté. Utilisez-le pour mesurer le nombre de sessions ayant subi une pause ; pour le volume total de pause, utilisez [Événements de pause](pause-events.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement [pause start](/help/implementation/events/playback/pause-start.md) est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pause` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | S.O. |
