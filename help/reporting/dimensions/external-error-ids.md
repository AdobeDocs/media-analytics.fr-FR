---
title: ID d'erreurs externes
description: Signale les identifiants d’erreur uniques provenant de sources externes telles que les erreurs CDN.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 7%

---


# ID d&#39;erreurs externes

La dimension **ID d’erreur externes** signale des identifiants d’erreur uniques provenant de n’importe quelle source en dehors du SDK du lecteur (par exemple, les erreurs CDN). Le lecteur doit fournir les codes ou les identifiants au moment de l’implémentation via l’API de suivi des erreurs. Plusieurs ID d’erreur par session sont pris en charge.

## Mode de remplissage de cette dimension

Le lecteur transmet les identifiants d’erreur externes au dispositif de suivi lors des événements [error](/help/implementation/events/error.md). Le serveur principal collecte des identifiants uniques tout au long de la session et les signale lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.externalErrors` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoeextneralerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.externalErrors` |

## Éléments de dimension

Chaque élément est un code d’erreur ou un identifiant fourni par le lecteur. Utilisez une taxonomie stable entre les implémentations afin que les identifiants d’erreur soient correctement cumulés entre les sessions.
