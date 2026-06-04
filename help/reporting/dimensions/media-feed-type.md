---
title: Type de flux multimédia
description: Indique le flux de diffusion (par exemple, East-HD ou West-SD) lorsque le même contenu est diffusé via plusieurs flux.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# Type de flux multimédia

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Type de flux multimédia**. Voir [Type de flux multimédia](/help/implementation/variables/standard-metadata/media-feed-type.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Type de flux multimédia** indique le flux de diffusion pour chaque session (par exemple, `"East-HD"`, `"West-SD"` ou `"4K"`). Utilisez-le lorsque le même contenu est diffusé par le biais de plusieurs flux régionaux ou de qualité et que l’engagement doit être signalé par flux.

## Mode de remplissage de cette dimension

Le type de flux multimédia est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.feed` de données contextuelles lorsque [[!UICONTROL  Métadonnées vidéo ]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Éléments de dimension

Chaque élément correspond à la valeur de flux littérale signalée au début de la session. Utilisez un ensemble stable d’identifiants de flux par division régionale ou de qualité.
