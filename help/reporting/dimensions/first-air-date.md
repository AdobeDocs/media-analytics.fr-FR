---
title: Date de première diffusion
description: Indique la date de première diffusion du contenu à la télévision.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# Date de première diffusion

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Première diffusion**. Voir [Date de première diffusion](/help/implementation/variables/standard-metadata/first-air-date.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Première diffusion** indique la date à laquelle le contenu a été diffusé pour la première fois à la télévision. Utilisez-la pour séparer l’engagement sur les nouvelles versions de l’engagement sur les anciens contenus.

## Mode de remplissage de cette dimension

La date de première diffusion est définie par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.airDate` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Contenu (ID)](content.md) : Adobe crée automatiquement cette classification lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.airDate` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.airDate` |

## Approche de classification

Adobe crée automatiquement la structure de classification Date de première diffusion lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque identifiant de contenu et sa première date de diffusion. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification Date de première diffusion . Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.airDate` à un eVar. Cette approche capture la première date de diffusion sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre la première date de diffusion et la dimension parent [Contenu (ID)](content.md). Si votre implémentation envoie des valeurs incohérentes pour le même ID de contenu sur plusieurs événements, plusieurs dates de première diffusion peuvent apparaître sous le même contenu. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond à la chaîne de date littérale signalée au début de la session. Utilisez un format cohérent dans toutes les implémentations. Adobe recommande de `YYYY-MM-DD`.
