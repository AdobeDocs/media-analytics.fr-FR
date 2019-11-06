---
seo-title: Migration du SDK multimédia autonome vers Adobe Launch - Android
title: Migration du SDK multimédia autonome vers Adobe Launch - Android
seo-description: Instructions et exemples de code pour faciliter la migration du SDK multimédia vers le lancement pour Android.
description: Instructions et exemples de code pour faciliter la migration du SDK multimédia vers le lancement pour Android.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# Migration du SDK multimédia autonome vers Adobe Launch - Android

## Configuration

### Extension de lancement

1. Dans le lancement de la plateforme d’expérience, cliquez sur l’onglet [!UICONTROL Extensions] pour votre propriété mobile.
1. Dans l’onglet [!UICONTROL Catalogue] , recherchez l’extension Adobe Media Analytics pour l’audience et la vidéo, puis cliquez sur [!UICONTROL Installer].
1. Dans la page des paramètres d’extension, configurez les paramètres de suivi.
L’extension Media utilisera les paramètres configurés pour le suivi.

[Utilisation des extensions mobiles](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

### SDK de média autonome

Dans le SDK multimédia autonome, vous configurez le suivi dans l’application et le transmettez au SDK lorsque vous créez le suivi.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

## Création du suivi

### Extension de lancement

[Référence à l’API Media - Création d’un outil de suivi des médias](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Avant de créer l'outil de suivi, vous devez enregistrer l'extension multimédia et les extensions dépendantes avec le noyau mobile.

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension 
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

Une fois que vous avez enregistré l’extension multimédia, créez le suivi à l’aide de l’API suivante.
Le suivi sélectionne automatiquement la configuration à partir de la propriété de lancement configurée.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

### SDK de média autonome

Dans le SDK multimédia autonome, vous créez manuellement l’ `MediaHeartbeatConfig` objet et configurez les paramètres de suivi. Mettez en oeuvre l’interface déléguée exposant`getQoSObject()` et `getCurrentPlaybackTime()functions.`créez une `MediaHeartbeat` instance pour le suivi.

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override 
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>); 
    } 

    @Override 
    public Double getCurrentPlaybackTime() { 
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>; 
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

## Mise à jour des valeurs Playhead et Quality of Experience.

### Extension de lancement

L’implémentation doit mettre à jour le curseur de lecture actuel du lecteur en appelant la méthode exposée par`updateCurrentPlayhead` l’outil de suivi. Pour un suivi précis, vous devez appeler cette méthode au moins une fois par seconde.

[Référence de l’API Media - Mettre à jour le lecteur actuel](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

L’implémentation doit mettre à jour les informations de QoE en appelant la `updateQoEObject`méthode exposée par l’outil de suivi. Nous nous attendons à ce que cette méthode soit appelée chaque fois qu’il y a un changement dans les mesures de qualité.

[Référence de l’API Media - Mettre à jour l’objet QoE](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

### SDK de média autonome

Dans le SDK multimédia autonome, vous transmettez un objet délégué qui implémente l’interface lors`MediaHeartbeartDelegate` de la création de l’outil de suivi.  L’implémentation doit renvoyer la dernière qualité de qualité de l’expérience et le curseur de lecture chaque fois que l’outil de suivi appelle les`getQoSObject()` méthodes d’interface et les `getCurrentPlaybackTime()` méthodes d’interface.

## Transmission de métadonnées publicitaires/médias standard

### Extension de lancement

* Métadonnées Media standard :

   ```java
   HashMap<String, Object> mediaObject = 
     Media.createMediaObject("media-name", 
                             "media-id", 
                             60D, 
                             MediaConstants.StreamType.VOD, 
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, 
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, 
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Métadonnées de publicité standard:

   ```java
   HashMap<String, Object> adObject = 
     Media.createAdObject("ad-name", 
                          "ad-id", 
                          1L, 
                          15D);
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, 
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, 
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart, 
                       adObject, 
                       adMetadata);
   ```

### SDK de média autonome

* Métadonnées Media standard :

   ```java
   MediaObject mediaInfo = 
     MediaHeartbeat.createMediaObject("media-name", 
                                      "media-id", 
                                      60D, 
                                      MediaHeartbeat.StreamType.VOD, 
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata = 
     new HashMap<String, String>(); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, 
                             "Sample Episode"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, 
                             "Sample Show"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, 
                             "Sample Season"); 
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata, 
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* Métadonnées de publicité standard:

   ```java
   MediaObject adInfo = 
     MediaHeartbeat.createAdObject("ad-name", 
                                   "ad-id", 
                                   1L, 
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata = 
     new HashMap<String, String>(); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, 
                          "Sample Advertiser"); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, 
                          "Sample Campaign"); 
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
                   standardAdMetadata); 
   
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart, 
                      adObject, 
                      adMetadata);
   ```


