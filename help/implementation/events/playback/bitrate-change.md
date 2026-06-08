---
title: Changement de débit
description: Signale que le débit de lecture a changé.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 6%

---


# Changement de débit

L’événement de changement de débit indique que le lecteur a négocié un nouveau débit de lecture. Envoyez-le chaque fois que le débit change pendant la lecture. Incluez la nouvelle valeur de débit dans les données de la QoE afin que le serveur principal puisse calculer [[!UICONTROL débit moyen]](/help/reporting/metrics/average-bitrate.md) et la dimension par débit-intervalle.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : [[!UICONTROL modifications de débit]](/help/reporting/metrics/bitrate-changes.md)

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.bitrateChange"` et le nouveau débit en `qoeDataDetails` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Créez un objet QoE avec le nouveau débit et mettez à jour le dispositif de suivi avant le déclenchement de l’événement de changement de débit.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Créez un objet QoE avec le nouveau débit et mettez à jour le dispositif de suivi avant le déclenchement de l’événement de changement de débit.

```kotlin
val qoeObject = Media.createQoEObject(3200, 0, 24, 0)

tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku Edge]

Appelez `sendMediaEvent` avec `eventType: "media.bitrateChange"` et le nouveau débit en `qoeDataDetails` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/) avec le nouveau débit en `qoeDataDetails` :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bitrateChange?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Créez un objet QoE avec le nouveau débit et mettez à jour le dispositif de suivi :

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB  Chromecast ]

Mettez à jour l’objet QoS renvoyé par le délégué `getQoSObject`, puis suivez l’événement :

```javascript
// Update QoS data via the delegate
this._qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // dropped frames
  24,    // fps
  0      // startup time
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

Créez un objet QoS avec le nouveau débit binaire à l’aide de `adb_media_init_qosinfo`, mettez à jour le dispositif de suivi avec `mediaUpdateQoS`, puis suivez l’événement. Notez l’ordre des paramètres Roku : `bitrate, startupTime, fps, droppedFrames`.

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB  API Media Collection ]

Envoyez une `bitrateChange` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) avec le nouveau débit en `qoeData` :

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "qoeData": {
    "media.qoe.bitrate": 3200
  }
}
```

>[!ENDTABS]
