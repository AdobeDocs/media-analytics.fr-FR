---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées standard sur JavaScript
title: Mise en œuvre de métadonnées standard sur JavaScript
uuid: 523 d 29 e 3-0 a 62-40 d 7-ac 74-da 645024 cdcb
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Mise en œuvre de métadonnées standard sur JavaScript{#implement-standard-metadata-on-javascript}

## Constante de métadonnées

| Nom de constante | Description   |
| --- | --- |
| `StandardMediaMetadata` | Constante permettant d’associer des métadonnées standard à `MediaObject` |

## Mise en œuvre

Instanciez un objet de métadonnées standard, renseignez les variables désirées et définissez l’objet de métadonnées sur l’objet Media Heartbeat. Par exemple :

```js
_onVideoLoad = function () { 
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>, 
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>); 
 
    //Set standard Video Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
 
    //Set standard Audio Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label"; 
 
    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata); 
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
}; 
```

