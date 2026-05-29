---
title: Longueur du chapitre
description: Indique la durée de chaque chapitre.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# Longueur du chapitre

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **longueur du chapitre**. Voir [Longueur du chapitre](/help/implementation/variables/chapters/chapter-length.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Longueur du chapitre** indique la durée de chaque chapitre, en secondes.

## Mode de remplissage de cette dimension

La longueur du chapitre est définie par le lecteur à chaque événement [début du chapitre](/help/implementation/events/chapters/chapter-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.length` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Chapitres](chapter.md) : Adobe crée automatiquement cette classification lorsque l’option **[[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.length`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.chapter.length` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.chapter.length` |

## Approche de classification

Adobe crée automatiquement la structure de classification Longueur du chapitre lorsque l’option **[[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID de chapitre et sa longueur. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification Longueur du chapitre . Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.length` à un eVar. Cette approche capture la longueur du chapitre en tant que valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre la longueur du chapitre et la dimension [Chapitre](chapter.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même ID de chapitre à travers les événements, plusieurs longueurs peuvent apparaître sous le même chapitre. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond à la valeur de longueur entière, en secondes, indiquée au [début du chapitre](/help/implementation/events/chapters/chapter-start.md).
