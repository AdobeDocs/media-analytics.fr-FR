---
title: Nom du lecteur de contenu
description: Indique quel lecteur a rendu chaque session multimédia.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 6%

---


# Nom du lecteur de contenu

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de compte rendu des performances **Nom du lecteur de contenu**. Voir [Nom du lecteur de contenu](/help/implementation/variables/core/content-player-name.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Nom du lecteur de contenu** indique le lecteur qui a rendu chaque session multimédia (par exemple, `HTML5 Player`, `Brightcove` ou `Roku Player`). Utilisez-le pour comparer l’engagement, la réalisation et la qualité entre les acteurs d’une même propriété.

## Mode de remplissage de cette dimension

Le nom du lecteur est défini par le lecteur au début de la session et persiste pendant toute la durée de la session. La valeur est envoyée sur chaque événement et signalée dans Adobe Analytics et Customer Journey Analytics.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.playerName` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>Si le nom du lecteur n’est pas défini, la dimension n’est pas renseignée pour cette session. Les sessions sans nom de lecteur ne peuvent pas être divisées par lecteur dans les rapports.

## Éléments de dimension

Chaque élément correspond à la chaîne littérale définie au début de la session. Utilisez un nom stable et distinct par lecteur afin que les données de différents lecteurs ne soient pas réduites en un seul élément de ligne.
