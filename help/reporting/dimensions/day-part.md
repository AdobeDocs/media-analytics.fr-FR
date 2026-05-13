---
title: Tranche horaire
description: Indique l’intervalle d’heure de la journée (matin, après-midi, heure de grande écoute, tard le soir) auquel le contenu a été diffusé ou lu.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 6%

---


# Tranche horaire

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Jour**. Voir [Tranche horaire](/help/implementation/variables/standard-metadata/day-part.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Partie jour** indique l’intervalle d’heure de la journée auquel le contenu a été diffusé ou lu. Les valeurs courantes sont `"Morning"`, `"Afternoon"`, `"Primetime"` et `"Late Night"`. Utilisez-la pour comparer l’engagement sur plusieurs tranches horaires, indépendamment du fuseau horaire local de la visionneuse.

## Mode de remplissage de cette dimension

La période est définie par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.dayPart` de données contextuelles lorsque [[!UICONTROL &#x200B; Métadonnées vidéo &#x200B;]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videodaypart, post_videodaypart` |

## Éléments de dimension

Chaque élément correspond au libellé de partie de jour littéral indiqué au début de la session. Utilisez un ensemble fixe de valeurs dans toutes les implémentations pour garantir la cohérence des lignes.
