---
seo-title: Configuration de JavaScript
title: Configuration de JavaScript
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Configuration de JavaScript{#set-up-javascript}

## Conditions préalables

* **Obtention de paramètres** de configuration valides Ces paramètres peuvent être obtenus auprès d’un représentant Adobe après avoir configuré votre compte Analytics.
* **Mise en oeuvre`AppMeasurement`de JavaScript dans votre application** multimédia Pour plus d’informations sur la documentation du SDK mobile Adobe, voir [Mise en oeuvre d’Analytics à l’aide de JavaScript.](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **Fournissez les fonctionnalités suivantes dans votre lecteur multimédia :**

   * *Une API pour vous abonner aux événements de lecteur* : Le kit SDK Media vous oblige à appeler une série d’API simples lorsque des événements ont lieu dans votre lecteur.
   * *Une API fournissant des informations sur le lecteur* : Ces informations comprennent des détails tels que le nom du média et la position du curseur de lecture.

1. Ajoutez la bibliothèque que vous avez [téléchargée](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) à votre projet. Créez des références locales aux classes pour des raisons pratiques.

   1. Développez le `MediaSDK-js-v2.*.zip` fichier que vous avez téléchargé.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      Ce fichier JavaScript principal doit être hébergé sur un serveur Web accessible par toutes les pages de votre site. Vous aurez besoin du chemin d’accès à ces fichiers à l’étape suivante.

   1. Référencez `MediaSDK.min.js` sur toutes les pages du site.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. Par exemple :

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Pour vérifier rapidement que la bibliothèque a bien été importée, instanciez la classe `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. Pour faciliter l’accès aux API, créez des références locales aux classes `MediaHeartbeat`. 

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

   Cette section vous aide à comprendre les paramètres de configuration `MediaHeartbeat` et à comprendre comment définir les bonnes valeurs de configuration sur votre instance `MediaHeartbeat` pour un suivi précis.

   Voici un exemple d’ `MediaHeartbeatConfig` initialisation :

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. Implement the `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. Cette instance sera utilisée pour tous les événements de suivi suivants.

   >[!TIP]
   >
   >`MediaHeartbeat` nécessite une instance de `AppMeasurement` pour envoyer des appels à Adobe Analytics. Voici un exemple d’une instance `AppMeasurement` :

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## Migration de la version 1.x vers 2.x dans JavaScript

Dans la version 2.x, toutes les méthodes publiques sont consolidées dans la classe `ADB.va.MediaHeartbeat` pour faciliter le travail des développeurs. De plus, toutes les configurations sont désormais consolidées dans la classe `ADB.va.MediaHeartbeatConfig`. 

Pour plus d’informations sur la migration de 1.x vers 2.x, voir [Migration de VHL 1.x vers 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
