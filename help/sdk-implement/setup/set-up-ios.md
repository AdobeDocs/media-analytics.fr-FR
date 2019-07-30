---
seo-title: Configuration d’iOS
title: Configuration d’iOS
uuid: a 1 c 6 be 79-a 6 dc -47 b 6-93 b 3-ac 7 b 42 f 1 f 3 eb
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Configuration d’iOS{#set-up-ios}

## Conditions préalables

* **Obtention des paramètres de configuration valides pour le kit Media SDK**
Ces paramètres peuvent être obtenus auprès d'un représentant Adobe après avoir configuré votre compte Analytics.
* **Mise en œuvre d'adbmobile pour ios dans votre application**
Pour plus d'informations sur la documentation du SDK mobile Adobe, reportez-vous à [la section SDK 4. x ios pour les solutions Experience Cloud.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >A compter d'ios 9, Apple a introduit une fonctionnalité appelée App Transport Security (ATS). Cette fonction vise à améliorer la sécurité du réseau en s’assurant que vos applications utilisent uniquement des protocoles et des codes aux normes industrielles. Cette fonction est activée par défaut, mais des options de configuration vous permettent d’effectuer des choix quant à l’utilisation d’ATS. For details on ATS, see [App Transport Security.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **Fournissez les fonctionnalités suivantes dans votre lecteur multimédia :**

   * _Une API pour vous abonner aux événements de lecteur_ : Le kit SDK Media vous oblige à appeler une série d’API simples lorsque des événements ont lieu dans votre lecteur.
   * _Une API fournissant des informations sur le lecteur_ : Ces informations comprennent des détails tels que le nom du média et la position du curseur de lecture.

## Implémentation du SDK

1. Ajoutez le SDK Media que vous avez [téléchargé](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) à votre projet.

   1. Vérifiez que le répertoire `libs` contient les composants logiciels suivants :

      * `ADBMediaHeartbeat.h` : fichier d’en-tête Objective-C utilisé pour les API de suivi de la pulsation iOS.
      * `ADBMediaHeartbeatConfig.h` : fichier d’en-tête Objective-C utilisé pour la configuration du kit SDK.
      * `MediaSDK.a` : binaire gras en bytecode contenant les versions de bibliothèque pour les appareils (armv7, armv7s et arm64) et les simulateurs (i386 et x86_64) iOS.

         Ce binaire doit être lié lorsque la cible est destinée à une application iOS.

      * `MediaSDK_TV.a` : binaire gras en bytecode contenant les versions de bibliothèque pour les nouveaux appareils (arm64) et le nouveau simulateur (x86_64) Apple TV.

         Ce binaire doit être lié lorsque la cible est destinée à une application Apple TV (tvOS).
   1. Ajoutez la bibliothèque à votre projet :

      1. Lancez Xcode IDE et ouvrez votre application.
      1. Dans **[!UICONTROL Project Navigator]** (Navigateur de projets), faites glisser le répertoire `libs` sous votre projet.

      1. Assurez-vous que la case **[!UICONTROL Copy Items if Needed]** (Copier les éléments si nécessaire) est cochée, que **[!UICONTROL Create Groups](Créer des groupes) est sélectionné et qu’aucune des cases dans** Add to Target] (Ajouter à la cible) n’est cochée.**[!UICONTROL **

         ![](assets/choose-options_ios.png)

      1. Cliquez sur **[!UICONTROL Terminer]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. Liez les structures et bibliothèques requises dans la section **[!UICONTROL Structures liées]** et **[!UICONTROL Bibliothèques]** dans l’onglet **[!UICONTROL Général]**.

         **Cibles d’une application iOS :**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Cibles d’une application Apple TV (tvOS) :**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. Vérifiez qu’aucune erreur n’est générée lors de la création de votre application.




1. Importez la bibliothèque.

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a `ADBMediaHeartbeatConfig` instance.

   Cette section vous aide à comprendre les paramètres de configuration `MediaHeartbeat` et à définir les bonnes valeurs de configuration sur votre instance `MediaHeartbeat` pour un suivi précis.

   Voici un exemple d’ `ADBMediaHeartbeatConfig` initialisation :

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. Cette instance sera utilisée pour tous les événements de suivi suivants.

## Migration de la version 1.x vers 2.x sur iOS {#migrate-to-two-x}

Dans la version 2.x, toutes les méthodes publiques sont consolidées dans la classe `ADBMediaHeartbeat` pour faciliter le travail des développeurs. Toutes les configurations ont été consolidées dans la classe `ADBMediaHeartbeatConfig`.

Pour en savoir plus sur la migration de la version 1.x vers 2.x, consultez la rubrique [Migration de VHL 1.x vers 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## Configuration d’une application native pour tvOS

Avec la sortie de la nouvelle Apple TV, vous pouvez désormais créer des applications s’exécutant dans l’environnement natif de tvOS. Vous pouvez soit créer une application complètement native, à l’aide des différentes structures disponibles dans iOS, soit créer votre application à l’aide de modèles XML et de JavaScript. La version 2.0 du SDK Media prend désormais en charge tvOS. Pour en savoir plus sur tvOS, consultez le [site du développeur tvOS.](https://developer.apple.com/tvos/documentation/)

Procédez comme suit dans votre projet Xcode. Ce guide suppose que votre projet concerne une application Apple TV ciblant tvOS :

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. Dans l’onglet **[!UICONTROL Créer des phases]** de la cible de votre application tvOS, développez la section **[!UICONTROL Lier le fichier binaire avec les bibliothèques]** et ajoutez les bibliothèques suivantes :

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

