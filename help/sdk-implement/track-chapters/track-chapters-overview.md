---
title: Aperçu
description: Comment mettre en oeuvre le suivi des chapitres et des segments avec le SDK multimédia.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Aperçu{#overview}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour l’implémentation à l’aide des SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

Le suivi des chapitres et des segments est disponible pour les chapitres ou segments de médias personnalisés. Le suivi des chapitres sert généralement à définir des segments personnalisés en fonction du contenu multimédia (par exemple, des manches de base-ball) ou à définir des segments de contenu entre des pauses publicitaires. Chapter tracking is **not** required for core media tracking implementations.

Le suivi des chapitres comprend les démarrages de chapitre, les fins de chapitre, et les chapitres ignorés. Vous pouvez utiliser l’API du lecteur multimédia avec une logique de segmentation personnalisée pour identifier les événements de chapitre et renseigner les variables de chapitre obligatoires et facultatives.

## Événements du lecteur

### Au début du chapitre

* Créez l’instance d’objet de chapitre du chapitre, `chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* L’appel   `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Au chapitre terminé

* L’appel   `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Lors du saut de chapitre

* L’appel   `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Mise en oeuvre du suivi des chapitres {#implement-chapter-tracking}

1. Identifiez le moment où a lieu l’événement de début de chapitre et créez l’instance `ChapterObject` à l’aide des informations de chapitre.

   Voici la référence de suivi de chapitre `ChapterObject` :

   >[!NOTE]
   >
   >Ces variables ne sont requises que si vous prévoyez de suivre les chapitres.

   | Nom de variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom du chapitre | Oui |
   | `position` | Position du chapitre | Oui |
   | `length` | Durée du chapitre | Oui |
   | `startTime` | Heure de début du chapitre | Oui |

1. Si vous incluez des métadonnées personnalisées pour le chapitre, créez les variables de données contextuelles pour les métadonnées.
1. Pour lancer le suivi de la lecture du chapitre, appelez l’événement `ChapterStart` dans l’instance `MediaHeartbeat`.
1. Lorsque la lecture atteint la limite de fin du chapitre, comme défini par votre code personnalisé, appelez l’événement `ChapterComplete` dans l’instance `MediaHeartbeat`.
1. Si la lecture du chapitre ne s’est pas terminée car l’utilisateur a choisi d’ignorer le chapitre (par exemple, si l’utilisateur effectue une recherche en dehors de la limite du chapitre), appelez l’événement `ChapterSkip` dans l’instance MediaHeartbeat.
1. S’il existe d’autres chapitres, répétez les étapes 1 à 5.

L’exemple de code suivant utilise le SDK JavaScript 2.x pour un lecteur de médias HTML5. Utilisez ce code avec le code de lecture du média principal.

```js
/* Call on chapter start */ 
if (e.type == "chapter start") { 
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500); 
    /* Set custom context data*/ 
    var chapterCustomMetadata = { 
        segmentType:"Baseball Innings", 
        segmentName:"Inning 5", 
        segmentInfo:"Game Six" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata); 
}; 
 
/* Call on chapter complete */ 
if (e.type == "chapter complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
}; 
 
/* Call on chapter skip */ 
if (e.type == "chapter skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
}; 
```

