---
title: Session terminée
description: Signale que la visionneuse a atteint la fin du contenu principal.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 8%

---


# Session terminée

L’événement de fin de session indique que la visionneuse a atteint la fin du contenu principal. La session n’est pas fermée immédiatement ; elle reste ouverte jusqu’à ce qu’elle expire naturellement. Si vous souhaitez fermer la session immédiatement, appelez plutôt [Fin de session](session-end.md).

* **Conditions préalables** : [début de session](session-start.md)
* **Mesure associée** : [[!UICONTROL Contenu terminé]](/help/reporting/metrics/content-completes.md)

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec `eventType: "media.sessionComplete"` :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

>[!TAB iOS]

Appelez `trackComplete` lorsque le lecteur multimédia atteint la fin du contenu.

```swift
tracker.trackComplete()
```

>[!TAB Android]

Appelez `trackComplete` lorsque le lecteur multimédia atteint la fin du contenu.

```kotlin
tracker.trackComplete()
```

>[!TAB Roku Edge]

Appelez `sendMediaEvent` avec `eventType: "media.sessionComplete"` :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete) :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
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

Appelez `trackComplete` lorsque le lecteur multimédia atteint la fin du contenu :

```javascript
tracker.trackComplete();
```

>[!TAB  Chromecast ]

Appelez `trackComplete` lorsque le lecteur multimédia atteint la fin du contenu :

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB Roku 2.x]

Appelez `mediaTrackComplete` lorsque le lecteur multimédia atteint la fin du contenu :

```brightscript
ADBMobile().mediaTrackComplete()
```

>[!TAB  API Media Collection ]

Envoyez une `sessionComplete` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
