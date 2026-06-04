---
title: Position du chapitre
description: Indique l’index de chaque chapitre dans le contenu.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Position du chapitre

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Position du chapitre**. Voir [Position du chapitre](/help/implementation/variables/chapters/chapter-position.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Position du chapitre** indique l’index de chaque chapitre dans le contenu.

## Mode de remplissage de cette dimension

La position du chapitre est définie par le lecteur à chaque événement [début du chapitre](/help/implementation/events/chapters/chapter-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.position` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Chapitres](chapter.md) : Adobe crée automatiquement cette classification lorsque l’option **[[!UICONTROL Chapitres de médias]](/help/reporting/setup/analytics-reporting.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.index`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.chapter.position` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.chapter.position` |

## Approche de classification

Adobe crée automatiquement la structure de classification des positions de chapitre lorsque l’option **[[!UICONTROL Chapitres de médias]](/help/reporting/setup/analytics-reporting.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID de chapitre et sa position. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification des postes du chapitre. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.position` à un eVar. Cette approche capture la position du chapitre sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre la position du chapitre et la dimension [Chapitre](chapter.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même ID de chapitre à travers les événements, plusieurs positions peuvent apparaître sous le même chapitre. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément est la valeur de position entière indiquée au [début du chapitre](/help/implementation/events/chapters/chapter-start.md).
