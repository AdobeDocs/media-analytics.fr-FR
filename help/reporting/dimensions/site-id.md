---
title: ID du site
description: Indique l’identifiant du site publicitaire pour chaque publicité.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# ID du site

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Identifiant de site**. Voir [Identifiant de site](/help/implementation/variables/ads/site-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Identifiant du site** indique l’identifiant du site publicitaire (généralement un identifiant de votre plateforme de serveur de publicités). Utilisez la dimension pour ventiler l’engagement par site d’emplacement publicitaire.

## Mode de remplissage de cette dimension

L’identifiant du site est défini par le lecteur à chaque événement [début de la publicité](/help/implementation/events/ads/ad-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.site` à un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.ad.site` mappée) |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## Éléments de dimension

Chaque élément correspond à la valeur de l’identifiant de site littéral indiquée au [début de la publicité](/help/implementation/events/ads/ad-start.md).
