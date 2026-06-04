---
title: Marqueurs de progression
description: Comptez les sessions dont le curseur de lecture a dépassé chacun des cinq seuils fixes (10 %, 25 %, 50 %, 75 % et 95 %).
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 9%

---


# Marqueurs de progression

Les **marqueurs de progression** sont cinq mesures distinctes qui comptabilisent les sessions dont le curseur de lecture a dépassé chacun des cinq seuils fixes (10 %, 25 %, 50 %, 75 % et 95 % de la longueur du contenu). Utilisez-les pour représenter graphiquement le taux de déperdition sur l’exécution du contenu ; associez-les à [démarrages de contenu](content-starts.md) pour calculer le nombre de sessions démarrées ayant atteint chaque jalon.

Chaque marqueur se déclenche une fois par session et n’est pas redéclenché lors de la recherche vers l’arrière. Les marqueurs ignorés lors de la recherche vers l’avant ne sont pas comptabilisés (par exemple, une visionneuse qui passe de 5 % à 60 % déclenche les marqueurs 10 %, 25 % et 50 % en même temps).

## Méthode de calcul de chaque marqueur

Le serveur principal du média évalue le curseur de lecture signalé par rapport à [Longueur du contenu](../dimensions/content-length.md) après chaque événement. Lorsque le curseur de lecture dépasse un seuil pour la première fois, l’indicateur correspondant est défini pour le reste de la session. Les cinq marqueurs sont signalés au moment de la fermeture. Les sessions qui ne produisent jamais d’événement de lecture sur le contenu principal (comme [Dépose avant le début](/help/reporting/metrics/drops-before-start.md)) ne font jamais avancer le curseur de lecture au-delà d’un seuil ; aucun marqueur n’est donc défini.

>[!IMPORTANT]
>
>Les marqueurs de progression nécessitent une longueur de contenu [non nulle](/help/reporting/dimensions/content-length.md) et un compte rendu des performances du curseur de lecture précis. Si la longueur du contenu n’est pas définie, nulle ou incorrecte, les marqueurs peuvent se déclencher au mauvais moment ou pas du tout.

### Marque de progression de 10 % {#progress-10}

Se déclenche lorsque le curseur de lecture atteint pour la première fois 10 % de la longueur du contenu.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.progress10` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress10` |

### Marque de progression de 25 % {#progress-25}

Se déclenche lorsque le curseur de lecture atteint pour la première fois 25 % de la longueur du contenu.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.progress25` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress25` |

### Marqueur de progression de 50 % {#progress-50}

Se déclenche lorsque le curseur de lecture atteint 50 % de la longueur du contenu pour la première fois.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.progress50` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress50` |

### Marqueur de progression de 75 % {#progress-75}

Se déclenche lorsque le curseur de lecture atteint 75 % de la longueur du contenu pour la première fois.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.progress75` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress75` |

### Marque de progression de 95 % {#progress-95}

Se déclenche lorsque le curseur de lecture atteint pour la première fois 95 % de la longueur du contenu.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.progress95` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress95` |
