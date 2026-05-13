---
title: Type de diffusion
description: Capture si chaque session multimédia était du contenu audio ou vidéo.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 5%

---


# Type de diffusion

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Type de flux**. Voir [Type de flux](/help/implementation/variables/core/stream-type.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Type de flux** capture si chaque session multimédia était du contenu audio ou vidéo. Elle est disponible dans Adobe Analytics une fois que [Media Core est activé](/help/reporting/media-reports-enable.md) pour la suite de rapports et dans Customer Journey Analytics pour tout jeu de données qui inclut des données de médias en flux continu.

## Mode de remplissage de cette dimension

Le type de flux est défini par le lecteur au début de la session et transmis jusqu’à l’appel de fermeture de la session. Elle n’est ni calculée ni dérivée. La valeur signalée correspond exactement à ce qui a été envoyé lors de la collecte.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.streamType` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videostreamtype` |

>[!IMPORTANT]
>
>Si le type de flux n’est pas défini, la dimension n’est pas renseignée pour cette session. Ces sessions sont exclues des segments Audio uniquement et Vidéo intégrés et le segment Tous les médias en flux continu sera sous-comptabilisé s’il est utilisé avec des répartitions de type de flux.

## Éléments de dimension

| Valeur | Description |
| --- | --- |
| `video` | La session était consacrée au contenu vidéo. |
| `audio` | La session comportait du contenu audio tel qu’un podcast, un livre audio ou un flux musical. |

Les valeurs personnalisées sont techniquement acceptées par les API de collection, mais ne sont pas recommandées. Elles ne correspondent pas aux segments intégrés décrits ci-dessous et peuvent entraîner des incohérences dans les rapports entre les implémentations.

## Segments recommandés

Le type de diffusion est la base des segments intégrés [!UICONTROL Type de diffusion multimédia] d’Adobe Analytics. Utilisez ces segments pour étendre tout rapport de média en flux continu à un type de contenu spécifique :

| Segment | Composants de |
| --- | --- |
| [!UICONTROL Tous les médias en flux continu] | Le contenu (ID) existe |
| [!UICONTROL Audio uniquement] | Contenu (ID) présent ET type de flux = `audio` |
| [!UICONTROL Vidéo uniquement] | Contenu (ID) présent ET type de flux != `audio` |

>[!TIP]
>
>Le segment [!UICONTROL Vidéo uniquement] utilise une règle de `!=` plutôt que des `= video` pour capturer correctement les sessions où le type de flux peut avoir été défini sur une valeur personnalisée qui n’est pas `audio`.
