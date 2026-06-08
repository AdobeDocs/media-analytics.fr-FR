---
title: Décalage de chapitre
description: Indique le décalage de chaque chapitre dans le contenu.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---


# Décalage de chapitre

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Décalage de chapitre**. Voir [Décalage de chapitre](/help/implementation/variables/chapters/chapter-offset.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Décalage du chapitre** indique le décalage de chaque chapitre à l’intérieur du contenu, mesuré en secondes depuis le début.

## Mode de remplissage de cette dimension

Le décalage de chapitre est défini par le lecteur à chaque événement [début du chapitre](/help/implementation/events/chapters/chapter-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.offset` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Chapitre](chapter.md). Adobe crée automatiquement cette classification lorsque l’option **[[!UICONTROL Chapitres de médias]](/help/reporting/setup/analytics-reporting.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.chapter.offset` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.chapter.offset` |

## Approche de classification

Adobe crée automatiquement la structure de classification Décalage de chapitre lorsque l’option **[[!UICONTROL Chapitres de média]](/help/reporting/setup/analytics-reporting.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID de chapitre et son décalage. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification Décalage de chapitre. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.offset` à un eVar. Cette approche capture le décalage de chapitre en tant que valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre le décalage de chapitre et la dimension [Chapitre](chapter.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même identifiant de chapitre à travers les événements, plusieurs décalages peuvent apparaître sous le même chapitre. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond à la valeur de décalage entière, en secondes, indiquée au [début du chapitre](/help/implementation/events/chapters/chapter-start.md).
