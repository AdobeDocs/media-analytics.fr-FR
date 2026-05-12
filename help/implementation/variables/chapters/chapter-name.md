---
title: Nom du chapitre
description: Définissez le nom convivial de chaque chapitre afin que le rapport au niveau du chapitre puisse être divisé par titre de chapitre.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 14%

---


# Nom du chapitre

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Nom du chapitre**. Voir [Nom du chapitre](/help/reporting/dimensions/chapter-name.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de nom du chapitre est le titre lisible d’un chapitre (par exemple, `"Pilot Episode - Opening"`). Définissez-le sur chaque événement `media.chapterStart` dont le contenu est divisé en chapitres.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.chapter.friendlyName` |
| **champ de collection XDM** | [`mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début et fin du chapitre |

## SDK web

`friendlyName` à l’intérieur des `mediaCollection.chapterDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

Transmettez le nom du chapitre en tant que premier argument (`name`) à `createChapterObject`.

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

`friendlyName` à l’intérieur des `mediaCollection.chapterDetails` lors de l’appel de `sendMediaEvent` pour `media.chapterStart` :

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

Appelez le point d’entrée [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) avec `friendlyName` à l’intérieur du `mediaCollection.chapterDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
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

Transmettez le nom du chapitre comme premier argument à `ADB.Media.createChapterObject` :

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## API Media Collection

Incluez `media.chapter.friendlyName` dans l’objet `params` de votre `chapterStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
