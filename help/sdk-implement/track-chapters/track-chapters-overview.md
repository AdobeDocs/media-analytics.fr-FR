---
title: Découvrez comment effectuer le suivi des chapitres et des segments présentés dans la section
description: Comment mettre en œuvre le suivi des chapitres et des segments avec le SDK Media.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 97%

---

# Aperçu{#overview}

>[!IMPORTANT]
>
>Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 2.x. Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK.](/help/sdk-implement/download-sdks.md)

Le suivi des chapitres et des segments est disponible pour les chapitres ou les segments médias personnalisés. Certaines utilisations courantes du suivi des chapitres consistent à définir des segments personnalisés basés sur le contenu média, tels que les manches au baseball, ou à définir des segments de contenu entre les coupures publicitaires. Le suivi des chapitres n’est **pas** requis pour les mises en œuvre de suivi multimédia principal.

Le suivi des chapitres comprend les démarrages de chapitre, les fins de chapitre, et les chapitres ignorés. Vous pouvez utiliser l’API du lecteur multimédia avec une logique de segmentation personnalisée pour identifier les événements de chapitre et renseigner les variables de chapitre obligatoires et facultatives.

## Événements du lecteur

### Au début du chapitre

* Créez l’instance d’objet de chapitre du chapitre, `chapterObject`
* Renseignez les métadonnées du chapitre, `chapterCustomMetadata`
* L’appel `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### À la fin du chapitre

* L’appel `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Lorsque le chapitre est ignoré

* L’appel `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Mise en œuvre du suivi des chapitres {#implement-chapter-tracking}

1. Identifiez le moment où a lieu l’événement de début de chapitre et créez l’instance `ChapterObject` à l’aide des informations de chapitre.

   Voici la référence de suivi de chapitre `ChapterObject` :

   >[!NOTE]
   >
   >Ces variables ne sont nécessaires que si vous envisagez d’effectuer le suivi des chapitres.

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

L’exemple de code suivant utilise le kit SDK JavaScript 2.x pour un lecteur multimédia HTML5. Utilisez ce code avec le code de lecture multimédia principal.

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
