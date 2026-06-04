---
title: Canal de contenu
description: Indique la station de distribution, le réseau ou la propriété où chaque session a été lue.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 7%

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
| Adobe Analytics | Collecté automatiquement à partir des `a.media.channel` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Si le canal n’est pas défini, la dimension n’est pas renseignée pour cette session.

## Éléments de dimension

Chaque élément correspond à la chaîne littérale définie au début de la session. Toute chaîne est acceptée. Les valeurs standard sont un nom de réseau, une partie d’un chemin d’accès au site ou un identifiant de propriété interne.
