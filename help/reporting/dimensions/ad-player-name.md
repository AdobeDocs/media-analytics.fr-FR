---
title: Nom du lecteur publicitaire
description: Indique le lecteur qui a rendu chaque publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# Nom du lecteur publicitaire

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de compte rendu des performances **Nom du lecteur publicitaire**. Voir [Nom du lecteur publicitaire](/help/implementation/variables/ads/ad-player-name.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Nom du lecteur d’annonces** indique le lecteur qui a rendu chaque annonce (par exemple, `"Freewheel"`, `"Google IMA"`). Le lecteur d’annonces publicitaires peut différer du lecteur de contenu principal lorsque des annonces sont regroupées par un service d’insertion d’annonces côté serveur.

## Mode de remplissage de cette dimension

Le nom du lecteur de publicités est défini par le lecteur à chaque événement [début de la publicité](/help/implementation/events/ads/ad-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.playerName` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## Éléments de dimension

Chaque élément correspond au nom littéral du lecteur d’annonces publicitaires signalé au [début de l’annonce](/help/implementation/events/ads/ad-start.md).
