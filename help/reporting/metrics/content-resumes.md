---
title: Reprises du contenu
description: Compte les sessions qui ont repris une lecture précédemment interrompue.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 7%

---


# Reprises du contenu

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Reprises du contenu**. Voir [Reprises du contenu](/help/implementation/variables/core/content-resumes.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Reprises du contenu** comptabilise les sessions qui ont repris une lecture précédemment interrompue. Il est incrémenté lorsque le lecteur marque une session comme reprise sur `sessionStart` (par exemple, après une mise en mémoire tampon, une pause ou un blocage de plus de 30 minutes). Utilisez-le pour séparer les nouvelles sessions authentiques des sessions continues pour la même visionneuse et la même ressource.

## Méthode de calcul de cette mesure

Le serveur principal du média définit `mediaReporting.sessionDetails.hasResume = true` lorsqu’`mediaCollection.sessionDetails.hasResume` est `true` sur l’événement `media.sessionStart`. Le lecteur doit explicitement marquer la session comme reprise. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.resume` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
