---
title: Changement de débit
description: Déclenchez un événement de changement de débit dès que le lecteur passe à un autre débit.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 11%

---


# Changement de débit

>[!BEGINSHADEBOX]

*Cette page explique comment implémenter des événements de changement de débit. Voir [Modifications de débit (dimension)](/help/reporting/dimensions/bitrate-changes.md) et [Modifications de débit (mesure)](/help/reporting/metrics/bitrate-changes.md) pour les variables de rapports correspondantes.*

>[!ENDSHADEBOX]

L’événement de changement de débit indique que le lecteur est passé à un autre débit. Mettez d’abord à jour la valeur [Bitrate](/help/implementation/variables/quality/bitrate.md) sur l’objet QoE, puis déclenchez l’événement de changement de débit. Le serveur principal utilise le nombre de ces événements pour calculer la dimension et la mesure Modifications du débit , et les valeurs de débit obtenues alimentent le débit moyen.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | (aucun : comptabilisé par le serveur principal) |
| **Type d’événement XDM** | `media.bitrateChange` |
| **Obligatoire** | Non |
| **Envoyé avec** | Lorsque le lecteur change de débit |

## SDK web

Utilisez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) pour envoyer un événement `media.bitrateChange` avec le nouveau débit :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## SDK mobile

Mettez à jour l’objet QoE avec le nouveau débit, puis déclenchez l’événement de changement de débit.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

Utilisez `sendMediaEvent` avec `media.bitrateChange` pour signaler un changement de débit. Inclure le nouveau débit dans `qoeDataDetails` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) avec le `qoeDataDetails` mis à jour :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## SDK Media

Mettez à jour l’objet QoE et déclenchez l’événement :

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## API Media Collection

Envoyez une `bitrateChange` requête POST avec le nouveau débit :

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

Consultez la [référence des événements de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) pour obtenir la structure complète des requêtes.
