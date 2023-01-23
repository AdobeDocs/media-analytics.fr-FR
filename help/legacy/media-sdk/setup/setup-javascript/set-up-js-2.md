---
title: Comment configurer le SDK Media à lʼaide de JavaScript 2.x
description: Suivez les étapes suivantes pour configurer lʼapplication du SDK Media sur JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '399'
ht-degree: 100%

---

# Configuration de JavaScript 2.x{#set-up-javascript}

## Conditions préalables

* **Obtention de paramètres de configuration valides** Vous pouvez vous procurer ces paramètres auprès d’un représentant Adobe après avoir configuré votre compte Analytics.
* **Mise en œuvre `AppMeasurement` pour JavaScript dans votre application multimédia** Pour plus d’informations sur la documentation du SDK Adobe Mobile, reportez-vous à la rubrique [Mise en œuvre d’Analytics à l’aide de JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=fr)

* **Fournissez les informations suivantes à votre lecteur multimédia :**

   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.
   * *Une API qui fournit des informations au lecteur* - Ces informations incluent des éléments tels que le nom du média et la position de la tête de lecture.

1. Ajoutez la bibliothèque que vous avez [téléchargée](/help/getting-started/download-sdks.md) à votre projet. Créez des références locales aux classes pour des raisons pratiques.

   1. Développez le fichier `MediaSDK-js-v2.*.zip` que vous avez téléchargé.
   1. Vérifiez que le répertoire `MediaSDK.min.js` contient le fichier `libs` :

   1. Hébergez le fichier `MediaSDK.min.js`.

      Ce fichier JavaScript principal doit être hébergé sur un serveur web accessible par toutes les pages de votre site. Vous avez besoin du chemin d’accès à ces fichiers pour l’étape suivante.

   1. Référencez `MediaSDK.min.js` sur toutes les pages du site.

      Insérez `MediaSDK` pour JavaScript en ajoutant la ligne de code suivante dans la balise `<head>` ou `<body>` de chaque page. Par exemple :

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Pour vérifier rapidement que la bibliothèque a bien été importée, instanciez la classe `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >À partir de la version 2.1.0, le kit SDK JavaScript est conforme aux spécifications du module AMD et CommonJS, et `VideoHeartbeat.min.js` peut également être utilisé avec les chargeurs de module compatibles.

1. Pour faciliter l’accès aux API, créez des références locales aux classes `MediaHeartbeat`.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Créez une instance `MediaHeartbeatConfig`.

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

1. Mettez en œuvre le protocole `MediaHeartbeatDelegate`.

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

1. Créez l’instance `MediaHeartbeat`.

   Utilisez les instances `MediaHeartbeatConfig` et `MediaHeartbeatDelegate` pour créer l’instance `MediaHeartbeat`.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Assurez-vous que votre instance `MediaHeartbeat` est accessible et reste attribuée jusqu’à la fin de la session multimédia. Cette instance sera utilisée pour tous les événements de suivi suivants.

   >[!TIP]
   >
   >`MediaHeartbeat` requiert une instance de `AppMeasurement` pour envoyer des appels à Adobe Analytics. Voici un exemple d’une instance `AppMeasurement` :

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migration de JavaScript 1.x vers 2.x

Dans la version 2.x, toutes les méthodes publiques sont consolidées dans la classe `ADB.va.MediaHeartbeat` pour faciliter le travail des développeurs. De plus, toutes les configurations sont désormais consolidées dans la classe `ADB.va.MediaHeartbeatConfig`.

Pour plus d’informations sur la migration de la version 1.x vers la version 2.x, consultez la documentation sur l’implémentation héritée.
