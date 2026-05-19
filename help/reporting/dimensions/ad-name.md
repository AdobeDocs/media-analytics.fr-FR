---
title: Nom de la publicité
description: Indique le titre lisible par l’utilisateur de chaque publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 6%

---


# Nom de la publicité

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Nom de l’annonce**. Voir [Nom de l’annonce](/help/implementation/variables/ads/ad-name.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Nom de l’annonce** indique le titre lisible par l’utilisateur de chaque annonce.

## Mode de remplissage de cette dimension

Le nom de l’annonce publicitaire est défini par le lecteur à chaque événement [début de l’annonce](/help/implementation/events/ads/ad-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.friendlyName` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

Dans Adobe Analytics, cette dimension apparaît de deux manières : sous la forme **Nom de l’annonce (variable)** (collecté directement à partir de `a.media.ad.friendlyName`) et sous la forme **Nom de l’annonce** (classification dérivée de la dimension [Annonce](ad.md)). Si vous utilisez la classification, vous êtes chargé de renseigner et de gérer ses valeurs à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). L’utilisation de la **Nom de l’annonce (variable)** ne nécessite aucune maintenance de la classification, mais vous perdez la relation 1:1 garantie entre le nom de l’annonce et la dimension [Annonce](ad.md) parente. Utilisez le composant le mieux pris en charge par votre workflow d’implémentation.

## Éléments de dimension

Chaque élément correspond au titre littéral de l’annonce publicitaire indiqué au [début de l’annonce](/help/implementation/events/ads/ad-start.md) (par exemple, `"Ford F-150"`).
