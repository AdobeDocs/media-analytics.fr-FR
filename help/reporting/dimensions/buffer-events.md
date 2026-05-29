---
title: Événements de mémoire tampon (dimension)
description: Indique le nombre d’événements de mise en mémoire tampon par session.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---


# Événements de mémoire tampon (dimension)

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Événements de mémoire tampon**. Adobe Analytics renseigne automatiquement une paire [Événements de mémoire tampon (mesure)](/help/reporting/metrics/buffer-events.md) à partir de la même variable de données contextuelles `a.media.qoe.bufferCount`. Customer Journey Analytics expose un seul champ de `xdm.mediaReporting.qoeDataDetails.bufferCount` que vous pouvez utiliser comme dimension ou mesure.*

>[!ENDSHADEBOX]

La dimension **Événements de mise en mémoire tampon** indique le nombre d’événements de mise en mémoire tampon qui se sont produits au cours d’une session. Utilisez la dimension pour ventiler l’engagement par nombre exact de tampons.

## Mode de remplissage de cette dimension

Le serveur principal du média incrémente le nombre chaque fois que le lecteur passe en état `buffer`. La valeur est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bufferCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Éléments de dimension

Chaque élément est la valeur littérale du nombre de tampons signalée lors de l&#39;appel de fermeture. Pour les rapports booléens au niveau de la session (si la session a subi une mise en mémoire tampon quelconque), utilisez [Mettre en mémoire tampon les flux impactés](/help/reporting/metrics/buffer-impacted-streams.md).
