---
title: Décalage de chapitre
description: Définissez le décalage du chapitre à l’intérieur du contenu, en secondes à partir du début.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 7%

---


# Décalage de chapitre

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Chapter offset**. Voir [Décalage de chapitre](/help/reporting/dimensions/chapter-offset.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de décalage de chapitre est le décalage du chapitre à l’intérieur du contenu, mesuré en secondes à partir du début. Le premier chapitre comporte généralement des `0` de décalage ; les chapitres suivants présentent des décalages correspondant à leur heure de début de la lecture.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.chapter.offset` |
| **champ de collection XDM** | [`xdm.mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.chapter.offset` |
| **Obligatoire** | Non (Mobile SDK) ; Oui (Edge, API Media Collection) |
| **Envoyé avec** | [Début du chapitre](/help/implementation/events/chapters/chapter-start.md), fermeture du chapitre |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`offset` à l’intérieur des `xdm.mediaCollection.chapterDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

>[!TAB iOS]

Transmettez le décalage en secondes comme quatrième argument (`startTime`) à `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Transmettez le décalage en secondes comme quatrième argument (`startTime`) à `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku]

`offset` à l’intérieur des `xdm.mediaCollection.chapterDetails` lors de l’appel de `sendMediaEvent` pour `media.chapterStart` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) avec `offset` à l’intérieur du `xdm.mediaCollection.chapterDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmettez le décalage comme quatrième argument à `ADB.Media.createChapterObject` :

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

>[!TAB  Chromecast ]

Transmettez le décalage de chapitre en secondes comme quatrième argument (`startTime`) à `ADBMobile.media.createChapterObject` :

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime (seconds from content start)
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.chapter.offset` dans l’objet `params` de votre `chapterStart` requête POST :

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
