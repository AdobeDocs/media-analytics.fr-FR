---
title: Images perdues
description: Définissez le nombre d’images perdues en cours d’exécution sur l’objet QoE afin que le serveur principal puisse signaler la qualité de la perte d’images.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 12%

---


# Images perdues

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Images perdues**. Voir [Images perdues](/help/reporting/dimensions/dropped-frames.md) pour la dimension et la mesure de reporting correspondantes.*

>[!ENDSHADEBOX]

La variable images perdues correspond au nombre d’images perdues par le lecteur au cours de la session. Définissez-le sur l’objet QoE et mettez à jour la valeur à chaque fois que le lecteur signale de nouveaux abandons. Le serveur principal signale la dernière valeur à la fermeture de la session.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.qoe.droppedFrameCount` |
| **champ de collection XDM** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.qoe.droppedFrameCount` |
| **Obligatoire** | Non |
| **Envoyé avec** | Événements de qualité ([changement de débit](/help/implementation/events/playback/bitrate-change.md), [début de la mémoire tampon](/help/implementation/events/playback/buffer-start.md), [erreur](/help/implementation/events/error.md)), fermeture de la session |

## SDK web

`droppedFrames` à l’intérieur des `mediaCollection.qoeDataDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK mobile

Transmettez les images perdues comme quatrième argument à `createQoEObject`. Mettez à jour le dispositif de suivi avant le déclenchement d’un événement de qualité.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

`droppedFrames` à l’intérieur des `mediaCollection.qoeDataDetails` lors de l’appel de `sendMediaEvent` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) avec `droppedFrames` à l’intérieur du `mediaCollection.qoeDataDetails` :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## SDK Media

Transmettez les images perdues comme quatrième argument à `ADB.Media.createQoEObject` :

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## API Media Collection

Incluez `media.qoe.droppedFrames` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
