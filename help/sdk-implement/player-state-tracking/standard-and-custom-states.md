---
title: A propos des états standard et personnalisés
description: Cette rubrique décrit la fonction de suivi de l’état du lecteur, y compris les exigences et les directives relatives à la mise en oeuvre et au rapports des états standard et personnalisés du lecteur.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '251'
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

* Une session vidéo est limitée à 10 états de lecteur personnalisé uniques.
* Si plusieurs états de lecteur réussissent, seuls les 10 premiers sont conservés et transférés en aval vers le composant de traitement VA(?video analytics).
* Un maximum de 10 Etats est appliqué à tous les Etats, qu&#39;ils soient fermés ou non.
* Le même état peut être démarré et terminé un nombre indéfini de fois et est comptabilisé comme un état unique.
* Chaque état qui dépasse le nombre maximal autorisé de personnalisations ? les états (10) sont ignorés.

## Etats personnalisés

Avec la possibilité de créer des états personnalisés, vous pouvez capturer des actions personnalisées et mettre à jour des métadonnées personnalisées au cours d’une session de lecture.

BESOIN de plus d’informations sur les états personnalisés
