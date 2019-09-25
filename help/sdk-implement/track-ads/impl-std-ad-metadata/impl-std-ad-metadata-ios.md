---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées de publicité standard sur iOS
title: Mise en œuvre de métadonnées de publicité standard sur iOS
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Mise en œuvre de métadonnées de publicité standard sur iOS{#implement-standard-ad-metadata-on-ios}

## Constantes publicitaires

| Nom de constante | Description   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## Mise en oeuvre des métadonnées publicitaires standard

Pour les métadonnées publicitaires standard, créez un dictionnaire de paires clé-valeur de métadonnées publicitaires standard à l’aide des clés de votre plateforme :

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Clés de métadonnées iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
