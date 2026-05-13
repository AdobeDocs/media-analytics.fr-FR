---
title: Erreurs
description: Indique le nombre d’événements d’erreur par session.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 6%

---


# Erreurs

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Erreurs**. Adobe Analytics renseigne automatiquement une paire [mesure d’événements d’erreur](/help/reporting/metrics/error-events.md) à partir de la même variable de données contextuelles `a.media.qoe.errorCount`. Customer Journey Analytics expose un seul champ de `mediaReporting.qoeDataDetails.errorCount` que vous pouvez utiliser comme dimension ou mesure.*

>[!ENDSHADEBOX]

La dimension **Erreurs** indique le nombre d’événements d’erreur reçus au cours d’une session. Utilisez la dimension pour ventiler l’engagement par nombre exact d’erreurs.

## Mode de remplissage de cette dimension

Le serveur principal du média incrémente le décompte à chaque erreur signalée par le lecteur. La valeur est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.errorCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoeerrorcountevar, post_videoqoeerrorcountevar` |

## Éléments de dimension

Chaque élément est la valeur littérale du nombre d’erreurs signalée lors de l’appel de fermeture. Pour les rapports booléens au niveau de la session (si une erreur s’est produite), utilisez [Flux impactés par l’erreur](/help/reporting/metrics/error-impacted-streams.md). Pour les ID d’erreur uniques, utilisez [ID d’erreur externes](external-error-ids.md) et [ID d’erreur SDK du lecteur](player-sdk-error-ids.md).
