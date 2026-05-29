---
title: Présentation des dimensions de streaming multimédia
description: Découvrez comment les dimensions des médias en flux continu sont renseignées et organisées dans Adobe Analytics et Customer Journey Analytics.
feature: Dimensions
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# Présentation des dimensions de streaming multimédia

Les dimensions dans Streaming Media Analytics vous permettent de segmenter et de filtrer les mesures par nom de contenu, type de flux, nom publicitaire et des dizaines d’autres attributs. La plupart sont définies par le lecteur au début de la session et poursuivies jusqu’à la fermeture de la session.

## Mode de remplissage des dimensions

Les dimensions Streaming Media suivent trois schémas de population principaux :

* **Fourni par le lecteur multimédia** : source de la majorité des dimensions. Le lecteur envoie ces valeurs dans l’appel [Début de session](/help/implementation/events/session/session-start.md) et le serveur principal du média les joint à chaque événement suivant de la session. Ce que le lecteur envoie au début de la session est ce qui apparaît dans les rapports. Par exemple, [[!UICONTROL Type de flux]](/help/reporting/dimensions/stream-type.md), [[!UICONTROL Nom du contenu]](/help/reporting/dimensions/content-name.md) et [[!UICONTROL Longueur du contenu]](/help/reporting/dimensions/content-length.md).

* **Valeurs dérivées** : dimensions que le serveur principal du média calcule à partir de l’état de lecture accumulé plutôt que de lire une valeur fournie par le lecteur. Le [[!UICONTROL segment de contenu]](/help/reporting/dimensions/content-segment.md) est calculé à partir de la position de la tête de lecture au cours de la lecture. [[!UICONTROL Chemin d’accès au média]](/help/reporting/dimensions/media-path.md) suit les transitions entre les états de contenu et d’annonce publicitaire tout au long de la session. Ces dimensions ne peuvent pas être remplacées par le lecteur.

* **Classifications** : facultatif. Au lieu de renseigner des dimensions distinctes, vous pouvez gérer les données de classification à l’aide de [Jeux de classifications](https://experienceleague.adobe.com/fr/docs/analytics/components/classifications/sets/overview) (Adobe Analytics) ou [Jeux de données de recherche](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) (Customer Journey Analytics).

## Disponibilité par système de reporting

| Système de reporting | Comment les dimensions arrivent |
| --- | --- |
| Adobe Analytics | Renseigné à l’aide de [Variables de données contextuelles](https://experienceleague.adobe.com/fr/docs/analytics/implementation/vars/page-vars/contextdata). Certaines dimensions renseignent automatiquement les dimensions à l’aide de ces variables de données contextuelles, tandis que d’autres doivent être renseignées à l’aide de [Règles de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). Les dimensions qui renseignent automatiquement les valeurs doivent d’abord activer leur [paramètre de suite de rapports Streaming Media](../../implementation/media-sdk/setup/media-reports-enable.md) respectif. |
| Customer Journey Analytics | Les champs XDM sont généralement en `xdm.mediaReporting.sessionDetails`, provenant de tout jeu de données qui inclut des données de médias en flux continu. Vous devez créer chaque dimension avec les paramètres souhaités dans [Paramètres des composants de la vue de données](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Flux de données | Les dimensions automatiquement renseignées possèdent leurs propres noms de colonne de flux de données (par exemple `videostreamtype`, `videoname` ou `videolength`). Les dimensions qui nécessitent des règles de traitement utilisent des noms de colonne `evar`. |
| Audience Manager | Données contextuelles transférées depuis Adobe Analytics. Disponible uniquement lorsque le transfert côté serveur d’Analytics vers Audience Manager est configuré. |

>[!MORELIKETHIS]
>
>* [Présentation des mesures](../metrics/overview.md) : référence sur les mesures des médias en flux continu
>* [Mappage des paramètres](/help/implementation/parameters-mapping.md) : complète référence de variable à colonne à XDM.
>* [Segments de médias](/help/reporting/segments.md) : segments intégrés qui utilisent des dimensions de médias en flux continu
