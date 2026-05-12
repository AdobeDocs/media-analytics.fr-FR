---
title: Position du chapitre
description: Définissez l’index de chapitre dans le contenu. La position du chapitre est requise pour que l’ID de chapitre soit généré automatiquement correctement.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 12%

---


# Position du chapitre

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Position du chapitre**. Voir [Position du chapitre](/help/reporting/dimensions/chapter-position.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de position du chapitre est l’index du chapitre à l’intérieur du contenu, en commençant par `1` (standard) ou `0` (selon votre convention). Utilisez un index stable par chapitre afin que le même chapitre soit reporté entre les sessions.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.chapter.position` |
| **champ de collection XDM** | [`mediaCollection.chapterDetails.index`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Obligatoire** | Non (Mobile SDK) ; Oui (Edge, API Media Collection) |
| **Envoyé avec** | Début et fin du chapitre |

## SDK web

`index` à l’intérieur des `mediaCollection.chapterDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

Transmettez la position du chapitre comme deuxième argument à `createChapterObject`.

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

`index` à l’intérieur des `mediaCollection.chapterDetails` lors de l’appel de `sendMediaEvent` pour `media.chapterStart` :

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

Appelez le point d’entrée [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) avec `index` à l’intérieur du `mediaCollection.chapterDetails` :

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

Transmettez la position du chapitre comme deuxième argument à `ADB.Media.createChapterObject` :

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

Incluez `media.chapter.index` dans l’objet `params` de votre `chapterStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.index": 1
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
