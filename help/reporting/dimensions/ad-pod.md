---
title: Capsule publicitaire
description: Indique chaque coupure publicitaire unique, indexée par un identifiant de capsule généré automatiquement.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# Capsule publicitaire

La dimension **capsule publicitaire** signale chaque coupure publicitaire unique, indexée par un identifiant de capsule généré automatiquement. Chaque publicité d’une session appartient à une capsule publicitaire parente, qui regroupe plusieurs publicités lues à la suite. Utilisez la dimension pour ventiler l’engagement par coupure publicitaire et comme clé de jointure pour les classifications [Nom de la capsule](pod-name.md) et [Position de la capsule](pod-position.md).

## Mode de remplissage de cette dimension

L’ID de capsule publicitaire est généré automatiquement par le SDK lorsqu’un événement [début de la coupure publicitaire](/help/implementation/events/ads/ad-break-start.md) se déclenche. Les implémentations directes de l’API la construisent à partir de l’index de rupture et de l’heure de début ou fournissent un identifiant de capsule personnalisé.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.ad.pod` de données contextuelles lorsque [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Flux de données | `videoadpod`, `post_videoadpod` |
| Audience Manager | S.O. |

## Éléments de dimension

Chaque élément est un ID de capsule publicitaire unique. L’identifiant est opaque (généralement un hachage de l’identifiant de session, de l’identifiant de contenu et de l’index de saut) et est plus utile comme clé de regroupement lorsqu’il est combiné avec le [nom de la capsule](pod-name.md) pour le libellé convivial.
