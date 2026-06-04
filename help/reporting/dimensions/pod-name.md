---
title: Nom de la capsule
description: Indique le nom convivial de chaque coupure publicitaire. Collectez-les dans Adobe Analytics à l’aide d’une classification ou d’une règle de traitement personnalisée.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Nom de la capsule

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de création de rapports **Nom du pod**. Voir [Nom de la coupure publicitaire](/help/implementation/variables/ads/ad-break-name.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Nom de la capsule** indique le nom convivial de chaque coupure publicitaire (par exemple, `"pre-roll"`, `"mid-roll-1"`). Dans Customer Journey Analytics, il s’agit d’une dimension discrète renseignée directement à partir de la variable d’implémentation. Dans Adobe Analytics, elle est disponible selon deux approches : une classification de la dimension [capsule publicitaire](ad-pod.md) ou une eVar renseignée à l’aide d’une règle de traitement.

## Mode de remplissage de cette dimension

Le nom du pod provient de la valeur [Nom de la coupure publicitaire](/help/implementation/variables/ads/ad-break-name.md) que le lecteur définit sur [Début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.podFriendlyName` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension Capsule : Adobe crée automatiquement cette classification lorsque la **[[!UICONTROL Publicités médias]](/help/reporting/setup/analytics-reporting.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.ad.podFriendlyName` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.ad.podFriendlyName` |

## Approche de classification

Adobe crée automatiquement la structure de classification de nom de capsule lorsque **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche offre une relation 1:1 garantie entre chaque identifiant de capsule et son nom convivial. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification du nom de la capsule. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.podFriendlyName` à un eVar. Cette approche capture le nom convivial sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre le nom de la capsule et la dimension parent [capsule publicitaire](ad-pod.md). Si votre implémentation envoie des valeurs incohérentes pour le même identifiant de capsule sur plusieurs événements, plusieurs noms peuvent apparaître sous la même capsule publicitaire. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond au nom littéral de la coupure publicitaire indiqué au [début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md).
