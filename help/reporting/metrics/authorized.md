---
title: Autorisé
description: Comptabilise les sessions dont l’utilisateur a été autorisé via Adobe Pass.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 12%

---


# Autorisé

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Autorisé**. Voir [Autorisé](/help/implementation/variables/standard-metadata/authorized.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Autorisé** comptabilise les sessions dont l’utilisateur a été autorisé via Adobe Pass ou TV-Everywhere. Associez à la dimension [&#128279;](/help/reporting/dimensions/mvpd.md) pour ventiler le volume d&#39;authentification par fournisseur.

## Méthode de calcul de cette mesure

Le serveur principal du média incrémente le nombre lorsque le lecteur marque la session comme autorisée au début de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pass.auth` de données contextuelles lorsque [[!UICONTROL &#x200B; Métadonnées vidéo &#x200B;]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/fr/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
