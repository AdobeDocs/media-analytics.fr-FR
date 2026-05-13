---
title: Publicité
description: Indique chaque publicité lue, indexée par l’ID de publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 6%

---


# Publicité

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Ad**. Voir [ID d’annonce](/help/implementation/variables/ads/ad-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Annonce** signale chaque annonce publicitaire unique lue, indexée par l’ID d’annonce publicitaire défini sur `media.adStart`. La dimension est la répartition principale pour les rapports sur les publicités et la clé de jointure pour les classifications au niveau des publicités, telles que le nom de la publicité, la longueur de la publicité et l’identifiant Creative.

## Mode de remplissage de cette dimension

La publicité est définie par le lecteur sur chaque événement `media.adStart` comme identifiant stable de la publicité.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.name` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. Persiste pendant la durée de la visite. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `videoad, post_videoad` |

>[!IMPORTANT]
>
>L’ID d’annonce est obligatoire. S’il n’est pas défini ou s’il est vide, la publicité est supprimée des rapports publicitaires des médias en flux continu.

## Éléments de dimension

Chaque élément est un ID d’annonce publicitaire unique signalé sur `media.adStart`. Utilisez un identifiant stable par contenu publicitaire afin que la même annonce publicitaire s’affiche sur une seule ligne entre les sessions.
