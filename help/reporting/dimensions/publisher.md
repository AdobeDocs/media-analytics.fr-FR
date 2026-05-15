---
title: Éditeur
description: Indique l’éditeur de contenu audio.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# Éditeur

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Éditeur**. Voir [Publisher](/help/implementation/variables/standard-metadata/publisher.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Éditeur** indique l’éditeur de contenu audio (par exemple, un réseau de podcasts ou un éditeur de livres audio). Utilisez-le pour comparer l’engagement entre les éditeurs dans un catalogue audio traité.

## Mode de remplissage de cette dimension

L’éditeur est défini par le lecteur au début de la session pour le contenu audio.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.publisher` de données contextuelles lorsque [[!UICONTROL Métadonnées audio]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## Éléments de dimension

Chaque élément correspond au nom littéral de l’éditeur indiqué au début de la session.
