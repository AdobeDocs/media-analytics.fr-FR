---
seo-title: Suivi des chapitres et des segments sur Roku
title: Suivi des chapitres et des segments sur Roku
uuid: 15 c 07131-77 d 7-4 a 97-92 c 6-0 a 190 c 6 b 08 d 3
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi des chapitres et des segments sur Roku{#track-chapters-and-segments-on-roku}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l'aide de SDK 2. x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

## Métadonnées publicitaires standard de mise en œuvre

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

   ```
   chapterInfo =  
     adb_media_init_chapterinfo(<CHAPTER_NAME>,  
                                <POSITION>,  
                                <LENGTH>,  
                                <START_TIME>);)
   ```

1. Si vous incluez des métadonnées personnalisées pour le chapitre, créez les variables de données contextuelles pour les métadonnées :

   ```
   chapterContextData = {} 
   chapterContextData["seg_type"] = "seg_type" 
   chapterContextData["seg_name"] = "seg_name" 
   chapterContextData["seg_info"] = "seg_info"
   ```

1. Pour lancer le suivi de la lecture du chapitre, appelez l’événement `ChapterStart` dans l’instance `MediaHeartbeat` :

   ```
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_START, chapterInfo, chapterContextData)
   ```

1. Lorsque la lecture atteint la limite de fin du chapitre, comme défini par votre code personnalisé, appelez l’événement `ChapterComplete` dans l’instance `MediaHeartbeat`.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_COMPLETE, chapterInfo, chapterContextData)
   ```

1. Si la lecture du chapitre ne s’est pas terminée car l’utilisateur a choisi d’ignorer le chapitre (par exemple, si l’utilisateur effectue une recherche en dehors de la limite du chapitre), appelez l’événement `ChapterSkip` dans l’instance MediaHeartbeat.

   ```
   chapterContextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_CHAPTER_SKIP, chapterInfo, chapterContextData)
   ```

1. S’il existe d’autres chapitres, répétez les étapes 1 à 5.

