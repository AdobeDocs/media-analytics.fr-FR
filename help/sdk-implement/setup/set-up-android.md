---
title: Configuration d’Android
description: Configuration de l’application Media SDK pour implémentation sur Android.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Configuration d’Android {#set-up-android}

## Conditions préalables

* **Obtention de paramètres de configuration valides pour le SDK Media** Vous pouvez vous procurer ces paramètres auprès d’un représentant Adobe après avoir configuré votre compte Analytics.
* **Mise en œuvre d’ADBMobile pour Android dans votre application** Pour plus d’informations sur la documentation du kit SDK Adobe Mobile, reportezvous à la rubrique [Kit SDK Android 4.x pour les solutions Experience Cloud.](https://docs.adobe.com/content/help/fr-FR/mobile-services/android/overview.html)
* **Fournissez les informations suivantes à votre lecteur multimédia :**
   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.
   * *Une API qui fournit des informations au lecteur* - Ces informations incluent des éléments tels que le nom du média et la position de la tête de lecture.

## Implémentation du SDK

1. Ajoutez le SDK Media que vous avez [téléchargé](/help/sdk-implement/download-sdks.md#download-2x-sdks) à votre projet.

   1. Décompressez le fichier .zip Android (par exemple, `MediaSDK-android-v2.*.zip`).
   1. Vérifiez que le répertoire `libs/` contient le fichier `MediaSDK.jar`.

   1. Ajoutez la bibliothèque à votre projet.

      **IntelliJ IDEA :**

      1. Right click your project in the **[!UICONTROL Project navigation]** panel.
      1. Sélectionnez **[!UICONTROL Open Module Settings]**.
      1. Sous **[!UICONTROL Project Settings]**, sélectionnez **[!UICONTROL Libraries]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Sélectionnez **[!UICONTROL Java]** et accédez au fichier `MediaSDK.jar`.

      1. Sélectionnez les modules dans lesquels vous prévoyez d’utiliser la bibliothèque mobile.
      1. Click **[!UICONTROL Apply]** and then **[!UICONTROL OK]** to close the Module Settings window.
      **Eclipse :**

      1. Dans Eclipse IDE, cliquez avec le bouton droit sur le nom du projet.
      1. Cliquez sur  **[!UICONTROL Build Path]** > **[!UICONTROL Add External Archives]** .
      1. Sélectionnez `MediaSDK.jar`.
      1. Cliquez sur **[!UICONTROL Open]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** > **[!UICONTROL Configure Build Path]** .
      1. Cliquez sur les **[!UICONTROL Order]** onglets et **[!UICONTROL Export]** .

      1. Assurez-vous que le fichier `MediaSDK.jar` est bien sélectionné.


1. Importez la bibliothèque.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Créez l’instance `MediaHeartbeatConfig`.

   Voici un exemple d’ `MediaHeartbeatConfig` initialisation :

   ```java
   // Media Heartbeat Initialization 
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_; 
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName = <SAMPLE_PLAYER_NAME>; 
   config.ssl = <true/false>; 
   config.debugLogging = <true/false>; 
   ```

1. Mettez en œuvre l’interface `MediaHeartbeatDelegate`.

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override 
   public MediaObject getQoSObject() { 
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>); 
   } 
   
   //Replace <currentPlaybackTime> with the video player current playback time 
   @Override 
   public Double getCurrentPlaybackTime() { 
       return <currentPlaybackTime>; 
   }
   ```

1. Créez l’instance `MediaHeartbeat`.

   Utilisez l’instance `MediaHeartbeatConfig` et l’instance `MediaHertbeatDelegate` pour créer l’instance `MediaHeartbeat`.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Assurez-vous que votre instance `MediaHeartbeat` est accessible et *reste attribuée jusqu’à la fin de la session*. Cette instance sera utilisée pour tous les événements de suivi suivants.

**Ajout des autorisations des applications**

Votre application utilisant le SDK Media nécessite les autorisations suivantes pour envoyer des données dans les appels de suivi :

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Pour ajouter ces autorisations, ajoutez les lignes suivantes à votre fichier `AndroidManifest.xml`, situé dans le répertoire du projet d’application :

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migration de la version 1.x vers 2.x sur Android**

Dans les versions 2.x, toutes les méthodes publiques sont consolidées dans la classe `com.adobe.primetime.va.simple.MediaHeartbeat` pour faciliter le travail des développeurs. De plus, toutes les configurations sont désormais consolidées dans la classe `com.adobe.primetime.va.simple.MediaHeartbeatConfig`.

Pour plus d’informations sur la migration de 1.x vers 2.x, voir [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
