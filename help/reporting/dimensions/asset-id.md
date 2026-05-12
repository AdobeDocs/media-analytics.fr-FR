---
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---
﻿---
title: ID de ressource
description: Indique un identifiant de secteur stable pour la ressource de média sous-jacente.
feature: Dimensions
role: User, Admin
---

# ID de ressource

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **ID de ressource**. Voir [ID de ressource](/help/implementation/variables/standard-metadata/asset-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **ID de ressource** indique un identifiant de secteur stable pour la ressource de média sous-jacente (généralement un EIDR, un TMS/Gracenote ou un ID Rovi, mais les identifiants propriétaires sont également acceptés).

## Mode de remplissage de cette dimension

L’ID de ressource est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics (règle de traitement) | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.asset` à un eVar. |
| Adobe Analytics (classification) | Classification de la dimension [Contenu (ID)](content.md) : Adobe crée automatiquement cette classification lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de maintenir les valeurs de classification. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données (règle de traitement) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.asset` mappée) |
| Flux de données (classification) | S.O. — Les flux de données ne prennent pas en charge les classifications. |

## Approche de classification

Adobe crée automatiquement la structure de classification Identifiant de ressource lorsque **[[!UICONTROL Métadonnées vidéo]](/help/reporting/media-reports-enable.md)** est activé pour la suite de rapports. Il vous incombe de renseigner et de gérer la classification à l’aide des [ensembles de classifications](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Cette approche fournit une relation 1:1 garantie entre chaque ID de contenu et son ID de ressource. Les mises à jour de classification s’appliquent rétroactivement à toutes les données historiques de cet identifiant.

>[!IMPORTANT]
>
>Ne modifiez pas le nom de la classification de l’ID de ressource. Si vous la renommez, Adobe peut recréer la classification d’origine, ce qui entraîne un doublon.

## Approche des règles de traitement

Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.asset` à un eVar. Cette approche capture l’ID de ressource sous la forme d’une valeur par accès sans nécessiter de maintenance de la classification.

Le compromis est que vous perdez la relation 1:1 garantie entre l’ID de ressource et la dimension [Contenu (ID)](content.md) parente. Si votre implémentation envoie des valeurs incohérentes pour le même ID de contenu à travers les événements, plusieurs ID de ressource peuvent apparaître sous le même contenu. La mise à jour d’une valeur s’applique uniquement aux données dans le futur.

## Éléments de dimension

Chaque élément est une valeur d’ID d’actif unique signalée pendant la période de rapport. Utilisez un identifiant stable unique par ressource sur toutes les plateformes de distribution afin que le même contenu soit regroupé sur un seul élément de ligne.
