---
title: Créateur
description: Indique le créateur ou le studio de production du contenu.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---


# Créateur

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Auteur**. Voir [Originator](/help/implementation/variables/standard-metadata/originator.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Originateur** indique le créateur ou le studio de production du contenu (par exemple, `"Warner Brothers"` ou `"Sony"`). Utilisez-le pour comparer l’engagement entre les propriétaires de contenu ou les titulaires de droits.

## Mode de remplissage de cette dimension

L’initiateur est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.originator` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Contenu (ID)](content.md) : Adobe crée automatiquement cette classification lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/setup/analytics-reporting.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.originator` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.originator` |

## Approche de classification

Adobe crée automatiquement la structure de classification d’origine lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/setup/analytics-reporting.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID de contenu et son auteur. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification de l&#39;expéditeur. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.originator` à un eVar. Cette approche capture l’initiateur sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre l’initiateur et la dimension [Contenu (ID)](content.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même ID de contenu à travers les événements, plusieurs personnes d’origine peuvent apparaître sous le même contenu. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément est la valeur d’origine littérale signalée au début de la session. Utilisez un nom stable et distinct par studio afin que l’engagement ne se réduise pas entre des entités non liées.
