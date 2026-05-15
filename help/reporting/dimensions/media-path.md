---
title: Chemin du média
description: Capture l’identifiant du contenu en tant que variable de trafic pour l’analyse des chemins.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# Chemin du média

La dimension **Chemin d’accès au média** capture l’ID de contenu en tant que variable de trafic (prop) afin qu’il puisse être utilisé dans l’analyse du cheminement (par exemple, les rapports de flux contenu suivant et contenu précédent). Elle est propre à Adobe Analytics : Customer Journey Analytics ne stocke pas les variables de trafic et le cheminement est effectué directement sur la dimension Contenu (ID).

## Mode de remplissage de cette dimension

Le chemin d’accès au média est automatiquement dérivé de l’identifiant de contenu défini au démarrage de la session. Il n’y a pas de variable distincte à définir ; la colonne de flux de données `videopath` est renseignée chaque fois que le contenu (ID) est renseigné.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement à partir des données contextuelles `a.media.name` en tant que variable de trafic (prop) lorsque [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) est activé. |
| Customer Journey Analytics | N/A — utiliser [Contenu](content.md) pour l&#39;analyse des chemins |
| Flux de données | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Les props Adobe Analytics sont limitées à 100 octets. Les valeurs de plus de 100 octets sont tronquées.

>[!IMPORTANT]
>
>Les rapports de cheminement comparent la valeur prop entre les accès au cours d’une même visite. Si le contenu (ID) change au cours d’une visite (par exemple, lorsqu’une personne passe d’un élément de contenu à un autre), le rapport Chemin d’accès affiche ce flux.

## Éléments de dimension

Chaque élément est un identifiant de contenu signalé lors d’une visite. Utilisez les rapports Flux de page suivante et Flux de page précédente sous Contenu > Chemin du média dans Adobe Analytics pour afficher les chemins de navigation contenu à contenu.
