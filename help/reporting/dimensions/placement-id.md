---
title: Identifiant de référencement
description: Indique l’identifiant d’emplacement pour chaque publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 9%

---


# Identifiant de référencement

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **ID d’emplacement**. Voir [ID d’emplacement](/help/implementation/variables/ads/placement-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Identifiant d’emplacement** indique l’identifiant de l’emplacement publicitaire (généralement un emplacement ou une zone défini dans votre plateforme de serveur d’annonces). Utilisez la dimension pour comparer l’engagement et l’achèvement sur les emplacements d’emplacement.

## Mode de remplissage de cette dimension

L’identifiant d’emplacement est défini par le lecteur à chaque événement `media.adStart`.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.placement` à un eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.ad.placement` mappée) |

## Éléments de dimension

Chaque élément correspond à la valeur d’emplacement littérale indiquée sur `media.adStart`.
