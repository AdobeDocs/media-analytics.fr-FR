---
title: Longueur du chapitre
description: Définissez la longueur de chaque chapitre, en secondes.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---


# Longueur du chapitre

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Longueur du chapitre**. Voir [Longueur du chapitre](/help/reporting/dimensions/chapter-length.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de longueur du chapitre correspond à la durée du chapitre, exprimée en secondes. Définissez-le sur chaque événement `media.chapterStart`.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.chapter.length` |
| **champ de collection XDM** | [`mediaCollection.chapterDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.chapter.length` |
| **Obligatoire** | Non (Mobile SDK) ; Oui (Edge, API Media Collection) |
| **Envoyé avec** | [Début du chapitre](/help/implementation/events/chapters/chapter-start.md), fermeture du chapitre |

## SDK web

`length` à l’intérieur des `mediaCollection.chapterDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez la longueur du chapitre en secondes comme troisième argument à `createChapterObject`.

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

`length` à l’intérieur des `mediaCollection.chapterDetails` lors de l’appel de `sendMediaEvent` pour `media.chapterStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) avec `length` à l’intérieur du `mediaCollection.chapterDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez la longueur du chapitre comme troisième argument à `ADB.Media.createChapterObject` :

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",
  1,
  240,
  0
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## API Media Collection

Incluez `media.chapter.length` dans l’objet `params` de votre `chapterStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.length": 240
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
