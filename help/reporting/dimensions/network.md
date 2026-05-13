---
title: Réseau
description: Indique le nom du réseau ou du canal de diffusion.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 9%

---


# Réseau

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Réseau**. Voir [Network](/help/implementation/variables/standard-metadata/network.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Réseau** indique le nom du réseau ou du canal de diffusion (par exemple, `"Fox"` ou `"ESPN"`). Utilisez-la pour comparer l’engagement sur plusieurs réseaux au sein de la même propriété de diffusion en continu.

## Mode de remplissage de cette dimension

Le réseau est défini par le lecteur au démarrage de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.network` de données contextuelles lorsque [[!UICONTROL  Métadonnées vidéo ]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videonetwork, post_videonetwork` |

## Éléments de dimension

Chaque élément correspond à la valeur réseau littérale signalée au début de la session. Utilisez un nom stable et distinct par réseau afin que les données ne se fragmentent pas entre les variantes orthographiques.
