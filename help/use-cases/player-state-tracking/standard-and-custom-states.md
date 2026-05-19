---
title: À propos des états standards et personnalisés
description: Cette rubrique décrit la fonctionnalité de suivi de l’état du lecteur, y compris les exigences et les instructions relatives à la mise en œuvre et à la création de rapports portant sur les états du lecteur standards et personnalisés.
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/QdUkyWt6cTcdmQXpj6Qe6-s3aYkGfro-G7DYegOVKvA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 287
ht-degree: 96%

---

# À propos des états standards et personnalisés

Cinq états de lecteur standards sont disponibles, et vous pouvez y ajouter vos propres états personnalisés.

| Nom de l’état standard | Constante Media SDK | Nom de l’API Media Collection |
|-----------------------|------------------------------------------|-----------------------------|
| Plein écran | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Sous-titrage codé | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Mode muet | `ADB.Media.PlayerState.Mute` | `mute` |
| Mode « Image dans l’Image » | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Mode « En point de mires » | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Les données sont calculées de la même manière pour les états standards et personnalisés, mais elles sont stockées différemment pour la création de rapports Analytics.

**Pour les états standards** : lorsque vous activez le suivi de l’état du lecteur à partir de la console de gestion des médias dans la création de rapports Analytics (côté administrateur), 15 variables de solution sont disponibles pour la création de rapports et l’exportation de données.

**Pour les états personnalisés** : vous pouvez créer vos propres règles de traitement afin de stocker les valeurs calculées dans des événements personnalisés, et ensuite utiliser ces règles pour la création de rapports et l’exportation de données.

## Instructions

* Une session vidéo est limitée à 10 états du lecteur.
* Toutes les combinaisons d’états sont autorisées.
* Si plusieurs états de lecteur sont transmis, seuls les 10 premiers sont conservés et transférés en aval vers la composante de traitement VA.
* La limite de 10 états s’applique à tous les états, et ce qu’ils soient fermés ou non.
* Un état peut démarrer et se terminer plusieurs fois, et compter comme un état unique. Par exemple, `closedCapationing` peut être démarré et arrêté cinq fois, mais il sera compté comme un état unique.
* Chaque état dépassant la limite de 10 états autorisés est ignoré.

## États personnalisés

Créer des états personnalisés vous permet de capturer des actions personnalisées et de mettre à jour des métadonnées personnalisées au cours d’une session de lecture.

Pour plus d’informations sur la création d’états personnalisés, reportez-vous au [guide de référence de l’API Media : `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)
