---
title: ID d’erreur du SDK du lecteur
description: Indique les identifiants d’erreur uniques générés par le lecteur de contenu SDK.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# ID d’erreur du SDK du lecteur

La dimension **ID d’erreur du lecteur SDK** signale des identifiants d’erreur uniques générés par le SDK du lecteur de contenu au cours d’une session. Le lecteur doit fournir les codes ou les identifiants au moment de l’implémentation via l’API de suivi des erreurs. Plusieurs ID d’erreur par session sont pris en charge.

## Mode de remplissage de cette dimension

Le lecteur transmet les identifiants d’erreur player-SDK au dispositif de suivi lors des événements [error](/help/implementation/events/error.md). Le serveur principal collecte des identifiants uniques tout au long de la session et les signale lors de l’appel de fermeture.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.qoe.playerSdkErrors` de données contextuelles lorsque la [[!UICONTROL Qualité du média]](/help/reporting/media-reports-enable.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Flux de données | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## Éléments de dimension

Chaque élément est un code d’erreur ou un identifiant généré par le SDK du lecteur. Utilisez une taxonomie stable entre les implémentations afin que les identifiants d’erreur soient correctement cumulés entre les sessions.
