---
seo-title: Configuration d’Android
title: Configuration d’Android
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Configuration d’Android{#set-up-android}

## Conditions préalables

* **Obtention de paramètres de configuration valides pour le SDK** Media Ces paramètres peuvent être obtenus auprès d’un représentant Adobe après avoir configuré votre compte Analytics.
* **Mise en oeuvre d’ADBMobile pour Android dans votre application** Pour plus d’informations sur la documentation du SDK mobile Adobe, voir SDK [Android 4.x pour les solutions Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **Fournissez les fonctionnalités suivantes dans votre lecteur multimédia :**
   * *Une API pour vous abonner aux événements de lecteur* : Le kit SDK Media vous oblige à appeler une série d’API simples lorsque des événements ont lieu dans votre lecteur.
   * *Une API fournissant des informations sur le lecteur* : Ces informations comprennent des détails tels que le nom du média et la position du curseur de lecture.

## Implémentation du SDK

1. Ajoutez le SDK Media que vous avez [téléchargé](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) à votre projet.

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. Ajoutez la bibliothèque à votre projet.

      **IntelliJ IDEA :**

      1. Cliquez avec le bouton droit sur votre projet dans le panneau **[!UICONTROL Navigation dans le projet]**.
      1. Sélectionnez **[!UICONTROL Ouvrir les paramètres du module]**.
      1. Sous **[!UICONTROL Paramètres du projet]**, sélectionnez **[!UICONTROL Bibliothèques]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. Sélectionnez **[!UICONTROL Java]** et accédez au fichier `MediaSDK.jar`.

      1. Sélectionnez les modules dans lesquels vous prévoyez d’utiliser la bibliothèque mobile.
      1. Cliquez sur **[!UICONTROL Appliquer]** puis sur **[!UICONTROL OK]** pour fermer la fenêtre Paramètres du module.
      **Eclipse :**

      1. Dans Eclipse IDE, cliquez avec le bouton droit sur le nom du projet.
      1. Click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. Select `MediaSDK.jar`.
      1. Cliquez sur **[!UICONTROL Ouvrir]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. Cliquez sur les onglets **[!UICONTROL Commande]** et **[!UICONTROL Exporter]**.

      1. Assurez-vous que le fichier `MediaSDK.jar` est bien sélectionné.


1. Importez la bibliothèque.

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

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

1. Implement the `MediaHeartbeatDelegate` interface.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Cette instance sera utilisée pour tous les événements de suivi suivants.

**Ajout des autorisations d’application**

Votre application utilisant le SDK Media requiert les autorisations suivantes pour envoyer des données dans des appels de suivi :

* `INTERNET`
* `ACCESS_NETWORK_STATE`

Pour ajouter ces autorisations, ajoutez les lignes suivantes à votre fichier `AndroidManifest.xml`, situé dans le répertoire du projet d’application :

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**Migration de la version 1.x vers 2.x sur Android**

Dans les versions 2.x, toutes les méthodes publiques sont consolidées dans la classe `com.adobe.primetime.va.simple.MediaHeartbeat` pour faciliter le travail des développeurs. De plus, toutes les configurations sont désormais consolidées dans la classe `com.adobe.primetime.va.simple.MediaHeartbeatConfig`. 

For detailed information about migrating from 1.x to 2.x, see [mig-1x-2x-overview.md.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
