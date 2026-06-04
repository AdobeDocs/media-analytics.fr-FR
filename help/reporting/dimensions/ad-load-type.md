---
title: Chargements des annonces publicitaires
description: Indique le type de charge publicitaire utilisé pour chaque session de streaming multimédia.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# Chargements des annonces publicitaires

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Chargements d’annonces**. Voir [Type de chargement des annonces](/help/implementation/variables/standard-metadata/ad-load-type.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Chargement de l’annonce** indique le type d’annonce publicitaire chargé au début de chaque session de streaming multimédia. La valeur est définie par le client ou la cliente, ce qui permet aux organisations de classer les sessions en fonction de leur mécanisme de diffusion des annonces (par exemple, `"linear"`, `"dynamic"` ou `"programmatic"`).

## Mode de remplissage de cette dimension

Le type de chargement de l’annonce est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.adLoad` de données contextuelles lorsque [[!UICONTROL Streaming Media]](/help/reporting/setup/analytics-reporting.md) est configuré. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## Éléments de dimension

Chaque élément correspond à la chaîne de type littéral et de chargement définie au début de la session. Les valeurs ne sont pas limitées à une énumération standard : définissez une taxonomie cohérente sur l’ensemble de vos implémentations afin que les valeurs soient cumulées de manière prévisible dans les rapports.
