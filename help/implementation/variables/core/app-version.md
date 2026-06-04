---
title: Version de l’application
description: Configurez la chaîne de version de votre application de lecteur multimédia.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# Version de l’application

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Version de l’application**. Voir [Version de l’application](/help/reporting/dimensions/app-version.md) pour la dimension de reporting correspondante.*

>[!ENDSHADEBOX]

La variable de version d’application identifie la version de votre application de lecteur multimédia. Définissez-la une fois lors de l’initialisation de SDK ; la valeur est automatiquement incluse dans chaque requête de démarrage de session suivante. Utilisez une chaîne de version correspondant au cycle de publication de votre application (par exemple, `"2.1.0"` ou `"prod-YYYY-03-15"`).

>[!NOTE]
>
>Ce champ capture la version de votre **application de lecteur multimédia**, et non la bibliothèque SDK Adobe. La version de la bibliothèque SDK d’Adobe est collectée automatiquement en tant que champ interne distinct.

| Propriété | Valeur |
| --- | --- |
| **champ de collection XDM** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Paramètre de l’API Media Collection** | `media.sdkVersion` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de la session](/help/implementation/events/session/session-start.md) |

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Définissez `appVersion` dans l’objet de configuration `streamingMedia` lors de l’appel de [`configure`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/configure/streamingmedia) :

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

Définissez `edgeMedia.appVersion` dans la configuration de l’application avant d’initialiser le suivi multimédia :

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

Définissez `edgeMedia.appVersion` dans la configuration de l’application avant d’initialiser le suivi multimédia :

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku]

Définissez la version de l’application dans la configuration SDK à l’aide de `ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION` :

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB  API Media Edge ]

Incluez `appVersion` dans l’objet `sessionDetails` de la requête [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) :

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
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

Définissez `appVersion` sur l’objet `MediaConfig` avant d’appeler `ADB.Media.configure` :

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB  Chromecast ]

Définissez `sdkVersion` dans la section `mediaHeartbeat` de la configuration ADBMobile. Ce champ capture la version de votre application de lecteur, et non la version de la bibliothèque SDK Chromecast.

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB  API Media Collection ]

Incluez `media.sdkVersion` dans l’objet `params` de votre `sessionStart` requête POST :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.

>[!ENDTABS]
