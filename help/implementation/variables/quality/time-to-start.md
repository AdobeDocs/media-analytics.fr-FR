---
title: Heure de début
description: Définissez l’heure de démarrage du lecteur, en millisecondes, de sorte que le serveur principal puisse signaler la qualité du délai de première image.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 12%

---


# Heure de début

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Time to start**. Voir [Heure de début](/help/reporting/dimensions/time-to-start.md) pour la dimension et la mesure de reporting correspondantes.*

>[!ENDSHADEBOX]

La variable time to start correspond au temps écoulé, en millisecondes, entre le lancement de la lecture par le lecteur et le premier rendu d’image. Définissez-le sur l’objet QoE avant que l’événement de début de session ne se déclenche. Adobe stocke et signale la valeur en secondes ; transmettez les millisecondes et Adobe convertit au moment de l’ingestion.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.qoe.timeToStart` |
| **champ de collection XDM** | [`mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.qoe.timeToStart` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

Définissez `timeToStart` à l’intérieur du `mediaCollection.qoeDataDetails` sur `media.sessionStart` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’heure de démarrage comme deuxième argument (`startupTime`) à `createQoEObject`.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Définissez `timeToStart` à l’intérieur du `mediaCollection.qoeDataDetails` sur `media.sessionStart` lors de l’appel de `createMediaSession` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `timeToStart` à l’intérieur du `mediaCollection.qoeDataDetails` :

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
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’heure de début comme deuxième argument à `ADB.Media.createQoEObject` :

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## API Media Collection

Incluez `media.qoe.timeToStart` dans l’objet `params` sur `sessionStart` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
