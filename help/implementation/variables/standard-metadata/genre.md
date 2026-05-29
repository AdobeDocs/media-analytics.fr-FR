---
title: Genre
description: Définissez le genre du contenu sous la forme d’une chaîne délimitée par des virgules. Le contenu multigenre est fractionné sur plusieurs éléments de ligne dans les rapports.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 8%

---


# Genre

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Genre**. Voir [Genre](/help/reporting/dimensions/genre.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable genre correspond au genre de contenu tel que défini par le producteur (par exemple, `"Drama"`, `"Comedy"` ou `"Drama,Action"`). Délimitez plusieurs valeurs par des virgules lorsque le contenu correspond à plusieurs genres. Dans les rapports, la variable de liste divise chaque valeur en un élément de ligne distinct, chaque élément de ligne recevant un poids métrique égal.

>[!NOTE]
>
>Dans le pipeline de création de rapports, la valeur de genre est exposée sous la forme `xdm.mediaReporting.sessionDetails.genreList` (un champ de liste). L’ancien chemin de `xdm.mediaReporting.sessionDetails.genre` reste fonctionnel, mais `genreList` est recommandé.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.genre` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.genre` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`genre` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez la chaîne de genre en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.GENRE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmettez la chaîne de genre en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.GENRE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Utilisez `createMediaSession` pour définir des `genre` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `genre` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "genre": "Drama,Action"
        },
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

Transmettez le genre dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Genre` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Utilisez `ADBMobile.media.VideoMetadataKeys.GENRE` pour définir le genre dans la propriété `StandardMediaMetadata` de l’objet média avant d’appeler `trackSessionStart` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "Drama,Action";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.genre` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
