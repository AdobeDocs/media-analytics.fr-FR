---
title: Format du flux
description: Indique le niveau de qualité de chaque session (généralement HD ou SD).
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Format du flux

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Format de flux**. Voir [Format de flux](/help/implementation/variables/standard-metadata/stream-format.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Format du flux** indique le niveau de qualité de chaque session (généralement `"HD"` ou `"SD"`, mais toute chaîne est acceptée). Utilisez-le pour comparer l’engagement, la réalisation et la qualité entre les niveaux de qualité de la diffusion.

## Mode de remplissage de cette dimension

Le format du flux est défini par le lecteur au début de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.format` à un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.format` mappée) |
| Audience Manager | `c_contextdata.a.media.format` |

## Éléments de dimension

Chaque élément correspond à la valeur de format littéral signalée au début de la session. Utilisez un ensemble stable de valeurs (`HD`, `SD`, `4K`, `UHD`) afin que les éléments de ligne ne se fragmentent pas entre les variations d’orthographe.
