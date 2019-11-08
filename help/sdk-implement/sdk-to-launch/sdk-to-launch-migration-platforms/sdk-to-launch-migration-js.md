---
title: Migration du SDK multimédia autonome vers Adobe Launch - Web (JS)
description: Instructions et exemples de code pour faciliter la migration du SDK multimédia vers le lancement.
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# Migration du SDK multimédia autonome vers Adobe Launch - Web (JS)

## Différences de fonctionnalités

* *Lancement* - Lancement fournit une interface utilisateur qui vous guide tout au long de la configuration, de la configuration et du déploiement de vos solutions de suivi des médias en ligne. Le lancement améliore la gestion dynamique des balises.
* *SDK* multimédia - Le SDK multimédia fournit des bibliothèques de suivi des médias conçues pour des plateformes spécifiques (par exemple : Android, iOS, etc.). Adobe recommande Media SDK pour le suivi de l’utilisation des médias dans vos applications mobiles.

## Configuration

### SDK de média autonome

Dans le SDK Media autonome, vous configurez la configuration du suivi dans l’application et le transmettez au SDK lorsque vous créez l’outil de suivi.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Outre la `MediaHeartbeat` configuration, la page doit configurer et transmettre l’ `AppMeasurement` instance et `VisitorAPI` l’instance pour le suivi des médias afin de fonctionner correctement.

### Extension de lancement

1. Dans le lancement de la plateforme d’expérience, cliquez sur l’onglet [!UICONTROL Extensions] pour votre propriété web.
1. Dans l’onglet [!UICONTROL Catalogue] , recherchez l’extension Adobe Media Analytics pour l’audio et la vidéo, puis cliquez sur [!UICONTROL Installer].
1. Dans la page des paramètres d’extension, configurez les paramètres de suivi.
L’extension Media utilisera les paramètres configurés pour le suivi.

   ![](assets/launch_config_js.png)

[Guide de l'utilisateur du lancement - Installation et configuration de l'extension multimédia](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Différences de création de suivi

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

[SDK multimédia - Création d’un outil de suivi](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

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

## Documentation connexe

### SDK Media

* [Configuration de JS](/help/sdk-implement/setup/set-up-js.md)
* [API JS SDK multimédia](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Présentation du lancement](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Extension Media Analytics](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
