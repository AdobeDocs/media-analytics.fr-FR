---
title: Données fédérées
description: Comptabilise les sessions reçues par le biais d’un partage de données fédéré plutôt que la propre mise en œuvre d’un client.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# Données fédérées

>[!AVAILABILITY]
>
>Le service Federated Analytics est disponible uniquement lors de l’utilisation de fonctionnalités de streaming multimédia avec Adobe Analytics. Federated Analytics n’est pas disponible dans Customer Journey Analytics.

La mesure **Données fédérées** comptabilise les sessions reçues par l’intermédiaire d’un partage de données fédérées plutôt qu’à partir de votre propre mise en œuvre. Utilisez-le pour mesurer le volume des sessions partagées par le partenaire et comparer l’engagement, l’achèvement ou la qualité par rapport aux sessions propriétaires.

Voir le cas d’utilisation [Federated Media](/help/use-cases/federated-media.md) pour plus d’informations.

>[!TIP]
>
>Si vous souhaitez utiliser les données fédérées en tant que dimension, créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe la variable de données contextuelles `a.media.federated` à une eVar.

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur lorsque la session arrive sur un canal fédéré. La mesure est incrémentée une fois par session de qualification et est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.federated` de données contextuelles lorsque [[!UICONTROL  Métadonnées vidéo ]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.federated` |
