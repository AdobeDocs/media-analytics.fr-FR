---
title: Auteur
description: Indique l’auteur du contenu. Principalement utilisé pour les livres audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 10%

---


# Auteur

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Auteur**. Voir [Auteur](/help/implementation/variables/standard-metadata/author.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Auteur** indique l’auteur du contenu (par exemple, `"Eleanor Clementine"`). Principalement utilisé pour les livres audio, mais également valable pour les podcasts dont l&#39;hôte ou le producteur est l&#39;attribution pertinente.

## Mode de remplissage de cette dimension

L’auteur est défini par le lecteur au début de la session pour le contenu audio.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.author` de données contextuelles lorsque [[!UICONTROL Métadonnées audio]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoaudioauthor` |

## Éléments de dimension

Chaque élément correspond au nom littéral de l’auteur indiqué au début de la session.
