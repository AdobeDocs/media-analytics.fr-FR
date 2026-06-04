---
title: Première date numérique
description: Indique la date à laquelle le contenu s’est affiché pour la première fois sur une plateforme numérique.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# Première date numérique

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Première date numérique**. Voir [Première date numérique](/help/implementation/variables/standard-metadata/first-digital-date.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Première date numérique** indique la date à laquelle le contenu est apparu pour la première fois sur une plateforme numérique. Utilisez-le avec [Date de première diffusion](first-air-date.md) pour comparer le timing de publication numérique à la diffusion originale.

## Mode de remplissage de cette dimension

La première date numérique est définie par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.digitalDate` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Contenu (ID)](content.md) : Adobe crée automatiquement cette classification lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/setup/analytics-reporting.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.digitalDate` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## Approche de classification

Adobe crée automatiquement la première structure numérique de classification de dates lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/setup/analytics-reporting.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque identifiant de contenu et sa première date numérique. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification Première date numérique . Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.digitalDate` à un eVar. Cette approche capture la première date numérique en tant que valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre la première date numérique et la dimension parent [Contenu (ID)](content.md). Si votre implémentation envoie des valeurs incohérentes pour le même ID de contenu à travers les événements, plusieurs premières dates numériques peuvent apparaître sous le même contenu. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément correspond à la chaîne de date littérale signalée au début de la session. Utilisez un format cohérent dans toutes les implémentations. Adobe recommande de `YYYY-MM-DD`.
