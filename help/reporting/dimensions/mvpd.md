---
title: MVPD
description: Indique le fournisseur par câble, satellite ou virtuel par lequel l’utilisateur s’est authentifié.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 8%

---


# MVPD

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **MVPD**. Voir [&#128279;](/help/implementation/variables/standard-metadata/mvpd.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **&#x200B;**&#x200B;(distributeur de programmation vidéo multicanal) indique le fournisseur par lequel l’utilisateur s’est authentifié via Adobe Pass (par exemple, `"Comcast"` ou `"DirecTV"`). Utilisez-le pour ventiler l’engagement par fournisseur d’authentification.

## Mode de remplissage de cette dimension

MVPD est défini par le lecteur au démarrage de la session lorsque le contenu est protégé par Adobe Pass.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.pass.mvpd` de données contextuelles lorsque [[!UICONTROL &#x200B; Métadonnées vidéo &#x200B;]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `videomvpd, post_videomvpd` |

## Éléments de dimension

Chaque élément correspond au nom MVPD littéral indiqué au début de la session. Utilisez l’identifiant Adobe Pass MVPD canonique par fournisseur pour que les données soient cumulées sur un seul élément de ligne par fournisseur.
