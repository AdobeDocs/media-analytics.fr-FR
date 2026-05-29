---
title: Démarrage de la pause
description: Signale que l’utilisateur a suspendu la lecture du média.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 10%

---


# Démarrage de la pause

L’événement pause start indique que l’utilisateur a suspendu la lecture. Il n’existe pas d’événement de reprise distinct ; envoyez un événement [Play](play.md) lors de la reprise de la lecture.

* **Conditions préalables** : [début de session](../session/session-start.md)
* **Mesure associée** : [[!UICONTROL Événements de pause]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>Il n’existe aucun type d’événement de reprise. La reprise est déduite lorsque vous envoyez un événement [`play`](play.md) après `pauseStart`.

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.pauseStart"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

>[!TAB iOS]

Appelez `trackPause` lorsque l’utilisateur met la lecture en pause.

```swift
tracker.trackPause()
```

>[!TAB Android]

Appelez `trackPause` lorsque l’utilisateur met la lecture en pause.

```kotlin
tracker.trackPause()
```

>[!TAB Roku]

Appelez `sendMediaEvent` avec `eventType: "media.pauseStart"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
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

Appelez `trackPause` lorsque l’utilisateur met la lecture en pause :

```javascript
tracker.trackPause();
```

>[!TAB  Chromecast ]

Appelez `trackPause` lorsque l’utilisateur met la lecture en pause :

```javascript
ADBMobile.media.trackPause();
```

>[!TAB  API Media Collection ]

Envoyez une `pauseStart` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
