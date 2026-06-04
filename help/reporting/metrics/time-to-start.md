---
title: Heure de début (mesure)
description: Indique le temps de démarrage pour les sommes et les moyennes entre les sessions.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 7%

---


# Heure de début (mesure)

>[!BEGINSHADEBOX]

*Cette page couvre la mesure **Heure de début**. Adobe Analytics renseigne automatiquement une paire [Heure de début (dimension)](/help/reporting/dimensions/time-to-start.md) à partir de la même variable de données contextuelles `a.media.qoe.timeToStart`. Customer Journey Analytics expose un seul champ de `xdm.mediaReporting.qoeDataDetails.timeToStart` que vous pouvez utiliser comme dimension ou mesure. Voir [Heure de début](/help/implementation/variables/quality/time-to-start.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Temps de démarrage** indique le temps de démarrage entre les sessions, qui convient aux cumuls de sommes, de moyennes et de centiles. Utilisez la mesure pour calculer le temps de démarrage moyen sur une période de rapport et pour comparer les performances de démarrage sur le contenu, les réseaux ou les lecteurs. Adobe stocke la valeur en secondes et la convertit lors de l’ingestion à partir des millisecondes signalées par le lecteur.

## Méthode de calcul de cette mesure

Le lecteur définit le `timeToStart` sur l’objet QoE avant le déclenchement du démarrage de la session. Le serveur principal signale la valeur lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.timeToStart` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/setup/analytics-reporting.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
