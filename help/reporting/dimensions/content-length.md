---
title: Durée du contenu
description: Indique la durée totale, en secondes, de chaque session multimédia, telle qu’elle est définie au début de la session.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%

---


# Durée du contenu

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Longueur du contenu**. Voir [Longueur du contenu](/help/implementation/variables/core/content-length.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Longueur du contenu** indique la durée totale, en secondes, de chaque session multimédia, telle qu’elle est définie au début de la session. Il alimente les mesures du serveur principal, y compris les [marqueurs de progression](/help/reporting/metrics/progress-markers.md) et [Audience moyenne par minute](/help/reporting/metrics/average-minute-audience.md).

## Mode de remplissage de cette dimension

La longueur du contenu est définie par le lecteur au début de la session. La valeur signalée correspond à la durée complète de la ressource en secondes, et non au curseur de lecture écoulé.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.length` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>Dans Adobe Analytics, cette valeur correspond également à une classification **Longueur de la vidéo** sur la dimension [Contenu](content.md). Il vous incombe de renseigner et de gérer cette classification séparément. Customer Journey Analytics utilise directement cette dimension. Vous pouvez utiliser le [regroupement de valeurs](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing) si vous le souhaitez.

>[!IMPORTANT]
>
>Si la longueur du contenu n’est pas définie ou n’est pas supérieure à zéro, les marqueurs de progression et l’audience moyenne par minute ne sont pas générés pour cette session. Pour les flux en direct d’une durée inconnue, définissez `86400`.

## Éléments de dimension

Chaque élément correspond à la valeur de longueur littérale, en secondes, indiquée au début de la session.
