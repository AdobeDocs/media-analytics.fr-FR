---
title: Événements de mémoire tampon (mesure)
description: Comptabilise les événements de mise en mémoire tampon pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# Événements de mémoire tampon (mesure)

>[!BEGINSHADEBOX]

*Cette page couvre la mesure **Événements de mémoire tampon**. Adobe Analytics renseigne automatiquement une paire [Événements de mémoire tampon (dimension)](/help/reporting/dimensions/buffer-events.md) à partir de la même variable de données contextuelles `a.media.qoe.bufferCount`. Customer Journey Analytics expose un seul champ de `xdm.mediaReporting.qoeDataDetails.bufferCount` que vous pouvez utiliser comme dimension ou mesure.*

>[!ENDSHADEBOX]

La mesure **Événements de mémoire tampon** comptabilise les événements de mise en mémoire tampon entre les sessions, adaptés aux sommes, aux moyennes et aux cumuls de centiles. Utilisez la mesure pour calculer le volume total de mémoire tampon sur une période de rapport et pour comparer la stabilité de la mémoire tampon sur le contenu, les réseaux ou les lecteurs.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente le nombre chaque fois que le lecteur passe à l’état [début de la mémoire tampon](/help/implementation/events/playback/buffer-start.md). La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bufferCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/setup/analytics-reporting.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

Pour les rapports booléens au niveau de la session (si la session a subi une mise en mémoire tampon quelconque), utilisez [Mettre en mémoire tampon les flux impactés](buffer-impacted-streams.md).
