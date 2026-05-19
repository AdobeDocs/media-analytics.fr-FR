---
title: Contenu
description: Indique chaque élément multimédia lu unique, indexé par l’identifiant du contenu.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

---


# Contenu

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Contenu**. Voir [ID de contenu](/help/implementation/variables/core/content-id.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Contenu** signale chaque élément multimédia lu unique, en fonction de l’identifiant de contenu défini au début de la session. Il s’agit de la répartition principale pour les rapports sur les médias en flux continu et de la clé de jointure pour les dimensions de classification telles que le nom de la vidéo, la durée de la vidéo, l’ID de ressource, la date de première diffusion et l’évaluation du contenu.

## Mode de remplissage de cette dimension

Le contenu est défini par le lecteur au début de la session en tant qu’identifiant stable de la ressource. Le même ID de contenu est signalé à chaque événement suivant de la session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.name` de données contextuelles lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. Persiste pendant la durée de la visite. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>L’ID de contenu est obligatoire. S’il n’est pas défini ou s’il est vide, la session est supprimée de la création de rapports sur les médias en flux continu et n’apparaîtra dans aucun rapport multimédia ni dans le segment [!UICONTROL Tous les médias en flux continu].

## Éléments de dimension

Chaque élément est un identifiant de contenu unique signalé au début de la session. Utilisez un identifiant stable (par exemple, un identifiant CMS interne, un identifiant de secteur tel que l’EIDR ou TMS/Gracenote, ou un slug persistant) de sorte que les sessions d’une même ressource soient cumulées sur un seul élément de ligne au fil du temps.

## Segments recommandés

| Segment | Composants de |
| --- | --- |
| [!UICONTROL Tous les médias en flux continu] | Le contenu (ID) existe |
