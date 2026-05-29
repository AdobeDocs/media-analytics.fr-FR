---
title: Type de diffusion
description: Définissez le type de flux pour identifier si un flux multimédia est du contenu audio ou vidéo.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 7%

---


# Type de diffusion

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Type de flux**. Voir [Type de flux](/help/reporting/dimensions/stream-type.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de type de flux identifie si un flux multimédia est du contenu audio ou vidéo. Elle est requise pour toutes les implémentations de médias en flux continu et doit être définie au début de chaque session de médias.

La définition correcte du type de flux est fondamentale pour la création de rapports sur les médias en flux continu. Elle active les segments **Type de diffusion multimédia** intégrés dans Adobe Analytics (Tous les médias, Audio uniquement, Vidéo uniquement) et génère des rapports audio et vidéo distincts dans Customer Journey Analytics. Cela permet également de s’assurer que les données de session sont correctement classées tout au long du pipeline Media Analytics. Les sessions avec un type de flux non défini ou non valide peuvent être dissociées ou mal classées dans les rapports en aval.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.streamType` |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.streamType` |
| **Obligatoire** | Oui |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

`streamType` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmettez `Media.MediaType.Video` ou `Media.MediaType.Audio` comme argument `mediaType` à `createMediaObject`. Notez que l’argument `streamType` dans `createMediaObject` contrôle la variable de type Contenu (VOD, Live, etc.), et non cette variable.

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Transmettez `Media.MediaType.Video` ou `Media.MediaType.Audio` comme argument `mediaType` à `createMediaObject`. Notez que l’argument `streamType` dans `createMediaObject` contrôle la variable de type Contenu (VOD, Live, etc.), et non cette variable.

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

`streamType` à l’intérieur des `xdm.mediaCollection.sessionDetails` lors de l’appel de `createMediaSession` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `streamType` à l’intérieur du `xdm.mediaCollection.sessionDetails` :

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
          "streamType": "video"
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

Transmettez `ADB.Media.MediaType.Video` ou `ADB.Media.MediaType.Audio` comme cinquième argument à `Media.createMediaObject` :

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB  Chromecast ]

Transmettez `ADBMobile.media.MediaType.Video` ou `ADBMobile.media.MediaType.Audio` comme cinquième argument à `ADBMobile.media.createMediaObject` :

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB  API Media Collection ]

Incluez `media.streamType` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes et tous les champs obligatoires.

>[!ENDTABS]
