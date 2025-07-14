---
title: Découvrez comment mettre en œuvre des métadonnées standard sur iOS
description: Découvrez comment définir des métadonnées vidéo et publicitaires standard à envoyer avec les appels de suivi sur iOS.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 100%

---

# Mise en œuvre de métadonnées standard sur iOS{#implement-standard-metadata-on-ios}

## Constantes de métadonnées

| Nom de constante | Description   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constante permettant d’associer des métadonnées standard à `MediaInfo ADBMediaObject` |

## Mise en œuvre

1. Créez un dictionnaire des paires clé-valeur des métadonnées publicitaires standard à l’aide de `ADBStandardMetadataKeys`.
   [Clés de métadonnées iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. Définissez le dictionnaire des métadonnées standard sur l’instance `MediaInfo` `ADBMediaObject` à l’aide de la constante de métadonnées standard pour les métadonnées.

1. Fournissez l’objet `MediaInfo` lorsque vous appelez l’API `trackSessionStart`.

### Exemple de mise en œuvre

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
