---
title: Artiste
description: Indique l’artiste performant pour le contenu audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 9%

---


# Artiste

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Artiste**. Voir [Artist](/help/implementation/variables/standard-metadata/artist.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Artiste** indique l’artiste interprète ou exécutant pour le contenu audio (par exemple, `"Crested Larks"`). Utilisez-le pour différencier l&#39;engagement sur les catalogues de musique ou de podcast par interprète.

## Mode de remplissage de cette dimension

L’artiste est défini par le lecteur au début de la session pour le contenu audio.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.artist` de données contextuelles lorsque [[!UICONTROL Métadonnées audio]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoaudioartist` |

## Éléments de dimension

Chaque élément correspond au nom littéral de l’artiste indiqué au début de la session. Utilisez un nom canonique et stable par artiste afin que les données ne se fragmentent pas entre les variantes de mise en forme.
