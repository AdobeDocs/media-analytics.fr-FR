---
seo-title: Reprise des sessions inactives
title: Reprise des sessions inactives
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Reprise des sessions inactives{#resuming-inactive-sessions}

## Longues pauses

Le SDK multimédia effectue automatiquement le suivi de la durée de lecture du média dans l’un des états inactifs suivants :

* En pause
* Recherche
* Bloqué
* Mise en mémoire tampon

If a media tracking session remains in an inactive state for longer than 30 minutes, the session will automatically be closed. Si l’utilisateur reprend une session de suivi vidéo précédemment inactive (`trackPlay`), Media Heartbeat crée automatiquement une nouvelle session vidéo à l’aide des informations et des métadonnées précédentes et envoie une reprise d’événement de pulsation. Pour plus d’informations, voir Paramètres [audio et vidéo.](/help/metrics-and-metadata/audio-video-parameters.md)

## Reprise manuelle d’une session précédemment fermée

Le SDK multimédia ne reprend automatiquement les sessions que si l’application n’a pas été fermée. Si l’application stocke des données utilisateur et peut reprendre un média précédemment fermé, il est possible de déclencher manuellement un événement de reprise. Lorsque vous démarrez la session de suivi vidéo, configurez la propriété facultative Video Resumed.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true 
public void onmediaLoad(Observable observable, Object data) { 

  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Set to true if this is a resume playback scenario 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);
   
  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification { 
  //Replace <MEDIA_NAME> with the media name. 
  //Replace <MEDIA_ID> with a media unique identifier. 
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                       mediaId:<MEDIA_ID> 
                       length:<MEDIA_LENGTH> 
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 

  //Set to YES if this user is resuming a previously closed media session 
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata]; 
} 
```

### JavaScript

```js
_onmediaLoad = function () { 
  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session 
  mediaObject.setValue(MediaObjectKey.mediaResumed, true); 
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

