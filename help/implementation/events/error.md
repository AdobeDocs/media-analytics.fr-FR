---
title: Erreur
description: Indique que le lecteur multimédia a rencontré une erreur.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 9%

---


# Erreur

L’événement d’erreur indique que le lecteur multimédia a rencontré une erreur. Le suivi d’une erreur ne ferme pas la session. Si l’erreur empêche la lecture de continuer, appelez [Fin de session](session/session-end.md) après l’événement d’erreur.

* **Conditions préalables** : [début de session](session/session-start.md)
* **Mesure associée** : [[!UICONTROL Flux impactés par l’erreur]](/help/reporting/metrics/error-impacted-streams.md)

La propriété `errorDetails.source` accepte uniquement deux valeurs : `player` (erreurs provenant du lecteur multimédia) et `external` (erreurs provenant d’une source externe telle qu’un réseau de diffusion de contenu ou un réseau).

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Appelez [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) avec les `eventType: "media.error"` et les `errorDetails` requises :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

>[!TAB iOS]

Appelez `trackError` avec une chaîne d&#39;ID d&#39;erreur.

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

Appelez `trackError` avec une chaîne d&#39;ID d&#39;erreur.

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Roku Edge]

Appelez `sendMediaEvent` avec les `eventType: "media.error"` et les `errorDetails` requises :

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

>[!TAB  API Media Edge ]

Appelez le point d’entrée [error](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) avec la `errorDetails` requise :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
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

Appelez `trackError` avec une chaîne d&#39;ID d&#39;erreur :

```javascript
tracker.trackError("media-error-001");
```

>[!TAB  Chromecast ]

Appelez `trackError` avec une chaîne d&#39;ID d&#39;erreur :

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB Roku 2.x]

Appelez `mediaTrackError` avec un ID d’erreur et la source de l’erreur. Utilisez la constante `ERROR_SOURCE_PLAYER` pour les erreurs du lecteur :

```brightscript
adb = ADBMobile()
adb.mediaTrackError("media-error-001", adb.ERROR_SOURCE_PLAYER)
```

>[!TAB  API Media Collection ]

Envoyez une `error` POST au point d’entrée [événements](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) :

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```

>[!ENDTABS]
