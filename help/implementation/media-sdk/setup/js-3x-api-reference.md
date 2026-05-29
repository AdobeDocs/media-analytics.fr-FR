---
title: Référence de l’API JavaScript 3.x Media SDK
description: Référence d’API pour Media SDK JavaScript 3.x (classes ADB.Media et ADB.MediaConfig).
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# Référence de l’API JavaScript 3.x Media SDK

>[!BEGINSHADEBOX]

Cette page couvre le SDK JavaScript 3.x uniquement pour Analytics. Pour connaître la mise en œuvre recommandée, voir [Implémentation de Streaming Media à l’aide d’Edge Network](/help/implementation/edge/edge-web-sdk.md).

>[!ENDSHADEBOX]

## ADB.Media

### Méthodes statiques

+++configure

Configure le SDK Media pour le suivi. Cette méthode doit être appelée une seule fois avant de créer des instances de suivi dans une page.

**Syntaxe**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| Nom de variable | Type | Description |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | Configuration de média valide |
| `appMeasurement` | objet | Instance AppMeasurement |

**Exemple**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

Crée une instance de média pour effectuer le suivi de la session de lecture. Renvoie `null` si appelé avant la configuration du média.

**Syntaxe**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| Nom de variable | Type | Obligatoire | Description |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | Configuration du dispositif de suivi | Non | Objet de configuration du suivi. |

**Exemple**

```javascript
var tracker = ADB.Media.getInstance();
```

Pour remplacer `channel` ou `playerName` par instance de suivi, transmettez les valeurs de remplacement dans l’objet de configuration du suivi.

**Exemple avec configuration du tracker**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

Crée un objet contenant des informations sur le média. Renvoie un objet vide si des paramètres non valides sont transmis.

**Syntaxe**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| Nom de variable | Type | Description |
| :--- | :--- | :--- |
| `name` | string | Chaîne non vide indiquant le nom du média |
| `id` | string | Chaîne non vide indiquant l’identifiant unique du média |
| `length` | number | Nombre positif désignant la longueur du média en secondes. Utilisez `0` si la longueur est inconnue. |
| `streamType` | string | Type de diffusion ou chaîne non vide pour indiquer le type de diffusion multimédia. |
| `mediaType` | Type de média | Type de média (audio ou vidéo) |

**Exemple**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

Crée un objet contenant des informations sur l’arrêt. Renvoie un objet vide si des paramètres non valides sont transmis.

**Syntaxe**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| Nom de variable | Type | Description |
| :--- | :--- | :--- |
| `name` | string | Chaîne non vide indiquant le nom de l’adresse (pre-roll, mid-roll et post-roll) |
| `position` | number | Position du nombre de la coupure publicitaire dans le contenu, en commençant par 1 |
| `startTime` | number | Valeur du curseur de lecture au début de la coupure publicitaire. |

**Exemple**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

Crée un objet contenant des informations publicitaires. Renvoie un objet vide si des paramètres non valides sont transmis.

**Syntaxe**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| Nom de variable | Type | Description |
| :--- | :--- | :--- |
| `name` | string | Chaîne non vide indiquant le nom de l’annonce |
| `id` | string | Chaîne non vide indiquant l’ID d’annonce |
| `position` | number | Position du nombre de l’annonce publicitaire dans le saut de page, en commençant par 1 |
| `length` | number | Nombre positif indiquant la longueur de la publicité |

**Exemple**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

Crée un objet contenant des informations sur le chapitre. Renvoie un objet vide si des paramètres non valides sont transmis.

**Syntaxe**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| Nom de variable | Type | Description |
| :--- | :--- | :--- |
| `name` | string | Chaîne non vide indiquant le nom du chapitre |
| `position` | number | Position du chapitre dans le contenu, en commençant par 1 |
| `length` | number | Nombre positif indiquant la longueur du chapitre |
| `startTime` | number | Valeur du curseur de lecture au début du chapitre |

**Exemple**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

Crée un objet contenant des informations sur l’état. Renvoie un objet vide si des paramètres non valides sont transmis.

**Syntaxe**

```javascript
ADB.Media.createStateObject(name)
```

| Nom de variable | Type | Description |
| :--- | :--- | :--- |
| `name` | string | État du lecteur ou chaîne non vide indiquant le nom de l’état |

**Exemple**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

Crée un objet contenant des informations sur la qualité de service. Renvoie un objet vide si des paramètres non valides sont transmis.

**Syntaxe**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| Nom de variable | Type | Description |
| :--- | :--- | :--- |
| `bitrate` | number | Nombre positif indiquant le débit courant (0 si inconnu) |
| `startupTime` | number | Nombre positif indiquant l’heure de démarrage (0 si inconnu) |
| `fps` | number | Nombre positif indiquant le nombre de fps en cours (0 si inconnu) |
| `droppedFrames` | number | Nombre positif indiquant le nombre d&#39;images perdues (0 si inconnu) |

**Exemple**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

Renvoie la version du SDK Media.

**Syntaxe**

```javascript
ADB.Media.version
```

**Exemple**

```javascript
console.log(ADB.Media.version);
```

+++

### Méthodes d’instance

+++trackSessionStart

Effectuez le suivi de l’intention de démarrer la lecture. Une session de suivi est ainsi lancée sur l’instance de suivi multimédia. Voir aussi Reprise du média.

**Syntaxe**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| Nom de variable | Description | Obligatoire |
| :--- | :--- | :---: |
| `mediaObject` | Informations sur le média créées à l’aide de la méthode `createMediaObject`. | Oui |
| `contextData` | Données contextuelles de média facultatives. Pour les clés de métadonnées standard, utilisez des constantes vidéo ou audio standard. | Non |

**Exemple**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

Effectuez le suivi de la lecture multimédia ou reprenez après une pause précédente.

**Syntaxe**

```javascript
ADB.Media.trackPlay();
```

**Exemple**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

Suivi de la pause du média.

**Syntaxe**

```javascript
ADB.Media.trackPause();
```

**Exemple**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

Suivi du média terminé. Appelez cette méthode uniquement lorsque le média a été entièrement visionné.

**Syntaxe**

```javascript
ADB.Media.trackComplete();
```

**Exemple**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

Effectuez le suivi de la fin d’une session de visualisation. Appelez cette méthode même si l’utilisateur ne voit pas le média jusqu’à la fin.

**Syntaxe**

```javascript
ADB.Media.trackSessionEnd();
```

**Exemple**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

Effectue le suivi d’une erreur lors de la lecture du média.

**Syntaxe**

```javascript
ADB.Media.trackError(errorId);
```

| Nom de variable | Description | Obligatoire |
| :--- | :--- | :---: |
| `errorId` | Chaîne non vide contenant les informations d&#39;erreur | Oui |

**Exemple**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

Méthode de suivi des événements multimédia.

| Nom de variable | Description |
| :--- | :--- |
| `event` | Événement multimédia |
| `info` | Pour `AdBreakStart` événement , les informations adbreak sont créées à l&#39;aide de la méthode `createAdBreakObject`. Pour `AdStart` événement , les informations publicitaires sont créées à l’aide de la méthode `createAdObject` . Pour `ChapterStart` événement , les informations de chapitre sont créées à l’aide de la méthode `createChapterObject` . Pour les événements `StateStart` et `StateEnd`, les informations d’état sont créées à l’aide de la méthode `createStateObject` . Cela n’est pas nécessaire pour les autres événements. |
| `contextData` | Des données contextuelles facultatives peuvent être fournies pour les événements `AdStart` et `ChapterStart`. Cela n’est pas nécessaire pour les autres événements. |

**Syntaxe**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**Exemples**

**Suivi des coupures publicitaires**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**Suivi des publicités**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**Suivi des chapitres**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**États du tracking**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**Suivi des événements de lecture**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**Suivi des modifications du débit**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

Fournissez le curseur de lecture multimédia actuel au dispositif de suivi multimédia. Pour un suivi précis, appelez cette méthode chaque fois que le curseur de lecture change pendant la lecture.

**Syntaxe**

```javascript
ADB.Media.updatePlayhead(time);
```

| Nom de variable | Description |
| :--- | :--- |
| `time` | Curseur actuel en secondes. Pour la vidéo à la demande (VOD), la valeur est spécifiée en secondes à partir du début de l’élément média. Pour la diffusion en direct, si le lecteur ne fournit pas d’informations sur la durée du contenu, la valeur peut être spécifiée comme le nombre de secondes écoulées depuis minuit UTC de ce jour. Remarque : lors de l’utilisation de marques de progression, la durée du contenu est une donnée obligatoire et le curseur de lecture doit être mis à jour en tant que nombre de secondes écoulées depuis le début de l’élément média, en commençant par 0. |

**Exemple**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

Fournit les informations QoE actuelles au suivi multimédia. Pour un suivi précis, appelez cette méthode plusieurs fois lorsque le lecteur multimédia fournit les informations de QoE mises à jour.

**Syntaxe**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| Nom de variable | Description |
| :--- | :--- |
| `qoeObject` | Informations QoE actuelles créées à l’aide de la méthode `createQoEObject`. |

**Exemple**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++détruire

Détruit l’instance de suivi.

**Syntaxe**

```javascript
ADB.Media.destroy();
```

**Exemple**

```javascript
tracker.destroy();
```

+++

### Constantes

+++Configuration du dispositif de suivi

Définit les clés de configuration qui peuvent être définies par instance de suivi.

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++Type de média

Définit le type d’un média qui fait l’objet d’un suivi.

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++Type de diffusion

Définit le type de flux du contenu qui fait actuellement l’objet d’un suivi.

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++Clés de métadonnées standard

`ADB.Media.VideoMetadataKeys`, `ADB.Media.AudioMetadataKeys` et `ADB.Media.AdMetadataKeys` fournissent les chaînes clés de données contextuelles pour les métadonnées standard. Pour obtenir la liste complète des clés et des variables de création de rapports correspondantes, reportez-vous à la [Référence de variable de métadonnées standard](/help/implementation/variables/standard-metadata/show.md).

+++

+++Événements multimédia

Définit le type d’un événement de tracking.

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++États du lecteur

Définit des valeurs standard pour le suivi de l’état du lecteur.

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++CV multimédia

Constante indiquant que la session de suivi en cours reprend une session précédemment fermée. Ces informations doivent être fournies lors du démarrage d&#39;une session de tracking.

**Syntaxe**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**Exemple**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| Clé | Obligatoire | Description |
| :--- | :--- | :--- |
| `trackingServer` | Oui | Saisissez le nom du serveur d’API de collecte de médias auquel les données de suivi multimédia téléchargées doivent être envoyées. Contactez votre représentant de compte Adobe pour recevoir ces informations. |
| `channel` | Non | Propriété du nom de canal |
| `playerName` | Non | Nom du lecteur multimédia utilisé |
| `appVersion` | Non | Saisissez la version de l’application du lecteur multimédia/SDK |
| `debugLogging` | Non | Active ou désactive les journaux Media SDK (valeur par défaut : `false`) |
| `ssl` | Non | Envoie des pings via SSL (valeur par défaut : `true`) |
