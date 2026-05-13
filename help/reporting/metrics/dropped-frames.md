---
title: Images perdues (mesure)
description: Indique les pertes d’images cumulées pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Images perdues (mesure)

>[!BEGINSHADEBOX]

*Cette page couvre la mesure **Images perdues**. Adobe Analytics renseigne automatiquement une paire [images perdues (dimension)](/help/reporting/dimensions/dropped-frames.md) à partir de la même variable de données contextuelles `a.media.qoe.droppedFrameCount`. Customer Journey Analytics expose un seul champ de `mediaReporting.qoeDataDetails.droppedFrames` que vous pouvez utiliser comme dimension ou mesure. Voir [Images perdues](/help/implementation/variables/quality/dropped-frames.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Images perdues** signale les images perdues cumulées entre les sessions, adaptées aux sommes, aux moyennes et aux cumuls de centiles. Utilisez la mesure pour calculer le volume total de perte au cours d’une période de rapport et pour comparer la qualité de rendu des images sur l’ensemble du contenu, des réseaux ou des lecteurs.

## Méthode de calcul de cette mesure

Le lecteur met à jour la valeur `droppedFrames` de l’objet QoE à mesure que les pertes s’accumulent. Le serveur principal signale la dernière valeur de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.droppedFrameCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

Pour les rapports booléens au niveau de la session (si des images ont été perdues), utilisez [Flux impactés par l’image perdue](dropped-frame-impacted-streams.md).
