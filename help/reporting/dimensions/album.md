---
title: Album
description: Indique l’album auquel appartient la piste audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 8%

---


# Album

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Album**. Voir [Album](/help/implementation/variables/standard-metadata/album.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Album** indique l’album auquel appartient la piste audio (par exemple, `"Pinegrove"`). Utilisez-le pour remonter l&#39;engagement entre les pistes du même album.

## Mode de remplissage de cette dimension

L’album est défini par le lecteur au début de la session pour le contenu audio.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.album` de données contextuelles lorsque [[!UICONTROL Métadonnées audio]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoaudioalbum` |

## Éléments de dimension

Chaque élément correspond au titre littéral de l’album indiqué au début de la session. Deux albums portant le même titre de différents artistes sont réduits à un seul élément de ligne. Associez-la à la dimension [Artiste](artist.md) pour clarifier les choses.
