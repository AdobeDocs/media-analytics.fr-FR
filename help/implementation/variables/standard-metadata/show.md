---
title: Programme
description: Définissez le nom de l’émission pour le contenu vidéo qui fait partie d’une série, de sorte que les épisodes soient regroupés dans un seul programme dans les rapports.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 13%

---


# Programme

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Show**. Voir [Afficher](/help/reporting/dimensions/show.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable show est le nom du programme ou de la série (par exemple, `"Blinding Light"` ou `"Coastline Mysteries"`). Définissez-le sur chaque session dont le contenu appartient à une série, de sorte que les épisodes de plusieurs saisons se cumulent sur un seul élément de ligne dans la dimension Afficher . Ne le définissez pas pour le contenu unique qui ne fait pas partie d’une série.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.show` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obligatoire** | Non |
| **Envoyé avec** | Début et fin de la session |

## SDK web

`show` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        show: "Blinding Light"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez le nom de l’affichage en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.SHOW`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `show` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "show": "Blinding Light"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `show` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "show": "Blinding Light"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez le nom de l’affichage dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Show` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Show] = "Blinding Light";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.show` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.show": "Blinding Light"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
