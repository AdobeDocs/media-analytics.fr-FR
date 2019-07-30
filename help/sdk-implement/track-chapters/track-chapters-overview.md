---
seo-title: Aperçu
title: Aperçu
uuid: 3 fe 32425-5 e 2 a -4886-8 fea-d 91 d 15671 bb 0
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Aperçu{#overview}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l'aide de SDK 2. x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

Le suivi des chapitres et des segments est disponible pour les chapitres ou segments de médias définis personnalisés. Pour le suivi des chapitres, certaines utilisations courantes sont de définir des segments personnalisés basés sur le contenu multimédia (par exemple, les incréments du baseball) ou de définir des segments de contenu entre les coupures publicitaires. Chapter tracking is **not** required for core media tracking implementations.

Le suivi des chapitres comprend les démarrages de chapitre, les fins de chapitre, et les chapitres ignorés. Vous pouvez utiliser l'API du lecteur multimédia avec une logique de segmentation personnalisée pour identifier les événements de chapitre et renseigner les variables de chapitre obligatoires et facultatives.

## Evénements du lecteur

### Au démarrage du chapitre

* Créez l’instance d’objet de chapitre du chapitre, `chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* L’appel   `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Au chapitre Terminé

* L’appel   `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Sur le saut de chapitre

* L’appel   `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Identifiez le moment où a lieu l’événement de début de chapitre et créez l’instance `ChapterObject` à l’aide des informations de chapitre.

   Voici la référence de suivi de chapitre `ChapterObject` :

   >[!NOTE]
   >
   >Ces variables ne sont requises que si vous envisagez de suivre des chapitres.

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

L'exemple de code suivant utilise le SDK JavaScript 2. x pour un lecteur de médias HTML 5. Utilisez ce code avec le code de lecture de média principal.

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

## Validation {#section_07EC2811BE3249249494596BFE9BF869}

### Début du chapitre

Au début d'une lecture de chapitre individuelle, un appel clé est envoyé :

* Heartbeat chapter start (Cet appel contient des variables de métadonnées de chapitre supplémentaires.)

### Chapitre terminé

À la fin de la limite du chapitre, un appel de fin de chapitre Heartbeat est envoyé.

### Ignorer le chapitre

Lorsqu’un chapitre est ignoré, un appel de chapitre ignoré Heartbeat est envoyé.
