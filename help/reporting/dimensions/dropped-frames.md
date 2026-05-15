---
title: Images perdues (dimension)
description: Indique le nombre cumulé d’images perdues par session.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---


# Images perdues (dimension)

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Images perdues**. Adobe Analytics renseigne automatiquement une paire [Images perdues (mesure)](/help/reporting/metrics/dropped-frames.md) à partir de la même variable de données contextuelles `a.media.qoe.droppedFrameCount`. Customer Journey Analytics expose un seul champ de `mediaReporting.qoeDataDetails.droppedFrames` que vous pouvez utiliser comme dimension ou mesure. Voir [Images perdues](/help/implementation/variables/quality/dropped-frames.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Images perdues** indique le nombre cumulé d’images perdues au cours d’une session. Utilisez la dimension pour ventiler l’engagement par nombre exact de gouttes.

## Mode de remplissage de cette dimension

Le lecteur met à jour la valeur `droppedFrames` de l’objet QoE au fur et à mesure qu’il accumule des pertes. Le serveur principal signale la dernière valeur de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.droppedFrameCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## Éléments de dimension

Chaque élément est la valeur littérale de décompte signalée lors de l’appel de fermeture. Pour les rapports booléens au niveau de la session (si des images ont été perdues), utilisez [Flux impactés par l’image perdue](/help/reporting/metrics/dropped-frame-impacted-streams.md).
