---
title: MVPD
description: Indique le fournisseur par câble, satellite ou virtuel par lequel l’utilisateur s’est authentifié.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 9%

---


# MVPD

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **MVPD**. Voir [](/help/implementation/variables/standard-metadata/mvpd.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **** (distributeur de programmation vidéo multicanal) indique le fournisseur par lequel l’utilisateur s’est authentifié via Adobe Pass (par exemple, `"Comcast"` ou `"DirecTV"`). Utilisez-le pour ventiler l’engagement par fournisseur d’authentification.

## Mode de remplissage de cette dimension

MVPD est défini par le lecteur au démarrage de la session lorsque le contenu est protégé par Adobe Pass.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pass.mvpd` de données contextuelles lorsque [[!UICONTROL  Métadonnées vidéo ]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## Éléments de dimension

Chaque élément correspond au nom MVPD littéral indiqué au début de la session. Utilisez l’identifiant Adobe Pass MVPD canonique par fournisseur pour que les données soient cumulées sur un seul élément de ligne par fournisseur.
