---
title: Migration du SDK multimédia autonome vers Adobe Launch - iOS
description: Instructions et exemples de code pour faciliter la migration du SDK multimédia vers le lancement pour iOS.
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# Migration du SDK multimédia autonome vers Adobe Launch - iOS

## Configuration

### SDK de média autonome

Dans le SDK Media autonome, vous configurez la configuration du suivi dans l’application et le transmettez au SDK lorsque vous créez l’outil de suivi.

```objective-c
ADBMediaHeartbeatConfig *config = 
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker = 
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### Extension de lancement

1. Dans le lancement de la plate-forme d’expérience, cliquez sur l’onglet [!UICONTROL Extensions] pour votre propriété mobile.
1. Dans l’onglet [!UICONTROL Catalogue] , recherchez l’extension Adobe Media Analytics pour l’audio et la vidéo, puis cliquez sur [!UICONTROL Installer].
1. Dans la page des paramètres d’extension, configurez les paramètres de suivi.
L’extension Media utilisera les paramètres configurés pour le suivi.

   ![](assets/launch_config_mobile.png)

[Configuration de l’extension Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## Création du suivi

### SDK de média autonome

Dans le SDK multimédia autonome, vous créez manuellement l’ `ADBMediaHeartbeatConfig` objet et configurez les paramètres de suivi. Mettez en oeuvre l’interface des délégués exposant les`getQoSObject()``getCurrentPlaybackTime()functions.`

Créez une instance MediaHeartbeat pour le suivi :

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker = 
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### Extension de lancement

[Référence de l’API Media - Création du suivi des médias](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

Avant de créer l'outil de suivi, enregistrez l'extension multimédia et les extensions dépendantes avec le noyau mobile.

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

Une fois l’extension multimédia enregistrée, le suivi peut être créé à l’aide de l’API suivante.
Le suivi sélectionne automatiquement la configuration à partir de la propriété de lancement configurée.

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## Mise à jour des valeurs Playhead et Quality of Experience.

### SDK de média autonome

Dans le SDK Media autonome, un objet délégué qui implémente le protocole est transmis lors de la création de l’outil de suivi.`ADBMediaHeartbeartDelegate` 
L’implémentation doit renvoyer la dernière QoE et le curseur de lecture chaque fois que l’outil de suivi appelle les `getQoSObject()` méthodes et les `getCurrentPlaybackTime()` méthodes d’interface.

### Extension de lancement

L’implémentation doit mettre à jour le curseur de lecture du lecteur actuel en appelant la méthode exposée par`updateCurrentPlayhead` l’outil de suivi. Pour un suivi précis, vous devez appeler cette méthode au moins une fois par seconde.

[Référence de l’API Media - Mettre à jour la tête de lecture actuelle](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

L’implémentation doit mettre à jour les informations de QoE en appelant la méthode exposée par`updateQoEObject` l’outil de suivi. Vous devez appeler cette méthode chaque fois qu’il y a un changement dans les mesures de qualité.

[Référence de l’API Media - Mettre à jour l’objet QoE](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## Transmission de métadonnées publicitaires/médias standard

### SDK de média autonome

* Métadonnées Media standard :

   ```objective-c
   ADBMediaObject *mediaObject = 
     [ADBMediaHeartbeat createMediaObjectWithName:@"media-name" 
                        mediaId:@"media-id" 
                        length:60 
                        streamType:ADBMediaHeartbeatStreamTypeVod 
                        mediaType:ADBMediaTypeVideo];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
   [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
   [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   
   [tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Métadonnées de publicité standard:

   ```objective-c
   ADBMediaObject* adObject = 
     [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"] 
                        adId:[adData objectForKey:@"id"]
                        position:[[adData objectForKey:@"position"] doubleValue]
                        length:[[adData objectForKey:@"length"] doubleValue]];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = 
     [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample Advertiser" 
                     forKey:ADBAdMetadataKeyADVERTISER];
   [standardMetadata setObject:@"Sample Campaign" 
                     forKey:ADBAdMetadataKeyCAMPAIGN_ID];
   [adObject setValue:standardMetadata 
                     forKey:ADBMediaObjectKeyStandardAdMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
   [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ADBMediaHeartbeatEventAdStart 
            mediaObject:adObject 
            data:adDictionary];
   ```

### Extension de lancement

* Métadonnées Media standard :

   ```objective-c
   NSDictionary *mediaObject = 
     [ACPMedia createMediaObjectWithName:@"media-name" 
               mediaId:@"media-id" 
               length:60 
               streamType:ACPMediaStreamTypeVod 
               mediaType:ACPMediaTypeVideo];
   
   NSMutableDictionary *mediaMetadata = 
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
   [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
   
   // Custom metadata keys
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   [_tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* Métadonnées de publicité standard:

   ```objective-c
   NSDictionary* adObject = 
     [ACPMedia createAdObjectWithName:@"ad-name" 
               adId:@"ad-id" 
               position:1 
               length:15];
   
   NSMutableDictionary* adMetadata = 
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
   [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
   
   // Custom metadata keys
   [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
   ```
