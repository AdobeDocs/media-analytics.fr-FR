---
title: Programme
description: Indique le nom du programme ou de la série pour le contenu vidéo qui fait partie d’une série.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

---


# Programme

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Afficher**. Voir [Afficher](/help/implementation/variables/standard-metadata/show.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Afficher** indique le nom du programme ou de la série. Les épisodes de plusieurs saisons se cumulent sur le même élément de ligne d’émission. Utilisez-le donc pour comparer l’engagement tout au long de la durée de vie d’une série.

## Mode de remplissage de cette dimension

Le diaporama est défini par le lecteur au début de la session lorsque le contenu fait partie d’une série.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.show` de données contextuelles lorsque [[!UICONTROL  Métadonnées vidéo ]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Éléments de dimension

Chaque élément correspond au nom d’affichage littéral indiqué au début de la session (par exemple, `"Blinding Light"`). Utilisez des noms stables et distincts par affichage afin que les données ne soient pas réduites dans des programmes non liés qui partagent un mot.
