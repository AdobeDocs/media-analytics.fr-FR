---
title: Suivi des chapitres et des segments à l’aide de JavaScript 3.x
description: Découvrez l’implémentation du suivi des chapitres et des segments à l’aide du SDK Media dans les applications de navigateur (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/YZAcZVcqS15hCae-LYwjpSYztXijauQNIzElCcWcPT0
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
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 224
ht-degree: 100%

---

# Effectuer le suivi des chapitres et des segments à l’aide de JavaScript 3.x{#track-chapters-and-segments-on-javascript}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 3.x.

>[!IMPORTANT]
>
> Si vous implémentez une version précédente du SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK](/help/getting-started/download-sdks.md).

1. Identifiez le moment où a lieu l’événement de début de chapitre et créez l’instance `ChapterObject` à l’aide des informations de chapitre.

   `ChapterObject` référence de suivi de chapitre :

   >[!NOTE]
   >
   >Ces variables ne sont nécessaires que si vous envisagez d’effectuer le suivi des chapitres.

   | Nom de variable | Type | Description |
   | --- | --- | --- |
   | `name` | string | Chaîne non vide désignant le nom du chapitre. |
   | `position` | number | Position du chapitre dans le contenu, en commençant par 1. |
   | `length` | number | Nombre positif désignant la longueur du chapitre. |
   | `startTime` | number | Valeur de la tête de lecture au début du chapitre. |

   Objet de chapitre :

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Si vous incluez des métadonnées personnalisées pour le chapitre, créez les variables de données contextuelles pour les métadonnées :

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Pour lancer le suivi de la lecture du chapitre, appelez l’événement `ChapterStart` dans l’instance `MediaHeartbeat` :

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Lorsque la lecture atteint la limite de fin du chapitre, comme défini par votre code personnalisé, appelez l’événement `ChapterComplete` dans l’instance `MediaHeartbeat` :

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Si la lecture du chapitre ne s’est pas terminée car l’utilisateur a choisi d’ignorer le chapitre (par exemple, si l’utilisateur effectue une recherche en dehors de la limite du chapitre), appelez l’événement `ChapterSkip` dans l’instance MediaHeartbeat :

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. S’il existe d’autres chapitres, répétez les étapes 1 à 5.
