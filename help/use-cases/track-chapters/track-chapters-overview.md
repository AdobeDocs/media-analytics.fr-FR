---
title: Découvrez comment effectuer le suivi des chapitres et des segments présentés
description: Comment mettre en œuvre le suivi des chapitres et des segments avec le SDK Media.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 97%

---

# Aperçu{#overview}

Les instructions suivantes fournissent des conseils pour la mise en œuvre à l’aide des kits SDK 2.x.

>[!IMPORTANT]
> 
> Si vous mettez en œuvre une version 1.x du kit SDK, vous pouvez télécharger le Guide du développeur dans la rubrique [Téléchargement des SDK.](/help/getting-started/download-sdks.md)

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
   | `length` | Longueur du chapitre | Oui |
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
