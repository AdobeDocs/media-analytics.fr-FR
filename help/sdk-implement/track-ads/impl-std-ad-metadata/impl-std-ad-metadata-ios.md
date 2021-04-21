---
title: Mise en œuvre de métadonnées de publicité standard sur iOS
description: Utilisation des métadonnées publicitaires standard dans le suivi des publicités sur iOS.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '62'
ht-degree: 100%

---

# Mise en œuvre de métadonnées de publicité standard sur iOS {#implement-standard-ad-metadata-on-ios}

## Constantes publicitaires

| Nom de constante | Description   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constante permettant d’associer des métadonnées publicitaires standard à `AdInfo ADBMediaObject` |

## Mise en œuvre de métadonnées de publicité standard

Pour les métadonnées de publicité standard, créez un dictionnaire de paires clé-valeur de métadonnées de publicité standard à l’aide des clés pour votre plateforme :

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[Clés de métadonnées iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
