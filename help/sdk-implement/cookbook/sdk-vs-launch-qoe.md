---
seo-title: Comprendre les différences de lancement et de SDK Media
title: Comprendre les différences de lancement et de SDK Media
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Comprendre les différences de lancement et de SDK Media

## Différences de fonctionnalités

* *Lancement* - Launch fournit une interface utilisateur qui vous guide tout au long du paramétrage de votre solution de suivi multimédia. Le lancement s'améliore sur la gestion dynamique des balises (DTM).
* *Media SDK* - Le kit de développement multimédia fournit des bibliothèques de suivi multimédia conçues pour des plateformes spécifiques (par exemple : Android, ios, etc.). Adobe recommande à Media SDK de suivre l'utilisation des médias dans vos applications mobiles.

## Différences de création de suivi

### Launch

Le lancement propose deux approches pour créer l'infrastructure de suivi. Les deux approches utilisent l'extension de lancement Media Analytics :

1. Utilisez les API de suivi multimédia d'une page Web.

   Dans ce scénario, l'extension Media Analytics exporte les API de suivi multimédia vers une variable configurée dans l'objet de fenêtre globale :

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilisez les API de suivi multimédia d'une autre extension de lancement.

   Dans ce scénario, vous utilisez les API de suivi multimédia exposées par les `get-instance` modules partagés et `media-heartbeat` les modules partagés.

   >[!NOTE]
   >
   >Les modules partagés ne sont pas disponibles dans les pages Web. Vous pouvez utiliser uniquement les modules partagés d'une autre extension.

   Créez une `MediaHeartbeat` instance à l'aide du `get-instance` module partagé.
Transmettez un objet délégué à `get-instance` ceci exposant `getQoSObject()` et `getCurrentPlaybackTime()` fonctions.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accédez `MediaHeartbeat` aux constantes via le module `media-heartbeat` partagé.

### SDK Media

1. Ajoutez la bibliothèque Media Analytics à votre projet de développement.
1. Créez un objet config (`MediaHeartbeatConfig`).
1. Mettez en œuvre le protocole délégué, exposant les fonctions `getQoSObject()` et `getCurrentPlaybackTime()` les fonctions.
1. Création d'une instance de Media Heartbeat (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

## Documentation connexe

### Launch

* [Présentation du lancement](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Extension MA](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### SDK Media

* [Configuration du fichier JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

