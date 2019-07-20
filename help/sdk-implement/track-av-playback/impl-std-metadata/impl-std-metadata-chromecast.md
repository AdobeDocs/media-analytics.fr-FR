---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées standard sur Chromecast
title: Mise en œuvre de métadonnées standard sur Chromecast
uuid: 1560 d 3 e 0-29 f 5-4678-9 f 01-c 672 e 0 ae 547 b
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Mise en œuvre de métadonnées standard sur Chromecast{#implement-standard-metadata-on-chromecast}

Instanciez un objet de métadonnées standard, renseignez les variables désirées et définissez l’objet de métadonnées sur l’objet Media Heartbeat. Par exemple :

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {}; 
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist"; 
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

See the comprehensive list of audio and video metadata here: [Audio and video parameters.](../../../metrics-and-metadata/audio-video-parameters.md)
