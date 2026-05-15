---
title: Autorisé
description: Marquez une session comme authentifiée via Adobe Pass afin qu’elle soit comptabilisée dans l’événement Autorisé.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 15%

---


# Autorisé

>[!BEGINSHADEBOX]

*Cette page traite de la collecte de données pour la variable **Autorisée**. Voir [Autorisé](/help/reporting/metrics/authorized.md) pour la mesure de reporting correspondante.*

>[!ENDSHADEBOX]

La variable autorisée marque une session dont l’utilisateur a été autorisé via Adobe Pass/TV-Everywhere. Définissez-la sur `"TRUE"` lorsqu’une autorisation est confirmée, sans quoi elle sera désactivée. Associez à [](/help/implementation/variables/standard-metadata/mvpd.md) pour ventiler l&#39;authentification par fournisseur.

| Propriété | Valeur |
| --- | --- |
| **Variable de données contextuelles** | `a.media.pass.auth` |
| **champ de collection XDM** | [`mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Caractéristique** | `c_contextdata.a.media.pass.auth` |
| **Obligatoire** | Non |
| **Envoyé avec** | [Début de session](/help/implementation/events/session/session-start.md), fermeture de session |

## SDK web

`authorized` à l’intérieur des `mediaCollection.sessionDetails` lors de l’appel de [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview) :

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        authorized: "TRUE"
      },
      playhead: 0
    }
  }
});
```

## SDK mobile

Transmettez l’indicateur autorisé en tant que clé de métadonnées dans l’argument HashMap à `trackSessionStart`. Utilisez `MediaConstants.VideoMetadataKeys.AUTHORIZED`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Utilisez `createMediaSession` pour définir des `authorized` dans `sessionDetails` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "authorized": "TRUE"
            },
            "playhead": 0
        }
    }
})
```

## API Media Edge

Appelez le point d’entrée [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) avec `authorized` à l’intérieur du `mediaCollection.sessionDetails` :

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
          "authorized": "TRUE"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK Media

Transmettez l’indicateur autorisé dans l’objet `contextData` à l’aide de `ADB.Media.VideoMetadataKeys.Authorized` :

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API Media Collection

Incluez `media.pass.auth` dans l’objet `params` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.auth": "TRUE"
  }
}
```

Consultez la [référence des sessions de l’API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour obtenir la structure complète des requêtes.
