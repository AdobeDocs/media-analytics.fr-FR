---
title: Station
description: Indique le nom ou l’ID de la station radio pour le contenu de diffusion audio.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# Station

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Station**. Voir [Station](/help/implementation/variables/standard-metadata/station.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Station** indique le nom ou l’identifiant de la station radio qui diffuse le contenu audio (par exemple, `"NPR"` ou `"WXYZ-FM"`). Utilisez-le pour comparer l&#39;engagement entre les stations d&#39;un réseau syndiqué.

## Mode de remplissage de cette dimension

La station est définie par le lecteur au début de la session pour le contenu audio.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.station` de données contextuelles lorsque [[!UICONTROL Métadonnées audio]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Éléments de dimension

Chaque élément correspond au nom ou à l&#39;ID littéral de la station indiqué au début de la session. Utilisez un seul identifiant canonique par station afin que l&#39;engagement ne se fragmente pas entre les variantes d&#39;appel.
