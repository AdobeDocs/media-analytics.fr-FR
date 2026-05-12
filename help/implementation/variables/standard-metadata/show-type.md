---
title: Type d’affichage
description: Identifiez le format du contenu (épisode complet, aperçu, clip ou autre) à l’aide d’un code entier de chaîne.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 13%

---


# Type d’affichage

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Type d’affichage**. Voir [Type d’affichage](/help/reporting/dimensions/show-type.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable show type identifie le format du contenu à l&#39;aide d&#39;un code entier de chaîne :

- `"0"` : épisode complet
- `"1"` : aperçu ou bande-annonce
- `"2"` : Clip
- `"3"` : autre

Utilisez-le pour séparer l’affichage du programme complet du contenu court, tel que des bandes-annonces et des clips, lors de la mesure de l’engagement.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.type` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début et fin de la session |

## SDK web

`showType` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        showType: "0"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez le type show comme clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.SHOW_TYPE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW_TYPE] = "0"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `showType` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "showType": "0"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `showType` à l’intérieur du `mediaCollection.sessionDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "showType": "0"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez le type show dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.ShowType` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.ShowType] = "0";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.showType` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.showType": "0"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
