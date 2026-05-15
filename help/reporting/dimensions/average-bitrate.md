---
title: Débit moyen (dimension)
description: Indique le débit moyen regroupé de chaque session par intervalles de 100 kbit/s.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Débit moyen (dimension)

>[!BEGINSHADEBOX]

*Cette page couvre la dimension **Débit moyen**, qui indique le débit regroupé de chaque session. Voir [Débit binaire moyen (mesure)](/help/reporting/metrics/average-bitrate.md) pour la mesure moyenne pondérée brute. Voir [Débit binaire](/help/implementation/variables/quality/bitrate.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Débit moyen** indique le débit de lecture moyen par session, regroupé par intervalles de 100 kbit/s. Le serveur principal calcule la valeur sous la forme d’une moyenne pondérée de toutes les valeurs de débit de la session, puis l’affecte à un compartiment. Utilisez la dimension pour ventiler l’engagement et la qualité par niveau de débit.

## Mode de remplissage de cette dimension

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.bitrateAverageBucket` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## Éléments de dimension

Chaque élément est un libellé d’intervalle de débit (par exemple, `800-899`, `3200-3299`). Utilisez le [Débit moyen (mesure)](/help/reporting/metrics/average-bitrate.md) pour une valeur moyenne pondérée brute plutôt que pour une dimension regroupée.
