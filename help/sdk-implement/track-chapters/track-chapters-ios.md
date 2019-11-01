---
title: Suivi des chapitres et des segments sur iOS
description: Cette rubrique décrit l’implémentation du suivi des chapitres et des segments à l’aide du SDK multimédia sur iOS.
uuid: ffc5ce9f-04ba-4059-92d4-4cb4180ac9ed
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Suivi des chapitres et des segments sur iOS{#track-chapters-and-segments-on-ios}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour l’implémentation à l’aide des SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

1. Identifiez le moment où a lieu l’événement de début de chapitre et créez l’instance `ChapterObject` à l’aide des informations de chapitre.

   `ChapterObject` référence de suivi de chapitre :

   >[!NOTE]
   >
   >Ces variables ne sont requises que si vous prévoyez de suivre les chapitres.

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom du chapitre | Oui |
   | `position` | Position du chapitre | Oui |
   | `length` | Durée du chapitre | Oui |
   | `startTime` | Heure de début du chapitre | Oui |

   Objet de chapitre :

   ```
   id chapterObject =  
     [ADBMediaHeartbeat createChapterObjectWithName:[CHAPTER_NAME] 
                        position:[POSITION] 
                        length:[LENGTH] 
                        startTime:[START_TIME]];
   ```

1. Si vous incluez des métadonnées personnalisées pour le chapitre, créez les variables de données contextuelles pour les métadonnées :

   ```
   NSMutableDictionary *chapterDictionary = [[NSMutableDictionary alloc] init]; 
   [chapterDictionary setObject:@"Sample segment type" forKey:@"segmentType"]; 
   [chapterDictionary setObject:@"Sample segment name" forKey:@"segmentName"]; 
   [chapterDictionary setObject:@"Sample segment info" forKey:@"segmentInfo"];
   ```

1. Pour lancer le suivi de la lecture du chapitre, appelez l’événement `ChapterStart` dans l’instance `MediaHeartbeat` :

   ```
   - (void)onChapterStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterStart  
                        mediaObject:chapterObject     
                        data:chapterDictionary]; 
   }
   ```

1. Lorsque la lecture atteint la limite de fin du chapitre, comme défini par votre code personnalisé, appelez l’événement `ChapterComplete` dans l’instance `MediaHeartbeat` :

   ```
   - (void)onChapterComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Si la lecture du chapitre ne s’est pas terminée car l’utilisateur a choisi d’ignorer le chapitre (par exemple, si l’utilisateur effectue une recherche en dehors de la limite du chapitre), appelez l’événement `ChapterSkip` dans l’instance MediaHeartbeat :

   ```
   - (void)onChapterSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventChapterSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. S’il existe d’autres chapitres, répétez les étapes 1 à 5.

