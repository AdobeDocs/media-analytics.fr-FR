---
title: Chapitre
description: Indique chaque chapitre lu unique, indexé par un identifiant de chapitre généré automatiquement.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 8%

---


# Chapitre

La dimension **Chapitre** signale chaque chapitre lu unique, indexé par un identifiant de chapitre généré automatiquement. L’ID est construit par le SDK ou le serveur principal à partir de l’ID de contenu, de l’index de chapitre et de l’heure de début du chapitre. De ce fait, deux sessions du même chapitre sur le même contenu sont cumulées sur un seul élément de ligne. Utilisez la dimension comme clé de jointure pour les classifications de niveau chapitre telles que le nom du chapitre, la longueur du chapitre, le décalage du chapitre et la position du chapitre.

## Mode de remplissage de cette dimension

L’identifiant de chapitre est généré automatiquement lorsqu’un événement [début de chapitre](/help/implementation/events/chapters/chapter-start.md) se déclenche. La valeur n’est pas définie directement ; elle est dérivée de la position du chapitre, du décalage et de l’identifiant du contenu.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des `a.media.chapter.name` de données contextuelles lorsque l’option [[!UICONTROL Chapitres de médias]](/help/reporting/setup/analytics-reporting.md) est activée. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Flux de données | `videochapter`, `post_videochapter` |
| Audience Manager | S.O. |

## Éléments de dimension

Chaque élément est un identifiant de chapitre unique. L’identifiant est opaque (généralement un hachage de l’identifiant de contenu + index + décalage) et est très utile comme clé de regroupement. Associez avec [Nom du chapitre](chapter-name.md) pour un libellé convivial.
