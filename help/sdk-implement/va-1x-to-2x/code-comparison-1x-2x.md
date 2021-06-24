---
title: Comparaison de code v1.x vers v2.x
description: Découvrez la différence entre le code des versions 1.x et 2.x du SDK Media.
uuid: 9f0a1660-2100-446d-ab75-afdf966478b3
exl-id: c2324c6a-329f-44e2-bea0-9d43ef9c6ef7
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 96%

---

# Comparaison de code : 1.x vers 2.x {#code-comparison-x-to-x}

Tous les paramètres de configuration et toutes les API de suivi sont désormais consolidés dans les classes `MediaHeartbeats` et `MediaHeartbeatConfig`.

**Modifications de l’API de configuration :**

* `AdobeHeartbeatPluginConfig.sdk` - Renommé en `MediaConfig.appVersion`
* `MediaHeartbeatConfig.playerName` - Désormais défini par `MediaHeartbeatConfig` au lieu de `VideoPlayerPluginDelegate`
* (Pour JavaScript uniquement) : Instance `AppMeasurement` - Désormais envoyée via le constructeur `MediaHeartbeat`.

**Modifications des propriétés de configuration :**

* `sdk` - Renommé en `appVersion`
* `publisher` - Supprimé ; l’ID Experience Cloud Org est utilisée au lieu d’un éditeur
* `quiteMode` - Supprimée

**Liens vers les exemples de lecteurs 1.x et 2.x :**

* [Lecteur échantillon 1.x ](https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58)
* [Lecteur échantillon 2.x ](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/2.x/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L47)

Les sections suivantes fournissent des comparaisons de code entre les versions 1.x et 2.x, couvrant l’initialisation, la lecture principale, la lecture de publicité, la lecture de chapitre et certains événements supplémentaires.

## Comparaison de code VHL : INITIALISATION

### Initialisation d’objet

| API 1.x | API 2.x |
| --- | --- |
| `Heartbeat()` | `MediaHeartbeat()` |
| `VideoPlayerPlugin()` | `MediaHeartbeatConfig()` |
| `AdobeAnalyticsPlugin()` |  |
| `HeartbeatPlugin()` |  |

#### Initialisation du module du lecteur vidéo (1.x) {#plugin-init-1.x}

```js
this._playerPlugin = new VideoPlayerPlugin( new SampleVideoPlayerPluginDelegate(this._player));
var playerPluginConfig = new VideoPlayerPluginConfig();
playerPluginConfig.debugLogging = true;

// Set up the AppMeasurement plugin 
this._aaPlugin = new AdobeAnalyticsPlugin( appMeasurement, new SampleAdobeAnalyticsPluginDelegate());
var aaPluginConfig = new AdobeAnalyticsPluginConfig();
aaPluginConfig.channel = Configuration.HEARTBEAT.CHANNEL;
aaPluginConfig.debuglogging = true;
this._aaPlugin.configure(aaPluginConfig);

// Set up the AdobeHeartbeat plugin 
var ahPlugin = new AdobeHeartbeatPlugin( new SampleAdobeHeartbeatPluginDelegate());
var ahPluginConfig = new AdobeHeartbeatPluginConfig( configuration.HEARTBEAT.TRACKING_SERVER, configuration.HEARTBEAT.PUBLISHER);
ahPluginConfig.ovp = configuration.HEARTBEAT.OVP;
ahPluginConfig.sdk = configuration.HEARTBEAT.SDK;
ahPluginConfig.debugLogging = true;
ahPlugin.configure(ahPluginConfig);
var plugins = [this._playerPlugin, this._aaPlugin, ahPlugin];

// Set up and configure the heartbeat library this._heartbeat = new Heartbeat(new SampleHeartbeatDelegate(), plugins);
var configData = new HeartbeatConfig();
configData.debugLogging = true;
this._heartbeat.configure(configData);
```

#### Initialisation de Media Heartbeat (2.x) {#mh-init-2.x}

```js
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
mediaConfig.playerName = Configuration.PLAYER.NAME;
mediaConfig.debugLogging = true;
mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
mediaConfig.ssl = false;
mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
this._mediaHeartbeat = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

### Délégués

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate()` | `MediaHeartbeatDelegate()` |
| `VideoPlayerPluginDelegate().getVideoInfo` | `MediaHeartbeatDelegate().getCurrentPlaybackTime` |
| `VideoPlayerPluginDelegate().getAdBreakInfo` | `MediaHeartbeatDelegate().getQoSObject` |
| `VideoPlayerPluginDelegate().getAdInfo` |  |
| `VideoPlayerPluginDelegate().getChapterInfo` |  |
| `VideoPlayerPluginDelegate().getQoSInfo` |  |
| `VideoPlayerPluginDelegate().get.onError` |  |
| `AdobeAnalyticsPluginDelegate()` |  |

#### VideoPlayerPluginDelegate (1.x) {#player-plugin-delegate-1.x}

```js
$.extend(SampleVideoPlayerPluginDelegate.prototype, VideoPlayerPluginDelegate.prototype);

function SampleVideoPlayerPluginDelegate(player) { 
    this._player = player;
} 

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = function() { 
    return this._player.getAdBreakInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = function() { 
    return this._player.getQoSInfo();
};
```

#### AdobeAnalyticsPluginDelegate (1.x) {#analytics-plugin-delegate-1.x}

```js
$.extend(SampleAdobeAnalyticsPluginDelegate.prototype, AdobeAnalyticsPluginDelegate.prototype);

function SampleAdobeAnalyticsPluginDelegate() {} 

SampleAdobeAnalyticsPluginDelegate.prototype.onError = function(errorInfo) { 
    console.log("AdobeAnalyticsPlugin error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### HeartbeatDelegate (1.x) {#hb-delegate-1.x}

```js
$.extend(SampleHeartbeatDelegate.prototype, HeartbeatDelegate.prototype);

function SampleHeartbeatDelegate() {} 

SampleHeartbeatDelegate.prototype.onError = function(errorInfo) { 
    console.log("Heartbeat error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### MediaHeartbeatDelegate (2.x) {#mh-delegate-2.x}

```js
ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, MediaHeartbeatDelegate.prototype);

function SampleMediaHeartbeatDelegate(player) { 
    this._player = player;
} 

SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() { 
    return this._player.getCurrentPlaybackTime();
};

SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() { 
    return this._player.getQoSInfo();
};

this._mediaHeartbeat = new MediaHeartbeat(new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

## Comparaison de code VHL : LECTURE PRINCIPALE

### Démarrage de la session

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.trackVideoLoad()` | `MediaHeartbeat.createMediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |

#### Démarrage de la session (1.x) {#session-start-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    this._playerPlugin.trackVideoLoad();
};

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Démarrage de la session (2.x) {#session-start-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

### Métadonnées vidéo standard

| API 1.x | API 2.x |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Métadonnées standard (1.x) {#std-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');

    var contextData = {};

    // Setting Standard Video Metadata 
    contextData[VideoMetadataKeys.SEASON] = "sample season";
    contextData[VideoMetadataKeys.SHOW] = "sample show";
    contextData[VideoMetadataKeys.EPISODE] = "sample episode";
    contextData[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    contextData[VideoMetadataKeys.GENRE] = "sample genre";
    contextData[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc. 
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Métadonnées standard (2.x) {#std-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);

    // Set standard Video Metadata 
    var standardVideoMetadata = {};
    standardVideoMetadata[VideoMetadataKeys.SEASON] = "sample season";
    standardVideoMetadata[VideoMetadataKeys.SHOW] = "sample show";
    standardVideoMetadata[VideoMetadataKeys.EPISODE] = "sample episode";
    standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    standardVideoMetadata[VideoMetadataKeys.GENRE] = "sample genre";
    standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";
    
    // Etc. 
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Au lieu de définir les métadonnées vidéo standard via l’API `AdobeAnalyticsPlugin.setVideoMetadata()`, dans VHL 2.0, les métadonnées vidéo standard sont définies via la clé MediaObject `MediaObject.MediaObjectKey.StandardVideoMetadata()`.

### Métadonnées vidéo personnalisées

| API 1.x | API 2.x |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Métadonnées personnalisées (1.x) {#custom-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Métadonnées personnalisées (2.x) {#custom-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Au lieu de définir les métadonnées vidéo standard via l’API `AdobeAnalyticsPlugin.setVideoMetadata()`, dans VHL 2.0, les métadonnées vidéo standard sont définies via l’API `MediaHeartbeat.trackSessionStart()`.


### Lecture

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackPlay()` | `MediaHeartbeat.trackPlay()` |

#### Lecture (1.x) {#playback-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._playerPlugin.trackSeekStart();
};
```

#### Lecture (2.x) {#playback-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};
```

### Pause

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackPause()` | `MediaHeartbeat.trackPausel()` |

#### Pause (1.x) {#pause-1.x}

```js
VideoAnalyticsProvider.prototype._onPause = function() { 
    console.log('Player event:X PAUSE');
    this._playerPlugin.trackPause();
};
```

#### Pause (2.x) {#pause-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Fin de la recherche

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackSeekComplete()` | `MediaHeartbeat.`<br/>  `trackEvent(MediaHeartbeat.Event.SeekComplete)` |

#### Recherche (1.x) {#seek-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._playerPlugin.trackSeekComplete();
};
```

#### Recherche (2.x) {#seek-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};
```

### Début de la mémoire tampon

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBufferStart()` | `MediaHeartbeat.trackEvent(`<br/>  `MediaHeartbeat.Event.BufferStart)` |

#### Début de la mémoire tampon (1.x) {#buffer-start-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._playerPlugin.trackBufferStart();
};
```

#### Début de la mémoire tampon (2.x) {#buffer-start-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};
```

### Fin de la mémoire tampon

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBufferComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BufferComplete)` |

#### Fin de la mémoire tampon (1.x) {#buffer-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._playerPlugin.trackBufferComplete();
};
```

#### Fin de la mémoire tampon (2.x) {#buffer-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Fin de la lecture

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackComplete()` | `MediaHeartbeat.trackComplete()` |

#### Lecture terminée (1.x) {#playback-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._playerPlugin.trackComplete(function() { 
        console.log( "The completion of the content has been tracked.");
    });
};
```

#### Lecture terminée (2.x) {#playback-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._mediaHeartbeat.trackComplete();
};
```

## Comparaison de code VHL : LECTURE DE LA PUBLICITÉ

### Démarrage de publicité

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdStart()` | `MediaHeartbeat.createAdBreakObject()` |
| `VideoPlayerPluginDelegate.getAdBreakInfo()` | `MediaHeartbeat.createAdObject()` |
| `VideoPlayerPluginDelegate.getAdInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakStart)` |
|  | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdStart)` |

#### Démarrage de la publicité (1.x) {#ad-start-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    this._playerPlugin.trackAdStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo(); 
};
```

#### Démarrage de la publicité (2.x) {#ad-start-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = {};

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

### Métadonnées de publicité standard

| API 1.x | API 2.x |
| --- | --- |
| `AdMetadataKeys()` | `MediaHeartbeat.createAdObject()` |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.trackAdStart()` |

#### Métadonnées de publicité standard (1.x) {#ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Métadonnées de publicité standard (2.x) {#ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);

    // Set standard Ad Metadata 
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Au lieu de définir les métadonnées de publicité standard via l’API `AdobeAnalyticsPlugin.setVideoMetadata()`, dans VHL 2.0, les métadonnées de publicité standard sont définies via la `AdMetadata` clé `MediaObject.MediaObjectKey.StandardVideoMetadata`

### Métadonnées de publicité personnalisées

| API 1.x | API 2.x |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
|  | `MediaHeartbeat.trackAdStart()` |

#### Métadonnées de publicité personnalisées (1.x) {#custom-ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var contextData = {};

    // Setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Métadonnées de publicité personnalisées (2.x) {#custom-ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { 
        affiliate: "Sample affiliate", 
        campaign: "Sample ad campaign" 
    };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Au lieu de définir les métadonnées de publicité personnalisées via l’API `AdobeAnalyticsPlugin.setVideoMetadata`, dans VHL 2.0, les métadonnées de publicité standard sont définies via l’API `MediaHeartbeat.trackAdStart()`.

### Ignorer la publicité

| API 1.x | API 2.x |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
|  | `MediaHeartbeat.trackAdStart()` |

#### Saut de publicité (1.x) {#ad-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};
```

#### Saut de publicité (2.x) {#ad-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onAdSkip = function() { 
    console.log('Player event: AD_SKIP');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};
```

>[!NOTE]
>Dans les API VHL 1.5.X ; `getAdinfo()` et `getAdBreakInfo()` doivent retourner null si le lecteur se trouve en dehors des limites de coupure publicitaire.

### Publicité terminée

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdComplete)` |
|  | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakComplete)` |

#### Fin de la publicité (1.x) {#ad-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._playerPlugin.trackAdComplete();
};
```

#### Fin de la publicité (2.x) {#ad-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

## Comparaison de code VHL : LECTURE DE CHAPITRE

### Début du chapitre

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.createChapterObject` |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Début du chapitre (1.x) {#chap-start-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._playerPlugin.trackChapterStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

#### Début du chapitre (2.x) {#chap-start-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Ignorer le chapitre

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterSkip)` |

#### Saut de chapitre (1.x) {#chap-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

>[!NOTE]
>Dans les API VHL 1.5.X ; `getChapterinfo()` doit retourner null si le lecteur se trouve en dehors des limites de chapitre.

#### Saut de chapitre (2.x) {#chap-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterSkip = function() { 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

### Métadonnées personnalisées du chapitre

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.createChapterObject()` |
| `AdobeAnalyticsPlugin.setChapterMetadata()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Métadonnées personnalisées du chapitre (1.x) {#chap-cust-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._aaPlugin.setChapterMetadata({ 
        segmentType: "Sample segment type" 
    });
    this._playerPlugin.trackChapterStart();
};
```

#### Métadonnées personnalisées du chapitre (2.x) {#chap-cust-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { 
        segmentType: "Sample segment type" 
    };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Chapitre terminé

| API 1.x | API 2.x |
| --- | --- |
| `trackChapterComplete()` | `trackEvent(MediaHeartbeat.Event.ChapterComplete)` |

#### Fin du chapitre (1.x) {#chap-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._playerPlugin.trackChapterComplete();
};
```

#### Fin du chapitre (2.x) {#chap-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};
```

## Comparaison de code VHL : AUTRES ÉVÉNEMENTS

### Changement de débit binaire

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBitrateChange()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BitrateChange)` |

#### Changement de débit binaire (1.x) {#bitrate-chg-1.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosInfo to return the updated bitrate 
    this._playerPlugin.trackBitrateChange();
};
```

#### Changement de débit binaire (2.x) {#bitrate-chg-2.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosObject to return the updated bitrate 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange);
};
```

### Reprise de la vidéo

| API 1.x | API 2.x |
| --- | --- |
| `VideoInfo.resumed()` | `MediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |
| `VideoPlayerPlugin.trackVideoLoad()` |  |

#### Reprise de la vidéo (1.x) {#video-resume-1.x}

```js
this._videoInfo.resumed=true;
```

```js
VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Reprise de la vidéo (2.x) {#video-resume-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.playerName, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

Pour plus d’informations sur le suivi vidéo avec 2.x, voir [Suivi de la lecture vidéo principale.](/help/sdk-implement/track-av-playback/track-core-overview.md)
