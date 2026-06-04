---
title: Erreurs
description: Indique le nombre d’événements d’erreur par session.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# Erreurs

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Erreurs**. Adobe Analytics renseigne automatiquement une paire [mesure d’événements d’erreur](/help/reporting/metrics/error-events.md) à partir de la même variable de données contextuelles `a.media.qoe.errorCount`. Customer Journey Analytics expose un seul champ de `xdm.mediaReporting.qoeDataDetails.errorCount` que vous pouvez utiliser comme dimension ou mesure.*

>[!ENDSHADEBOX]

La dimension **Erreurs** indique le nombre d’événements d’erreur reçus au cours d’une session. Utilisez la dimension pour ventiler l’engagement par nombre exact d’erreurs.

## Mode de remplissage de cette dimension

Le serveur principal du média incrémente le décompte à chaque erreur signalée par le lecteur. La valeur est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.errorCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/setup/analytics-reporting.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## Éléments de dimension

Chaque élément est la valeur littérale du nombre d’erreurs signalée lors de l’appel de fermeture. Pour les rapports booléens au niveau de la session (si une erreur s’est produite), utilisez [Flux impactés par l’erreur](/help/reporting/metrics/error-impacted-streams.md). Pour les ID d’erreur uniques, utilisez [ID d’erreur externes](external-error-ids.md) et [ID d’erreur SDK du lecteur](player-sdk-error-ids.md).

>[!NOTE]
>
>Si vous utilisez l’ancien Heartbeat SDK (Media SDK 1.5.x-2.x), les identifiants d’erreur générés en interne par le SDK sont automatiquement collectés sous la clé de données contextuelles `a.media.qoe.mediaSdkErrors` et accessibles dans Adobe Analytics via une règle de traitement personnalisée. La caractéristique Audience Manager est `c_contextdata.a.media.qoe.mediaSdkErrors`. Ce champ ne s’applique pas aux implémentations de l’API Media Collection ou Media Edge.
