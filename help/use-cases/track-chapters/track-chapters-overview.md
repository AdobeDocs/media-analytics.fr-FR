---
title: Découvrez comment effectuer le suivi des chapitres et des segments présentés
description: Comment mettre en œuvre le suivi des chapitres et des segments avec Media SDK.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 0%

---

# Aperçu{#overview}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des SDK 2.x.

>[!IMPORTANT]
> 
> Si vous mettez en œuvre une version 1.x de SDK, vous pouvez télécharger le guide du développeur à l’adresse suivante : [Télécharger les SDK.](/help/getting-started/download-sdks.md)

Le suivi des chapitres et des segments est disponible pour les chapitres ou segments de médias personnalisés. Le suivi des chapitres est souvent utilisé pour définir des segments personnalisés en fonction du contenu multimédia (comme les matchs de baseball) ou pour définir des segments de contenu entre les pauses publicitaires. Le suivi des chapitres n’est **pas** requis pour les implémentations de suivi des médias principaux.

Le suivi des chapitres comprend les débuts de chapitre, les fins de chapitre et les sauts de chapitre. Vous pouvez utiliser l’API du lecteur multimédia avec une logique de segmentation personnalisée pour identifier les événements de chapitre et renseigner les variables de chapitre obligatoires et facultatives.

## Événements du lecteur

### Au début du chapitre

* Créez l’instance d’objet de chapitre pour le chapitre, `chapterObject`
* Renseignez les métadonnées du chapitre, `chapterCustomMetadata`
* `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);` d’appel

### Chapitre terminé

* `trackEvent(MediaHeartbeat.Event.ChapterComplete);` d’appel

### Ignorer le chapitre

* `trackEvent(MediaHeartbeat.Event.ChapterSkip);` d’appel

## Mise en œuvre du suivi des chapitres {#implement-chapter-tracking}

1. Identifiez le moment où l’événement de début de chapitre se produit et créez l’instance de `ChapterObject` à l’aide des informations sur le chapitre.

   Voici la référence de suivi des chapitres `ChapterObject` :

   >[!NOTE]
   >
   >Ces variables ne sont nécessaires que si vous envisagez d’effectuer le suivi des chapitres.

   | Nom de la variable | Description | Obligatoire |
   | --- | --- | :---: |
   | `name` | Nom du chapitre | Oui |
   | `position` | Position du chapitre | Oui |
   | `length` | Longueur du chapitre | Oui |
   | `startTime` | Heure de début du chapitre | Oui |

1. Si vous incluez des métadonnées personnalisées pour le chapitre, créez les variables de données contextuelles pour les métadonnées.
1. Pour commencer à effectuer le suivi de la lecture du chapitre, appelez l’événement `ChapterStart` dans l’instance `MediaHeartbeat`.
1. Lorsque la lecture atteint la limite de fin de chapitre, telle que définie par votre code personnalisé, appelez l’événement `ChapterComplete` dans l’instance `MediaHeartbeat`.
1. Si la lecture du chapitre ne s’est pas terminée car l’utilisateur a choisi d’ignorer le chapitre (par exemple, s’il effectue une recherche en dehors de la limite du chapitre), appelez l’événement `ChapterSkip` dans l’instance MediaHeartbeat.
1. S’il existe d’autres chapitres, répétez les étapes 1 à 5.

L’exemple de code suivant utilise le SDK JavaScript 2.x pour un lecteur multimédia HTML5. Vous devez utiliser ce code avec le code de lecture des médias principaux.

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

>[!MORELIKETHIS]
>
>* [ Début du chapitre ](/help/implementation/events/chapters/chapter-start.md)
>* [Chapitre terminé](/help/implementation/events/chapters/chapter-complete.md)
>* [Saut de chapitre](/help/implementation/events/chapters/chapter-skip.md)
