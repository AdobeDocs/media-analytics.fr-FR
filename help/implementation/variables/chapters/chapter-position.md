---
title: Position du chapitre
description: Définissez l’index de chapitre dans le contenu. La position du chapitre est requise pour que l’ID de chapitre soit généré automatiquement correctement.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 7%

---


# Position du chapitre

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Position du chapitre**. Voir [Position du chapitre](/help/reporting/dimensions/chapter-position.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de position du chapitre est l’index du chapitre à l’intérieur du contenu, en commençant par `1` (standard) ou `0` (selon votre convention). Utilisez un index stable par chapitre afin que le même chapitre soit reporté entre les sessions.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.chapter.position` |
| **champ de collection XDM** | [`xdm.mediaCollection.chapterDetails.index`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.chapter.position` |
| **Obligatoire** | Non (Mobile SDK) ; Oui (Edge, API Media Collection) |
| **Envoyé avec** | [Début du chapitre](/help/implementation/events/chapters/chapter-start.md), fermeture du chapitre |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`index` à l’intérieur des `xdm.mediaCollection.chapterDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

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

>[!TAB iOS]

Transmettez la position du chapitre comme deuxième argument à `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Transmettez la position du chapitre comme deuxième argument à `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku]

`index` à l’intérieur des `xdm.mediaCollection.chapterDetails` lors de l’appel de `sendMediaEvent` pour `media.chapterStart` :

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

>[!TAB  API Media Edge ]

Appelez le point d’entrée [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) avec `index` à l’intérieur du `xdm.mediaCollection.chapterDetails` :

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB  Chromecast ]

Transmettez la position du chapitre comme deuxième argument à `ADBMobile.media.createChapterObject` :

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
