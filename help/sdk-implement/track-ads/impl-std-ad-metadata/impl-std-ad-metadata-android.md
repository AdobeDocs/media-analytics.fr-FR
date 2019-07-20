---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées de publicité standard sur Android
title: Mise en œuvre de métadonnées de publicité standard sur Android
uuid: 19 b 98 bc 1-c 659-4182-a 4 ff-b 3340 fe 2453 c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Mise en œuvre de métadonnées de publicité standard sur Android{#implement-standard-ad-metadata-on-android}

## Constantes publicitaires

| Nom de constante | Description   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante permettant d’associer des métadonnées publicitaires standard à Ad `MediaObject`. |

## Métadonnées publicitaires standard de mise en œuvre

Pour les métadonnées publicitaires standard, créez un dictionnaire des paires clé-valeur des métadonnées publicitaires standard à l'aide des clés de votre plateforme :

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

