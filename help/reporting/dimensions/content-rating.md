---
title: Classement du contenu
description: Indique l’évaluation de l’audience telle que définie par les directives parentales de TV ou un système d’évaluation régional.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---


# Classement du contenu

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Évaluation du contenu**. Voir [Évaluation du contenu](/help/implementation/variables/standard-metadata/content-rating.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Évaluation du contenu** indique l’évaluation de l’audience pour chaque session. Utilisez-le pour comparer l’engagement et la charge publicitaire entre les niveaux d’évaluation.

## Mode de remplissage de cette dimension

L’évaluation du contenu est définie par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.rating` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Contenu (ID)](content.md) : Adobe crée automatiquement cette classification lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.rating` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |

## Approche de classification

Adobe crée automatiquement la structure de classification de classification Contenu lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque identifiant de contenu et son évaluation. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification de classification de contenu . Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.rating` à un eVar. Cette approche capture l’évaluation du contenu sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre l’évaluation du contenu et la dimension [Contenu (ID)](content.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même ID de contenu à travers les événements, plusieurs évaluations peuvent apparaître sous le même contenu. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond à la valeur d’évaluation littérale signalée au début de la session (par exemple, `"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`). Respectez un ensemble fixe de valeurs par système d&#39;évaluation pour éviter de fragmenter les lignes.
