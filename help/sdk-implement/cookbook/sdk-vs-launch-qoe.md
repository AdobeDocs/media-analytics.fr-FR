---
seo-title: Comprendre les différences entre le lancement et le SDK multimédia
title: Comprendre les différences entre le lancement et le SDK multimédia
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Comprendre les différences entre le lancement et le SDK multimédia

## Différences de fonctionnalités

* *Lancement* - Lancement fournit une interface utilisateur qui vous guide tout au long de la configuration, de la configuration et du déploiement de vos solutions de suivi des médias en ligne. Le lancement améliore la gestion dynamique des balises.
* *SDK* multimédia - Le SDK multimédia fournit des bibliothèques de suivi des médias conçues pour des plateformes spécifiques (par exemple : Android, iOS, etc.). Adobe recommande Media SDK pour le suivi de l’utilisation des médias dans vos applications mobiles.

## Différences de création de suivi

### Launch

Launch propose deux méthodes pour créer l’infrastructure de suivi. Les deux approches utilisent Media Analytics Launch Extension :

1. Utilisez les API de suivi des médias d’une page Web.

   Dans ce scénario, l’extension Media Analytics exporte les API de suivi des médias vers une variable configurée dans l’objet de fenêtre globale :

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilisez les API de suivi des médias d’une autre extension de lancement.

   Dans ce scénario, vous utilisez les API de suivi des médias exposées par les modules `get-instance` et `media-heartbeat` partagés.

   >[!NOTE]
   >
   >Les modules partagés ne sont pas disponibles pour une utilisation dans des pages Web. Vous pouvez uniquement utiliser des modules partagés à partir d’une autre extension.

   Créez une `MediaHeartbeat` instance à l’aide du module `get-instance` partagé.
Transmettez un objet délégué à `get-instance` qui expose `getQoSObject()` et `getCurrentPlaybackTime()` des fonctions.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accédez aux `MediaHeartbeat` constantes via le module `media-heartbeat` partagé.

### SDK Media

1. Ajoutez la bibliothèque Media Analytics à votre projet de développement.
1. Créez un objet de configuration (`MediaHeartbeatConfig`).
1. Mettez en oeuvre le protocole délégué, exposant les fonctions `getQoSObject()` et `getCurrentPlaybackTime()` les fonctions.
1. Créez une instance Media Heartbeat (`MediaHeartbeat`).

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

* [Configuration de JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

