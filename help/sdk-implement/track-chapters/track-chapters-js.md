---
seo-title: Suivi des chapitres et des segments sur JavaScript
title: Suivi des chapitres et des segments sur JavaScript
uuid: ef 99 fed 7-7 a 77-46 c 4-8429-bc 9 a 856 b 98 d 6
translation-type: tm+mt
source-git-commit: b461da1823e45eef86302e14501eac0d4b055c7a

---


# Suivi des chapitres et des segments sur JavaScript{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l'aide de SDK 2. x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK.](../../sdk-implement/download-sdks.md)

1. Identifiez le moment où a lieu l’événement de début de chapitre et créez l’instance `ChapterObject` à l’aide des informations de chapitre.

   `ChapterObject` référence du suivi des chapitres :

   >[!NOTE]
   >
   >Ces variables ne sont requises que si vous envisagez de suivre des chapitres.

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom du chapitre | Oui |
   | `position` | Position du chapitre | Oui |
   | `length` | Durée du chapitre | Oui |
   | `startTime` | Heure de début du chapitre | Oui |

   Objet de chapitre :

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Si vous incluez des métadonnées personnalisées pour le chapitre, créez les variables de données contextuelles pour les métadonnées :

   ```js
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info" 
   };
   ```

1. Pour lancer le suivi de la lecture du chapitre, appelez l’événement `ChapterStart` dans l’instance `MediaHeartbeat` :

   ```js
   _onChapterStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata); 
   };
   ```

1. Lorsque la lecture atteint la limite de fin du chapitre, comme défini par votre code personnalisé, appelez l’événement `ChapterComplete` dans l’instance `MediaHeartbeat` :

   ```js
   _onChapterComplete = function() { 
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
   };
   ```

1. Si la lecture du chapitre ne s’est pas terminée car l’utilisateur a choisi d’ignorer le chapitre (par exemple, si l’utilisateur effectue une recherche en dehors de la limite du chapitre), appelez l’événement `ChapterSkip` dans l’instance MediaHeartbeat :

   ```js
   _onChapterSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
   };
   ```

1. S’il existe d’autres chapitres, répétez les étapes 1 à 5.

