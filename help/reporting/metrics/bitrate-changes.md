---
title: Modifications du débit (mesure)
description: Comptabilise les événements de changement de débit pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 7%

---


# Modifications du débit (mesure)

>[!BEGINSHADEBOX]

*Cette page couvre la mesure **Modifications du débit**. Adobe Analytics renseigne automatiquement une paire [Modifications de débit (dimension)](/help/reporting/dimensions/bitrate-changes.md) à partir de la même variable de données contextuelles `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics expose un seul champ de `mediaReporting.qoeDataDetails.bitrateChangeCount` que vous pouvez utiliser comme dimension ou mesure. Consultez [Modification de débit](/help/implementation/variables/quality/bitrate-change.md) pour savoir comment déclencher des événements de modification de débit.*

>[!ENDSHADEBOX]

La mesure **Changements de débit** comptabilise les événements de changement de débit entre les sessions, adaptés aux sommes, aux moyennes et aux cumuls de centiles. Utilisez la mesure pour calculer le volume total des modifications de débit au cours d’une période de rapport et pour comparer la stabilité du débit sur le contenu, les réseaux ou les lecteurs.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente le décompte à chaque événement [changement de débit](/help/implementation/events/playback/bitrate-change.md) reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bitrateChangeCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

Pour les rapports booléens au niveau de la session (si la session a subi un changement de débit), utilisez [&#x200B; Flux impactés par le changement de débit &#x200B;](bitrate-change-impacted-streams.md).
