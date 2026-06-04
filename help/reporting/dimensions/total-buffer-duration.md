---
title: Durée totale du buffer (dimension)
description: Indique le nombre cumulé de secondes passées en mémoire tampon par session.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Durée totale du buffer (dimension)

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Durée totale du tampon**. Adobe Analytics renseigne automatiquement une paire [Durée totale de la mémoire tampon (mesure)](/help/reporting/metrics/total-buffer-duration.md) à partir de la même variable de données contextuelles `a.media.qoe.bufferTime`. Customer Journey Analytics expose un seul champ de `xdm.mediaReporting.qoeDataDetails.bufferTime` que vous pouvez utiliser comme dimension ou mesure.*

>[!ENDSHADEBOX]

La dimension **Durée totale de la mémoire tampon** indique le temps cumulé, en secondes, que le lecteur a passé dans un état de mémoire tampon au cours d’une session. Utilisez la dimension pour ventiler l’engagement par valeur exacte de durée de la mémoire tampon.

## Mode de remplissage de cette dimension

Le serveur principal du média additionne la durée de chaque intervalle de mémoire tampon (du [&#x200B; début de la mémoire tampon &#x200B;](/help/implementation/events/playback/buffer-start.md) au changement d&#39;état suivant). La valeur est signalée lors de l’appel de fermeture. Analysis Workspace affiche la valeur en tant que `HH:MM:SS` ; les flux de données, Data Warehouse et les API de création de rapports affichent la valeur en secondes.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bufferTime` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/setup/analytics-reporting.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## Éléments de dimension

Chaque élément correspond à la valeur de durée littérale, en secondes, signalée lors de l’appel de fermeture.
