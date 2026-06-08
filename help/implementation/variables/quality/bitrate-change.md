---
title: Changement de débit
description: Déclenchez un événement de changement de débit dès que le lecteur passe à un autre débit.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%

---


# Changement de débit

>[!BEGINSHADEBOX]

*Cette page explique comment implémenter des événements de changement de débit. Voir [[!UICONTROL Modifications de débit] (dimension)](/help/reporting/dimensions/bitrate-changes.md) et [[!UICONTROL Modifications de débit] (mesure)](/help/reporting/metrics/bitrate-changes.md) pour les variables de rapport correspondantes.*

>[!ENDSHADEBOX]

L’événement de changement de débit indique que le lecteur est passé à un autre débit. Mettez d’abord à jour la valeur [Bitrate](/help/implementation/variables/quality/bitrate.md) sur l’objet QoE, puis déclenchez l’événement de changement de débit. Le serveur principal utilise le nombre de ces événements pour calculer la mesure [[!UICONTROL Changements de débit]](/help/reporting/dimensions/bitrate-changes.md) de dimension et [[!UICONTROL Changements de débit]](/help/reporting/metrics/bitrate-changes.md), ainsi que les valeurs de débit qui en résultent pour alimenter [[!UICONTROL Débit moyen]](/help/reporting/metrics/average-bitrate.md).

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | (aucun : comptabilisé par le serveur principal) |
| **Type d’événement XDM** | `media.bitrateChange` |
| **Caractéristique** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Changement de débit](/help/implementation/events/playback/bitrate-change.md) |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

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

>[!TAB iOS]

Mettez à jour l’objet QoE avec le nouveau débit, puis déclenchez l’événement de changement de débit.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Mettez à jour l’objet QoE avec le nouveau débit, puis déclenchez l’événement de changement de débit.

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB  API Media Edge ]

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

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Mettez à jour l’objet QoE et déclenchez l’événement :

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB  Chromecast ]

Mettez à jour l’objet QoS avec le nouveau débit, puis déclenchez l’événement de changement de débit :

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  4500,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

Mettez à jour l’objet QoS avec le nouveau débit, puis déclenchez l’événement de changement de débit :

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(4500.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB  API Media Collection ]

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

>[!ENDTABS]
