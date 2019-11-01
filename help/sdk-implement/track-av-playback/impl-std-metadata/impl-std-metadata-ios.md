---
title: Mise en œuvre de métadonnées standard sur iOS
description: Décrit la définition des métadonnées vidéo et publicitaires standard à envoyer avec les appels de suivi sur iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Mise en œuvre de métadonnées standard sur iOS{#implement-standard-metadata-on-ios}

## Constantes de métadonnées

| Nom de constante | Description   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante permettant d’associer des métadonnées standard à `MediaInfo ADBMediaObject` |

## Mise en œuvre

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys`
   [Clés de métadonnées IOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Définissez le dictionnaire des métadonnées standard sur l’instance `MediaInfo``ADBMediaObject`   à l’aide de la constante de métadonnées standard pour les métadonnées.

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

### Exemple de mise en oeuvre

Instanciez un objet de métadonnées standard, renseignez les variables désirées et définissez l’objet de métadonnées sur l’objet Media Heartbeat. Par exemple :

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

