---
title: URL de l’élément créatif
description: Indique l’URL de ressource de chaque élément publicitaire.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 10%

---


# URL de l’élément créatif

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **URL Creative**. Voir [URL &#x200B;](/help/implementation/variables/ads/creative-url.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **URL** indique l’URL de ressource de chaque contenu publicitaire. Utilisez la dimension lorsque l’URL elle-même a du sens pour l’analyse (par exemple, pour distinguer les chemins d’accès au réseau CDN ou les versions créatives).

## Mode de remplissage de cette dimension

L’URL de Creative est définie par le lecteur à chaque événement [début de la publicité](/help/implementation/events/ads/ad-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.creativeURL` à un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.ad.creativeURL` mappée) |
| Audience Manager | `c_contextdata.a.media.ad.creativeURL` |

## Éléments de dimension

Chaque élément est la chaîne d’URL littérale signalée au [début de l’annonce](/help/implementation/events/ads/ad-start.md).
