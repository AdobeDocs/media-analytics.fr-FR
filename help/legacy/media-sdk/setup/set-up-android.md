---
title: Comment configurer le SDK Media sur Android
description: Pour configurer l’application du SDK Media sur Android, procédez comme suit.
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 97%

---

# Configuration d’Android{#set-up-android}

Découvrez comment configurer des services de streaming multimédia pour les appareils Android.

>[!IMPORTANT]
>
>Avec l’abandon de la prise en charge des SDK mobiles de version 4 programmée au 31 août 2021, Adobe cessera également de prendre en charge le SDK Media Analytics pour iOS et Android.  Pour plus d’informations, reportez-vous à la [FAQ sur l’abandon de la prise en charge du SDK Media Analytics](/help/additional-resources/end-of-support-faqs.md).


## Conditions préalables

* **Obtention de paramètres de configuration valides pour le SDK Media** Vous pouvez vous procurer ces paramètres auprès d’un représentant Adobe après avoir configuré votre compte Analytics.
* **Mise en œuvre d’ADBMobile pour Android dans votre application** Pour plus d’informations sur la documentation du kit SDK Adobe Mobile, reportezvous à la rubrique [Kit SDK Android 4.x pour les solutions Experience Cloud.](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=fr)

* **Fournissez les informations suivantes à votre lecteur multimédia :**
   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.
   * *Une API qui fournit des informations au lecteur* - Ces informations incluent des éléments tels que le nom du média et la position de la tête de lecture.

## Implémentation du SDK

1. Ajoutez le SDK Media que vous avez téléchargé à votre projet.

   1. Décompressez le fichier .zip Android (par exemple, `MediaSDK-android-v2.*.zip`).
   1. Vérifiez que le répertoire `libs/` contient le fichier `MediaSDK.jar`.

   1. Ajoutez la bibliothèque à votre projet.

      **IntelliJ IDEA :**

      1. Cliquez avec le bouton droit sur votre projet dans le panneau **[!UICONTROL Navigation dans le projet]**.
      1. Sélectionnez **[!UICONTROL Ouvrir les paramètres du module]**.
      1. Sous **[!UICONTROL Paramètres du projet]**, sélectionnez **[!UICONTROL Bibliothèques]**.

      1. Cliquez sur **[!UICONTROL +]** pour ajouter une nouvelle bibliothèque.
      1. Sélectionnez **[!UICONTROL Java]** et accédez au fichier `MediaSDK.jar`.

      1. Sélectionnez les modules dans lesquels vous prévoyez d’utiliser la bibliothèque mobile.
      1. Cliquez sur **[!UICONTROL Appliquer]** puis sur **[!UICONTROL OK]** pour fermer la fenêtre Paramètres du module.

      **Eclipse :**

      1. Dans Eclipse IDE, cliquez avec le bouton droit sur le nom du projet.
      1. Cliquez sur **[!UICONTROL Créer un chemin]** > **[!UICONTROL Ajouter des archives externes]**.
      1. Sélectionnez `MediaSDK.jar`.
      1. Cliquez sur **[!UICONTROL Ouvrir]**.
      1. Cliquez de nouveau avec le bouton droit sur le projet, puis sélectionnez **[!UICONTROL Créer un chemin]** > **[!UICONTROL Configurer la création d’un chemin]**.
      1. Cliquez sur les onglets **[!UICONTROL Commande]** et **[!UICONTROL Exporter]**.

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

Pour plus d’informations sur la migration de la version 1.x vers la version 2.x, consultez la documentation sur l’implémentation héritée.
