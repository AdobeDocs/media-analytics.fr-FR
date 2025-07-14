---
title: Reprise des sessions inactives
description: Découvrez comment effectuer la reprise dʼune session inactive.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 100%

---

# Reprise des sessions inactives{#resuming-inactive-sessions}

## Longues pauses

Le SDK Media surveille automatiquement la durée de la lecture multimédia dans l’un des états inactifs suivants :

* En pause
* Recherche
* Bloqué
* Mise en mémoire tampon

Si une session de suivi multimédia inactive pendant plus de 30 minutes, celle-ci se fermera automatiquement. Si l’utilisateur reprend une session de suivi vidéo précédemment inactive (`trackPlay`), Media Heartbeat crée automatiquement une nouvelle session vidéo à l’aide des informations et des métadonnées précédentes et envoie une reprise d’événement de pulsation. Pour plus d’informations, voir [Paramètres audio et vidéo.](/help/implementation/variables/audio-video-parameters.md)


## Reprise manuelle d’une session précédemment fermée

Le SDK Media procédera uniquement à la reprise automatique des sessions si l’application n’a pas été fermée. Si l’application stocke des données utilisateur et permet de procéder à la reprise d’un média précédemment fermé, il est possible de déclencher manuellement un événement de reprise. Lorsque vous démarrez la session de suivi vidéo, configurez la propriété facultative Video Resumed.

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
