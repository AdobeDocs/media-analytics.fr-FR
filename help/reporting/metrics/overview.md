---
title: Présentation des mesures de streaming multimédia
description: Découvrez comment les mesures de médias en flux continu sont calculées et organisées dans Adobe Analytics et Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---


# Présentation des mesures de streaming multimédia

Les mesures dans Streaming Media Analytics sont des nombres et des durées pilotés par les événements calculés par le serveur principal des médias. Le lecteur multimédia envoie des événements tels que le début de la session, la lecture, le ping et le démarrage de l’annonce publicitaire ; le serveur principal du média traite ces événements et finalise les valeurs de mesure lors de l’appel de fermeture de la session.

## Méthode de calcul des mesures

Les mesures de médias en flux continu suivent quatre modèles de calcul principaux :

* **Indicateurs déclenchés par un événement** : définissez la première fois qu’un événement éligible arrive dans une session. Un événement [`play`](/help/implementation/events/playback/play.md) pour le contenu principal définit l’indicateur [[!UICONTROL Content starts]](content-starts.md) ; un événement [`adStart`](/help/implementation/events/ads/ad-start.md) définit [[!UICONTROL Ad starts]](ad-starts.md). L’indicateur est signalé une fois par session lors de l’appel de fermeture, et non par événement.

* **Durées cumulées** : additionne les intervalles entre les événements ping pendant qu’un état de lecture particulier est actif. [[!UICONTROL Temps passé sur le contenu]](content-time-spent.md) s’accumule pendant la lecture du contenu principal ; [[!UICONTROL Temps passé sur la publicité]](ad-time-spent.md) s’accumule pendant la lecture d’une publicité. L’intervalle ping recommandé par Adobe est de 10 secondes pour le contenu principal et de 1 seconde pendant les publicités. Par conséquent, les mesures de durée de la visite ne peuvent être aussi granulaires que l’intervalle ping de votre implémentation.

* **Nombre d’événements** : suivez le nombre total d’occurrences dans la session. Les mesures de qualité telles que [[!UICONTROL Événements de mémoire tampon]](buffer-events.md), [[!UICONTROL Modifications de débit]](bitrate-changes.md), [[!UICONTROL Événements d’erreur]](error-events.md) et [[!UICONTROL Événements de pause]](pause-events.md) comptabilisent chaque occurrence, pas seulement la première.

* **Flux impactés** : les indicateurs au niveau de la session sont définis sur 1 si l’événement correspondant s’est produit à tout moment au cours de la session, quel que soit le nombre de fois. Utilisez ces mesures pour mesurer la portée, tout en utilisant la mesure du nombre d’événements pour mesurer la gravité. Par exemple, vous pouvez utiliser [[!UICONTROL Mettre en mémoire tampon les flux impactés]](buffer-impacted-streams.md) pour déterminer la proportion de sessions qui ont été impactées par la mise en mémoire tampon sur toutes les sessions de lecture.

## Disponibilité par système de reporting

| Système de reporting | Comment les mesures arrivent |
| --- | --- |
| Adobe Analytics | Renseigné à l’aide de [Variables de données contextuelles](https://experienceleague.adobe.com/fr/docs/analytics/implementation/vars/page-vars/contextdata). Certaines mesures renseignent automatiquement les événements de solution à l’aide de ces variables de données contextuelles, tandis que d’autres doivent être mappées à un événement personnalisé à l’aide de [règles de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). Les mesures qui renseignent automatiquement les valeurs doivent d’abord activer leur [paramètre de suite de rapports Streaming Media](../setup/analytics-reporting.md) respectif. |
| Customer Journey Analytics | Champs XDM dans les nœuds `xdm.mediaReporting.sessionDetails` et associés, provenant de n’importe quel jeu de données qui inclut des données de médias en flux continu. Vous devez créer chaque mesure avec les paramètres souhaités dans [Paramètres des composants de la vue de données](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Flux de données | Les mesures apparaissent dans les colonnes `event_list` et `post_event_list` sous la forme d’identifiants d’événement. Chaque fichier de flux contient un fichier `events.csv` contenant la recherche de toutes les mesures, y compris les mesures des médias en flux continu. |

>[!MORELIKETHIS]
>
>* [Présentation des événements](/help/implementation/events/overview.md) : événements du lecteur qui renseignent les mesures
>* [Présentation des variables](/help/implementation/variables/overview.md) : données que les événements transmettent à Adobe
>* [Présentation des dimensions](/help/reporting/dimensions/overview.md) : dimensions de rapport renseignées par les variables
