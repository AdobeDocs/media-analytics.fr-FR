---
title: Nom du chapitre
description: Affiche le titre du chapitre lisible par l’utilisateur.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---


# Nom du chapitre

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Nom du chapitre**. Voir [Nom du chapitre](/help/implementation/variables/chapters/chapter-name.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Nom du chapitre** affiche le titre lisible par l’utilisateur de chaque chapitre (par exemple, `"Pilot Episode - Opening"`).

## Mode de remplissage de cette dimension

Le nom du chapitre est défini par le lecteur à chaque événement [début du chapitre](/help/implementation/events/chapters/chapter-start.md).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.friendlyName` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Chapitres](chapter.md) : Adobe crée automatiquement cette classification lorsque l’option **[[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.friendlyName`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.chapter.friendlyName` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.chapter.friendlyName` |

## Approche de classification

Adobe crée automatiquement la structure de classification Nom du chapitre lorsque l’option **[[!UICONTROL Chapitres de médias]](/help/reporting/media-reports-enable.md)** est activée pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID de chapitre et son nom convivial. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification du chapitre. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.chapter.friendlyName` à un eVar. Cette approche capture le nom convivial sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre le nom du chapitre et la dimension [Chapitre](chapter.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même ID de chapitre à travers les événements, plusieurs noms peuvent apparaître sous le même chapitre. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond au titre de chapitre littéral indiqué au [début du chapitre](/help/implementation/events/chapters/chapter-start.md).
