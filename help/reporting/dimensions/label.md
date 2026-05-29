---
title: Étiquette
description: Indique la maison de disques qui a diffusé le contenu audio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 10%

---


# Étiquette

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Libellé**. Voir [Libellé](/help/implementation/variables/standard-metadata/label.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Libellé** indique le libellé d’enregistrement qui a publié le contenu audio (par exemple, `"Capitol Records"`). Utilisez-le pour comparer l’engagement entre les libellés d’un catalogue de musique ou de podcast.

## Mode de remplissage de cette dimension

Le libellé est défini par le lecteur au début de la session pour le contenu audio.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.label` de données contextuelles lorsque [[!UICONTROL Métadonnées audio]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## Éléments de dimension

Chaque élément correspond au nom du libellé littéral indiqué au début de la session. Utilisez un nom canonique et stable par libellé afin que l’engagement ne se fragmente pas entre les variantes d’orthographe ou d’impression.
