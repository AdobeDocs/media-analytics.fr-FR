---
title: Audience moyenne par minute
description: Indique le nombre moyen de spectateurs et spectatrices qui regardent à une minute donnée au cours de l’exécution du contenu.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%

---


# Audience moyenne par minute

La mesure **Audience moyenne par minute** indique le nombre moyen de spectateurs et spectatrices qui regardent à une minute donnée sur l’exécution du contenu. Il s’agit de la mesure « AMA » standard utilisée pour comparer la portée multimédia sur un contenu de différentes longueurs.

## Méthode de calcul de cette mesure

Le serveur principal des médias calcule l’audience moyenne par minute par session en tant que `Content time spent / Content length`. Lorsqu’il est additionné entre les sessions, le total représente la taille moyenne de l’audience à chaque minute du contenu. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.averageMinuteAudience` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>L’audience moyenne par minute nécessite une valeur différente de zéro [Longueur du contenu](/help/reporting/dimensions/content-length.md). Si la longueur du contenu n’est pas définie ou si elle est nulle, cette mesure n’est pas générée pour la session.
