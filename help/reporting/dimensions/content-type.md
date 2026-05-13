---
title: Type de contenu
description: Indique le format du flux (VOD, Live, Linéaire, podcast, chanson, etc.).
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 8%

---


# Type de contenu

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Type de contenu**. Voir [Type de contenu](/help/implementation/variables/core/content-type.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Type de contenu** indique le format du flux (par exemple, VOD, Live ou Linéaire pour la vidéo, et chanson, podcast ou livre audio pour l’audio).

## Mode de remplissage de cette dimension

Le type de contenu est défini par le lecteur au début de la session et transmis à chaque événement. Elle n’est pas dérivée ; la valeur signalée correspond à ce qui a été envoyé lors de la collecte.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.contentType` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videocontenttype, post_videocontenttype` |

>[!IMPORTANT]
>
>Si le type de contenu n’est pas défini ou est vide, la dimension signale des `missing_content_type` pour la session. Utilisez cette valeur pour rechercher les implémentations à corriger.

## Éléments de dimension

Les valeurs définies par Adobe renseignent les segments et les rapports intégrés. Les chaînes personnalisées sont acceptées, mais ne correspondent pas aux segments intégrés.

| Type de diffusion | Valeurs recommandées |
| --- | --- |
| Vidéo | `vod`, `live`, `linear`, `ugc`, `dvod` |
| Audio | `song`, `podcast`, `audiobook`, `radio` |

## Segments recommandés

| Segment | Composants de |
| --- | --- |
| [!UICONTROL Contenu &#x200B;] | Type de contenu = `vod` |
| [!UICONTROL Contenu en direct] | Type de contenu = `live` |
| [!UICONTROL Contenu linéaire] | Type de contenu = `linear` |
