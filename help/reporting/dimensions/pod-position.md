---
title: Position de la capsule
description: Indique le décalage de chaque coupure publicitaire dans le contenu.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# Position de la capsule

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de rapport **Position de la capsule**. Voir [Heure de début de la coupure publicitaire](/help/implementation/variables/ads/ad-break-start-time.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Position de la capsule** indique le décalage de chaque coupure publicitaire dans le contenu, en secondes. Un pre-roll a une position `0` ; les mid-rolls ont des positions correspondant à leur heure de début de lecture.

## Mode de remplissage de cette dimension

La position du pod est définie à partir de la valeur [Heure de début de la coupure publicitaire](/help/implementation/variables/ads/ad-break-start-time.md) définie par le lecteur sur [Début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.podSecond` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [capsule publicitaire](ad-pod.md) : Adobe crée automatiquement cette classification lorsque **[[!UICONTROL Annonces publicitaires]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.ad.podSecond` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.ad.podSecond` |

## Approche de classification

Adobe crée automatiquement la structure de classification de position de capsule lorsque la fonction **[[!UICONTROL Publicités médias]](/help/reporting/media-reports-enable.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID de capsule publicitaire et sa position. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification de position de la capsule. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.ad.podSecond` à un eVar. Cette approche capture la position de la capsule en tant que valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre la position de la capsule et la dimension parent [capsule publicitaire](ad-pod.md). Si votre implémentation envoie des valeurs incohérentes pour le même ID de capsule entre les événements, plusieurs positions peuvent apparaître sous la même capsule publicitaire. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond à la valeur de décalage entière (en secondes) signalée au [début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md).
