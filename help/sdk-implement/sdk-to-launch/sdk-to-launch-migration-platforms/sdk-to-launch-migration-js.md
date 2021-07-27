---
title: '« Migration du SDK Media autonome vers Adobe Launch : Web (JS) »'
description: Découvrez comment migrer du SDK Media vers Launch pour JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '403'
ht-degree: 100%

---

# Migration du SDK Media autonome vers Adobe Launch : Web (JS)

## Différences de fonctionnalités

* *Launch* : Launch offre une interface utilisateur qui vous guide tout au long de l’installation, de la configuration et du déploiement de vos solutions de suivi multimédia en ligne. Launch est une version améliorée de Dynamic Tag Management (DTM).
* *SDK Media* : le SDK Media propose des bibliothèques de suivi multimédia conçues pour des plateformes spécifiques (comme Android, iOS, etc.). Adobe recommande le SDK Media pour le suivi de l’utilisation des médias dans vos applications mobiles.

## Configuration

### SDK Media autonome

Dans le SDK Media autonome, vous configurez le suivi dans l’application avant de le transmettre
au SDK lorsque vous créez le dispositif de suivi.

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

En plus de la configuration `MediaHeartbeat`, la page doit configurer et transmettre
l’instance `AppMeasurement` et l’instance pour le suivi multimédia `VisitorAPI` afin 
de fonctionner correctement.

### Extension de Launch

1. Dans Experience Platform Launch, cliquez sur l’onglet [!UICONTROL Extensions] pour votre 
propriété Web.
1. Dans l’onglet [!UICONTROL Catalogue], recherchez l’extension Adobe Media Analytics for Audio and
Video, puis cliquez sur [!UICONTROL Installer].
1. Dans la page des paramètres d’extension, configurez les paramètres de suivi.
L’extension Media utilisera les paramètres configurés pour le suivi.

   ![](assets/launch_config_js.png)

[Guide de l’utilisateur de Launch : installation et configuration de l’extension média](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html?lang=fr#install-and-configure-the-ma-extension)

## Différences dans la création du dispositif de suivi

### SDK Media

1. Ajoutez la bibliothèque Media Analytics à votre projet de développement.
1. Créez un objet de configuration (`MediaHeartbeatConfig`).
1. Implémentez le protocole délégué exposant les fonctions `getQoSObject()` et `getCurrentPlaybackTime()`.
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

<!--  Dead Link - from 2019 - can't locate where this should go
[Media SDK - Tracker Creation](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Launch

Launch propose deux méthodes pour créer l’infrastructure de suivi. Les deux méthodes utilisent l’extension Media Analytics pour Launch :

1. Utilisez les API de suivi multimédia d’une page Web.

   Dans cette configuration, l’extension Media Analytics exporte les API de suivi multimédia vers une variable configurée dans l’objet « window » global :

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilisez les API de suivi multimédia d’une autre extension de Launch.

   Dans cette configuration, vous utilisez les API de suivi multimédia exposées par les modules partagés `get-instance` et `media-heartbeat`.

   >[!NOTE]
   >
   >Les modules partagés ne peuvent pas être utilisés dans des pages Web. Vous pouvez uniquement utiliser des modules partagés à partir d’une autre extension.

   Créez une instance `MediaHeartbeat` à l’aide du module partagé `get-instance`.
Transmettez un objet délégué à `get-instance` qui expose les fonctions `getQoSObject()` et `getCurrentPlaybackTime()`.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accédez aux constantes `MediaHeartbeat` via le module partagé `media-heartbeat`.

## Documentation connexe

### SDK Media

* [Configuration de JavaScript 2.x](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [Configuration de JavaScript 3.x](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [API JS pour SDK Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Présentation de Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html?lang=fr)
* [Extension Media Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html?lang=fr)
