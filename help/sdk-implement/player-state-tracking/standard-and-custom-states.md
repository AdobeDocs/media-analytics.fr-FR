---
title: A propos des états standard et personnalisés
description: Cette rubrique décrit la fonction de suivi de l’état du lecteur, y compris les exigences et les directives relatives à la mise en oeuvre et au rapports des états standard et personnalisés du lecteur.
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# A propos des états standard et personnalisés

Cinq états de lecteur standard sont disponibles et vous pouvez ajouter vos propres états personnalisés.

| Nom d’état standard | Constante Media SDK | Nom de l’API de collecte de médias |
|-----------------------|------------------------------------------|-----------------------------|
| Plein écran | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sous-titrage | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Muet | `ADB.Media.PlayerState.Mute` | `mute` |
| Image dans l&#39;image | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Mise au point | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Les données sont calculées de la même manière pour les états standard et personnalisés, mais elles sont stockées différemment pour le rapports Analytics.

**Pour les états** standard : lorsque vous activez le suivi des états du lecteur à partir de la console Media Management dans le rapports Analytics (côté administrateur), 15 variables de solution sont disponibles pour les exportations de rapports et de données.

**Pour les états** personnalisés : vous pouvez créer vos propres règles de traitement pour stocker les valeurs calculées dans des événements personnalisés, puis utiliser ces règles pour les exportations de rapports et de données.

## Instructions

* Une session vidéo est limitée à 10 états de lecteur.
* Toute combinaison d’états est autorisée.
* Si plusieurs états de lecteur réussissent, seuls les 10 premiers sont conservés et transférés en aval vers le composant de traitement de l’AV.
* Un maximum de 10 Etats est appliqué à tous les Etats, qu&#39;ils soient fermés ou non.
* Un état peut se début et se terminer plusieurs fois et il est compté comme un état unique. Par exemple, `closedCapationing` peut être démarré et arrêté cinq fois, mais il sera compté comme un état unique.
* Chaque état qui dépasse le maximum de 10 états autorisés est ignoré.

## Etats personnalisés

Avec la possibilité de créer des états personnalisés, vous pouvez capturer des actions personnalisées et mettre à jour des métadonnées personnalisées au cours d’une session de lecture.

Pour plus d’informations sur la création d’états personnalisés, voir le guide de référence de l’API [Media : `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
