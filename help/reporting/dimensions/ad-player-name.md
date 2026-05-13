---
title: Nom du lecteur publicitaire
description: Indique le lecteur qui a rendu chaque publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# Nom du lecteur publicitaire

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de compte rendu des performances **Nom du lecteur publicitaire**. Voir [Nom du lecteur publicitaire](/help/implementation/variables/ads/ad-player-name.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Nom du lecteur d’annonces** indique le lecteur qui a rendu chaque annonce (par exemple, `"Freewheel"`, `"Google IMA"`). Le lecteur d’annonces publicitaires peut différer du lecteur de contenu principal lorsque des annonces sont regroupées par un service d’insertion d’annonces côté serveur.

## Mode de remplissage de cette dimension

Le nom du lecteur d’annonces est défini par le lecteur à chaque événement `media.adStart`.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.playerName` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videoadplayername, post_videoadplayername` |

## Éléments de dimension

Chaque élément correspond au nom littéral du lecteur d’annonces publicitaires signalé sur `media.adStart`.
