---
title: Mappage des données de l’API Media Edge et validation de la plateforme
description: Découvrez quels événements d’API Media Edge génèrent des événements d’expérience dans Adobe Experience Platform et comment valider votre implémentation à l’aide du schéma XDM mediaReporting.
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85eid: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 764
ht-degree: 4%

---


# Mappage des données de l’API Media Edge et validation de la plateforme

Lorsque vous envoyez des événements de suivi multimédia à l’aide de l’API Media Edge ou d’un SDK Media Edge, le serveur principal Media Analytics traite ces événements et écrit les événements d’expérience calculés dans les jeux de données Adobe Experience Platform. Comprendre quels événements atteignent Platform et ce que le serveur principal calcule pour vous permet de valider votre implémentation et de créer des rapports précis dans Customer Journey Analytics ou Adobe Analytics.

Media Edge utilise deux schémas XDM distincts :

| Schéma | Espace de noms | Direction | Rôle |
|---|---|---|---|
| Media Collection | `xdm.mediaCollection` | Client → Adobe | Ce que votre lecteur envoie pour chaque événement de suivi |
| Rapports multimédias | `xdm.mediaReporting` | Adobe → Platform | Ce que le serveur principal écrit dans les jeux de données après traitement |

Les champs présents dans `mediaReporting`, mais absents de votre payload `mediaCollection`, sont **calculés par le serveur principal** ; ils sont dérivés de la séquence complète d’événements d’une session. Ces champs ne sont jamais envoyés, ils sont générés par Adobe.

## Événements qui écrivent dans les jeux de données Platform

Sur les 12 types d’événements pouvant faire l’objet d’un suivi, seuls cinq génèrent des écritures d’événement d’expérience individuelles dans les jeux de données :

| Type d’événement | Inclus dans les jeux de données | Notes |
|---|---|---|
| [Début de la session](/help/implementation/events/session/session-start.md) | Oui | Ecrit à l’initialisation de la session |
| [Début de la publicité](/help/implementation/events/ads/ad-start.md) | Oui | Écrit lorsqu’une publicité individuelle commence |
| [Publicité terminée](/help/implementation/events/ads/ad-complete.md) | Oui | Écrit lorsqu’une publicité est lue jusqu’à la fin |
| [Chapitre terminé](/help/implementation/events/chapters/chapter-complete.md) | Oui | Écrit lorsqu’un chapitre est lu jusqu’à la fin |
| [Fin de la session](/help/implementation/events/session/session-complete.md) | Oui | Écrit à la fin de la session ; champ calculé le plus riche défini |
| [Lecture](/help/implementation/events/playback/play.md) | Non | Utilisé pour calculer les `timePlayed` |
| [Démarrer la pause](/help/implementation/events/playback/pause-start.md) | Non | Utilisé pour calculer les `pauseCount` et les `pauseTime` |
| [ Ping ](/help/implementation/events/playback/ping.md) | Non | Heartbeat ; utilisé pour détecter l’inactivité de session |
| [ Début de la mémoire tampon ](/help/implementation/events/playback/buffer-start.md) | Non | Utilisé pour calculer les mesures du tampon QoE |
| [Changement de débit](/help/implementation/events/playback/bitrate-change.md) | Non | Utilisé pour calculer les mesures de débit QoE |
| [Début état](/help/implementation/events/player-state/state-start.md) | Non | Utilisé pour calculer les mesures d’état du lecteur |
| [Erreur](/help/implementation/events/error.md) | Non | Utilisé pour calculer les `errorCount` dans QoE |

## Champs calculés du serveur principal

Les champs suivants apparaissent dans les payloads `mediaReporting`, mais ne font jamais partie de la payload de collection. Le serveur principal les dérive de la séquence d’événements complète.

**Niveau de session** (s’affiche sur `sessionComplete`) :

| Champ | Description |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | Durée totale en secondes du contenu principal lu, publicités exclues |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | Nombre total de secondes écoulées, publicités comprises |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | Secondes dédupliquées : les intervalles consultés plus d&#39;une fois ne sont comptabilisés qu&#39;une seule fois |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed` divisé par la longueur du contenu |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | Flux simultanés estimés |
| `xdm.mediaReporting.sessionDetails.adCount` | Nombre de publicités ayant démarré |
| `xdm.mediaReporting.sessionDetails.chapterCount` | Nombre de chapitres ayant démarré |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | Fréquence et durée totale de la pause |
| `xdm.mediaReporting.sessionDetails.hasProgress10` ... `xdm.mediaReporting.sessionDetails.hasProgress95` | Indicateurs de jalon de progression (10 %, 25 %, 50 %, 75 %, 95 %) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | Si au moins une image de contenu a été vue |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | Indicateurs d’achèvement et de début |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | Durée entre le dernier ping et la fermeture de session |
| `xdm.mediaReporting.sessionDetails.segment` | Crochet du segment de contenu (par exemple, `[0-1]`) |

**Niveau de l’annonce** (apparaît sur `adComplete`) :

| Champ | Description |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | Secondes de lecture du contenu publicitaire |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | Indique si l’annonce a été lue jusqu’à la fin. |

**Au niveau du chapitre** (apparaissant sur `chapterComplete`) :

| Champ | Description |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | Secondes de lecture du contenu du chapitre |
| `xdm.mediaReporting.chapterDetails.isCompleted` | Indique si le chapitre a été lu jusqu’à la fin. |
| `xdm.mediaReporting.chapterDetails.isStarted` | Indique si le chapitre a démarré. |

**QoE** (agrégé sur `sessionComplete`) :

| Champ | Description |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | Débit moyen sur l’ensemble de la session |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | Plage de débits moyens regroupés |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | Nombre de changements de débit |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | Nombre d’erreurs |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | Nombre total d’images perdues |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | Tableau de codes d’erreur du lecteur |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | Si une erreur s’est produite |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | Si des images ont été perdues |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | Si des changements de débit se sont produits |

## Contenu téléchargé

Pour les sessions suivies à l’aide du point d’entrée [téléchargé](/help/use-cases/track-downloaded-content.md), le serveur principal définit automatiquement le `xdm.mediaReporting.sessionDetails.isDownloaded` sur `true` sur l’événement de création de rapports `sessionStart`. Tous les autres événements de création de rapports pour les sessions téléchargées suivent le même schéma que les sessions actives. Utilisez ce champ dans CJA ou Adobe Analytics pour filtrer ou segmenter la lecture téléchargée.

Voir [Point d’entrée téléchargé](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/) dans Référence de l’API Media Edge pour les détails d’implémentation de la collection.

## Valider votre mise en œuvre

Après avoir envoyé des événements par le biais de l’API Media Edge, vérifiez que vos données ont bien atterri en utilisant l’une des méthodes suivantes :

**Aperçu du jeu de données**

1. Dans [CX Enterprise](https://experience.adobe.com), accédez à **[!UICONTROL Jeux de données]** et sélectionnez votre jeu de données de médias en flux continu.
2. Sélectionnez **[!UICONTROL Prévisualiser le jeu de données]** pour afficher les événements d’expérience les plus récemment ingérés.
3. Vérifiez que `eventType` valeurs telles que `media.sessionStart` et `media.sessionComplete` s’affichent avec des champs de `mediaReporting` renseignés.

**inspection du jeu de données**

1. Dans CJA, ouvrez la connexion associée à votre jeu de données de médias en flux continu.
2. Sélectionnez **Ajouter des jeux de données** et examinez le schéma pour confirmer que les champs `mediaReporting` sont mappés aux dimensions et mesures attendues.

**Règles de traitement Adobe Analytics (si vous utilisez la destination Analytics)**

Pour les suites de rapports Adobe Analytics recevant des données via le connecteur source Analytics, vous pouvez utiliser des règles de traitement pour mapper des variables de données contextuelles `mediaReporting` à des props ou des eVars personnalisées. L’indicateur `isDownloaded` est disponible en tant que `a.media.downloaded`.

## Exemples de payload XDM

Les exemples suivants montrent la structure XDM `mediaReporting` complète pour chaque événement de création de rapports tel qu’il est écrit dans les jeux de données Platform. La propriété `_{tenantName}` représente l’espace de noms du client de votre organisation pour tous les champs personnalisés.

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart (contenu téléchargé)

Les sessions suivies à l’aide du point d’entrée [téléchargé](/help/use-cases/track-downloaded-content.md) suivent le même schéma de création de rapports avec une différence clé : `xdm.mediaReporting.sessionDetails.isDownloaded` est défini sur `true` sur l’événement de création de rapports `sessionStart`. Tous les autres types d’événements sont identiques aux exemples de contenu en direct ci-dessus.

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++
