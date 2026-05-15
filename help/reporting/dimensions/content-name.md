---
title: Nom du contenu
description: Indique le titre lisible par l’utilisateur de chaque session multimédia.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 10%

---


# Nom du contenu

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Nom du contenu**. Voir [Nom du contenu](/help/implementation/variables/core/content-name.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Nom du contenu** indique le titre lisible par l’utilisateur de chaque session multimédia.

## Mode de remplissage de cette dimension

Le nom convivial est défini par le lecteur au début de la session. La valeur signalée correspond à ce qui a été envoyé.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.friendlyName` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>Dans Adobe Analytics, cette valeur correspond également à une classification **Nom de la vidéo** sur la dimension [Contenu](content.md). Il vous incombe de renseigner et de gérer cette classification séparément. Customer Journey Analytics utilise directement cette dimension.

>[!IMPORTANT]
>
>Si le nom du contenu n’est pas défini, la dimension n’est pas renseignée pour cette session.

## Éléments de dimension

Chaque élément correspond au titre littéral indiqué au début de la session (par exemple, `"Blinding Light"`).
