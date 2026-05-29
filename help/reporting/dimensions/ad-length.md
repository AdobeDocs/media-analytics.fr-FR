---
title: Longueur de la publicité
description: Indique la durée en secondes de chaque publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Longueur de la publicité

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **longueur de l’annonce**. Voir [Durée de l’annonce](/help/implementation/variables/ads/ad-length.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Longueur de l’annonce** indique la durée en secondes de chaque annonce publicitaire.

## Mode de remplissage de cette dimension

La durée de l’annonce est définie par le lecteur à chaque événement [début de l’annonce](/help/implementation/events/ads/ad-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.length` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videoadlength`, `post_videoadlength` |
| Audience Manager | `c_contextdata.a.media.ad.length` |

Dans Adobe Analytics, cette dimension apparaît de deux manières : sous la forme **Longueur de l’annonce (variable)** (collectée directement à partir de `a.media.ad.length`) et sous la forme **Longueur de l’annonce** (classification dérivée de la dimension [Annonce](ad.md)). Si vous utilisez la classification, vous êtes chargé de renseigner et de gérer ses valeurs à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). L’utilisation de la **longueur de l’annonce publicitaire (variable)** ne nécessite aucune maintenance de la classification, mais vous perdez la relation garantie 1:1 entre la longueur de l’annonce publicitaire et la dimension [annonce](ad.md) parente. Utilisez le composant le mieux pris en charge par votre workflow d’implémentation.

## Éléments de dimension

Chaque élément correspond à la valeur de la durée littérale de l’annonce, en secondes, indiquée au [début de l’annonce](/help/implementation/events/ads/ad-start.md).
