---
title: Flux impactés par l’image dans l’image
description: Comptabilise les sessions au cours desquelles la visionneuse a effectué au moins une saisie image par image.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---


# Flux impactés par l’image dans l’image

>[!BEGINSHADEBOX]

*Cette page couvre la mesure de reporting **Flux affectés par l’image dans l’image**. Voir [Image dans l’image](/help/implementation/variables/player-state/picture-in-picture.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La mesure **Flux affectés par image dans image** comptabilise les sessions au cours desquelles la visionneuse a effectué au moins une lecture d’image dans image. La mesure est un booléen au niveau de la session : plusieurs entrées image par image dans le même nombre de sessions qu’un flux affecté. Pour le volume total d&#39;entrée image dans image, utilisez [Image dans le nombre d&#39;images](picture-in-picture-count.md).

## Méthode de calcul de cette mesure

Le serveur principal du média définit cet indicateur la première fois qu’un événement de début d’état image dans image est reçu au cours de la session. La mesure est signalée lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.states.pictureinpicture.set` de données contextuelles lorsque le [[!UICONTROL suivi de l’état du lecteur]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) l’entrée où `name = "pictureInPicture"`, champ `isSet` |
| Flux de données | `event_list`, `post_event_list` (voir Recherche de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
