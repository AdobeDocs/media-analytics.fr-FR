---
title: Découvrez comment effectuer le suivi des chapitres et des segments à l’aide de JavaScript 3.x
description: Découvrez l’implémentation du suivi des chapitres et des segments à l’aide du SDK Media dans les applications de navigateur (JS).
exl-id: 00ba11df-d226-45a2-a561-dc9f15dcf714
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 89%

---

# Suivi des chapitres et des segments à l’aide de JavaScript 3.x{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 3.x. Si vous implémentez une version précédente du SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK](/help/sdk-implement/download-sdks.md).

1. Identifiez le moment où a lieu l’événement de début de chapitre et créez l’instance `ChapterObject` à l’aide des informations de chapitre.

   `ChapterObject` référence de suivi de chapitre :

   >[!NOTE]
   >
   >Ces variables ne sont nécessaires que si vous envisagez d’effectuer le suivi des chapitres.

   | Nom de variable | Type | Description |
   | --- | --- | --- |
   | `name` | chaîne | Chaîne non vide désignant le nom du chapitre. |
   | `position` | nombre | Position du chapitre dans le contenu, en commençant par 1. |
   | `length` | nombre | Nombre positif désignant la longueur du chapitre. |
   | `startTime` | nombre | Valeur de la tête de lecture au début du chapitre. |

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
