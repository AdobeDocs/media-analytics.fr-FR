---
title: Canal de contenu
description: Indique la station de distribution, le réseau ou la propriété où chaque session a été lue.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 6%

---


# Canal de contenu

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Canal de contenu**. Voir [Canal de contenu](/help/implementation/variables/core/content-channel.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Canal de contenu** indique la station de distribution, le réseau ou la propriété où chaque session a été lue. Utilisez-la pour ventiler la lecture par réseau ou section d’une propriété.

## Mode de remplissage de cette dimension

Le canal est défini par le lecteur au début de la session et persiste pendant toute la durée de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.channel` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videochannel, post_videochannel` |

>[!IMPORTANT]
>
>Si le canal n’est pas défini, la dimension n’est pas renseignée pour cette session.

## Éléments de dimension

Chaque élément correspond à la chaîne littérale définie au début de la session. Toute chaîne est acceptée. Les valeurs standard sont un nom de réseau, une partie d’un chemin d’accès au site ou un identifiant de propriété interne.
