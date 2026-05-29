---
title: ID d’élément créatif
description: Indique l’identifiant de la création publicitaire.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 3%

---


# ID d’élément créatif

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Creative ID**. Voir [Creative ID](/help/implementation/variables/ads/creative-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Creative ID** indique l’identifiant de la création publicitaire. Utilisez la dimension pour cumuler l’engagement sur les publicités qui partagent une création.

## Mode de remplissage de cette dimension

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.creative` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Annonce](ad.md) : Adobe crée automatiquement cette classification lorsque **[[!UICONTROL Annonces multimédia]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.ad.creative` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.ad.creative` |

## Approche de classification

Adobe crée automatiquement la structure de classification Creative ID lorsque **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID d’annonce publicitaire et son ID de contenu créatif. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification de l’identifiant Creative. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.creative` à un eVar. Cette approche capture l’ID de contenu créatif sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre l’ID créatif et la dimension [Annonce](ad.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même ID d’annonce publicitaire sur plusieurs événements, plusieurs ID de contenu créatif peuvent apparaître sous la même annonce. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément est un identifiant de contenu créatif unique. Utilisez un identifiant stable par élément créatif afin que le même élément créatif soit reporté sur une seule ligne dans toutes les campagnes.
