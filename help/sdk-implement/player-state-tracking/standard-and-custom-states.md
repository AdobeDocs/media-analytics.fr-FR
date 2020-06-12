---
title: À propos des états standards et personnalisés
description: Cette rubrique décrit la fonctionnalité de suivi de l’état du lecteur, y compris les exigences et les instructions relatives à la mise en œuvre et à la création de rapports portant sur les états du lecteur standards et personnalisés.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 66%

---


# À propos des états standards et personnalisés

Cinq états de lecteur standards sont disponibles, et vous pouvez y ajouter vos propres états personnalisés.

| Nom de l’état standard | Constante Media SDK | Nom de l’API Media Collection |
|-----------------------|------------------------------------------|-----------------------------|
| Plein écran | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sous-titrage codé | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Mode muet | `ADB.Media.PlayerState.Mute` | `mute` |
| Mode « Picture In Picture » (Image dans l’image) | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Mode « In Focus » (En point de mire) | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Les données sont calculées de la même manière pour les états standards et personnalisés, mais elles sont stockées différemment pour la création de rapports Analytics.

**Pour les états standards** : lorsque vous activez le suivi de l’état du lecteur à partir de la console de gestion des médias dans la création de rapports Analytics (côté administrateur), 15 variables de solution sont disponibles pour la création de rapports et l’exportation de données.

**Pour les états personnalisés** : vous pouvez créer vos propres règles de traitement afin de stocker les valeurs calculées dans des événements personnalisés, et ensuite utiliser ces règles pour la création de rapports et l’exportation de données.

## Instructions

* Une session vidéo est limitée à 10 états de lecteur.
* Toute combinaison d’états est autorisée.
* Si plusieurs états de lecteur réussissent, seuls les 10 premiers sont conservés et transférés en aval vers le composant de traitement de l’AV.
* La limite de 10 états s’applique à tous les états, et ce qu’ils soient fermés ou non.
* Un état peut se début et se terminer plusieurs fois et il est compté comme un état unique. Par exemple, `closedCapationing` peut être démarré et arrêté cinq fois, mais il sera compté comme un état unique.
* Chaque état qui dépasse le maximum de 10 états autorisés est ignoré.

## États personnalisés

Créer des états personnalisés vous permet de capturer des actions personnalisées et de mettre à jour des métadonnées personnalisées au cours d’une session de lecture.

Pour plus d’informations sur la création d’états personnalisés, voir le guide de référence de l’API [Media : `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
