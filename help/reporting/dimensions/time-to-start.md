---
title: Heure de début (dimension)
description: Indique le temps écoulé avant le rendu de la première image.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# Heure de début (dimension)

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Heure de début**. Adobe Analytics renseigne automatiquement une paire [Heure de début (mesure)](/help/reporting/metrics/time-to-start.md) à partir de la même variable de données contextuelles `a.media.qoe.timeToStart`. Customer Journey Analytics expose un seul champ de `mediaReporting.qoeDataDetails.timeToStart` que vous pouvez utiliser comme dimension ou mesure. Voir [Heure de début](/help/implementation/variables/quality/time-to-start.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Temps de démarrage** indique le temps écoulé entre le début de la session et le premier rendu d’image. Utilisez la dimension pour ventiler l’engagement par compartiment au moment du démarrage. Adobe stocke la valeur en secondes et la convertit lors de l’ingestion à partir des millisecondes signalées par le lecteur.

## Mode de remplissage de cette dimension

Le lecteur définit le `timeToStart` sur l’objet QoE avant le déclenchement du démarrage de la session. Le serveur principal signale la valeur lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.timeToStart` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoetimetostartevar, post_videoqoetimetostartevar` |

## Éléments de dimension

Chaque élément correspond à la valeur de temps de démarrage littérale signalée lors de l’appel de fermeture.
