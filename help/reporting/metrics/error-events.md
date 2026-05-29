---
title: Événements d’erreur
description: Comptabilise les événements d’erreur pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# Événements d’erreur

>[!BEGINSHADEBOX]

*Cette page couvre la mesure **Événements d’erreur**. Adobe Analytics renseigne automatiquement une paire [dimension Erreurs](/help/reporting/dimensions/errors.md) à partir de la même variable de données contextuelles `a.media.qoe.errorCount`. Customer Journey Analytics expose un seul champ de `xdm.mediaReporting.qoeDataDetails.errorCount` que vous pouvez utiliser comme dimension ou mesure.*

>[!ENDSHADEBOX]

La mesure **Événements d’erreur** comptabilise les événements d’erreur entre les sessions, adaptés aux sommes, aux moyennes et aux cumuls de centiles. Utilisez la mesure pour calculer le volume total d’erreurs sur une période de rapport et pour comparer les taux d’erreurs sur le contenu, les réseaux ou les lecteurs.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente le décompte à chaque erreur signalée par le lecteur. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.errorCount` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

Pour les rapports booléens au niveau de la session (si une erreur s’est produite), utilisez [Flux impactés par l’erreur](error-impacted-streams.md).
