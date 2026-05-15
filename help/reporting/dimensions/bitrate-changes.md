---
title: Changements de débit (dimension)
description: Indique le nombre d’événements de changement de débit par session.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# Changements de débit (dimension)

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Modifications du débit**. Adobe Analytics renseigne automatiquement une paire [Modifications de débit (mesure)](/help/reporting/metrics/bitrate-changes.md) à partir de la même variable de données contextuelles `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics expose un seul champ de `mediaReporting.qoeDataDetails.bitrateChangeCount` que vous pouvez utiliser comme dimension ou mesure. Consultez [Modification de débit](/help/implementation/variables/quality/bitrate-change.md) pour savoir comment déclencher des événements de modification de débit.*

>[!ENDSHADEBOX]

La dimension **Changements de débit** indique le nombre d’événements de changement de débit qui se sont produits au cours d’une session. Utilisez la dimension pour ventiler l’engagement et la qualité par valeur exacte de nombre de modifications (par exemple, « sessions avec des modifications de débit 3 par rapport aux sessions avec 0 »).

## Mode de remplissage de cette dimension

Le serveur principal du média incrémente le décompte à chaque événement [changement de débit](/help/implementation/events/playback/bitrate-change.md) reçu au cours de la session. La valeur est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bitrateChangeCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## Éléments de dimension

Chaque élément est la valeur littérale change-count signalée lors de l&#39;appel de fermeture. Pour les rapports booléens au niveau de la session (si la session a subi un changement de débit), utilisez [ Flux impactés par le changement de débit ](/help/reporting/metrics/bitrate-change-impacted-streams.md).
