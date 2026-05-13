---
title: Migration de Media SDK autonome vers Adobe Launch - Android
description: Découvrez comment migrer du SDK Media vers Launch pour Android.
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/HawnzTGV1nsGCibAtXkl3cAB5NjO2VfUpQODm6-w-qk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 428
ht-degree: 48%

---

# Migration du SDK Media autonome vers Adobe Launch : Android

>[!NOTE]
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.


## Configuration

### SDK Media autonome

Dans le SDK Media autonome, configurez le suivi dans l’application et transmettez-le à .
le SDK lorsque vous créez le dispositif de suivi.

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

### Extension de Launch

1. Dans Experience Platform Launch, cliquez sur l’onglet [!UICONTROL Extensions] de votre
Propriété mobile.
1. Dans l’onglet [!UICONTROL  Catalogue ], recherchez Adobe Media Analytics for Audio
et l’extension vidéo, puis cliquez sur [!UICONTROL Installer].
1. Dans la page des paramètres d’extension, configurez les paramètres de suivi.
L’extension Media utilisera les paramètres configurés pour le suivi.

![](assets/launch_config_mobile.png)

[Utilisation des extensions mobiles](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

## Création du dispositif de suivi

### SDK Media autonome

Dans le SDK Media autonome, vous créez manuellement l’objet `MediaHeartbeatConfig`
et configurez les paramètres de tracking. Implémenter l’interface de délégué exposant
`getQoSObject()` et `getCurrentPlaybackTime()functions.`
Créez une instance `MediaHeartbeat` pour le tracking.

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

### Extension de Launch

[Référence de l’API Media - Création d’un Media Tracker](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createtracker)

Avant de créer le dispositif de suivi, vous devez enregistrer l’extension Media et
extensions dépendantes avec mobile core.

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

Une fois que vous avez enregistré l’extension média, créez le dispositif de suivi à l’aide de l’API suivante.
Le dispositif sélectionne automatiquement la configuration à partir de la propriété configurée dans Launch.

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## Mise à jour des valeurs Playhead (curseur de lecture) et Quality of Experience (qualité de l’expérience).

### SDK Media autonome

Dans le SDK Media autonome, vous transmettez un objet délégué qui implémente
Interface `MediaHeartbeartDelegate` lors de la création du tracker.  La mise en œuvre
doit renvoyer la dernière QoE et le curseur de lecture chaque fois que le dispositif de suivi appelle la variable
`getQoSObject()` et méthodes d’interface `getCurrentPlaybackTime()`.

### Extension de Launch

L’implémentation doit mettre à jour le curseur de lecture actuel en appelant la fonction
`updateCurrentPlayhead` méthode exposée par le tracker. Pour un suivi précis
vous devez appeler cette méthode au moins une fois par seconde.

[Référence de l’API Media - Mise à jour du lecteur actuel](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#updatecurrentplayhead)

L’implémentation doit mettre à jour les informations de QoE en appelant la fonction `updateQoEObject`
méthode exposée par le tracker. Nous prévoyons d’appeler cette méthode dès que possible
est une modification des mesures de qualité.

[Référence de l’API Media - Mettre à jour l’objet QoE](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/#createqoeobject)

## Transmission de métadonnées publicitaires / médias standard

### SDK Media autonome

* Métadonnées médias standard :

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

* Métadonnées de publicité standard :

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

### Extension de Launch

* Métadonnées médias standard :

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

* Métadonnées de publicité standard :

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
