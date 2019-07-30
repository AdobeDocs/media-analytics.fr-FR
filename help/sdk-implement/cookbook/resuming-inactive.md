---
seo-title: Reprise des sessions inactives
title: Reprise des sessions inactives
uuid: 3 ff 1205 d -7 bbe -4016-9 bd 7-6 e 34 b 7862 c 4 c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Reprise des sessions inactives{#resuming-inactive-sessions}

## Longues pauses

Le kit Media SDK suit automatiquement la durée pendant laquelle la lecture multimédia se trouve dans l'un des états inactifs suivants :

* En pause
* Recherche
* Bloqué
* Mise en mémoire tampon

Si une session de suivi multimédia reste à un état inactif pendant plus de 30 minutes, la session est automatiquement fermée. Si l’utilisateur reprend une session de suivi vidéo précédemment inactive (`trackPlay`), Media Heartbeat crée automatiquement une nouvelle session vidéo à l’aide des informations et des métadonnées précédentes et envoie une reprise d’événement de pulsation. For more information, see [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)

## Reprise manuelle d’une session précédemment fermée

Le kit de développement multimédia ne reprendra que automatiquement les sessions si l'application n'a pas été fermée. Si l'application stocke les données utilisateur et permet de reprendre un média précédemment fermé, il est possible de déclencher manuellement un événement de reprise. Lorsque vous démarrez la session de suivi vidéo, configurez la propriété facultative Video Resumed.

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

