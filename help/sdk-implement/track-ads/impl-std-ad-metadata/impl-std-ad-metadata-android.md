---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées de publicité standard sur Android
title: Mise en œuvre de métadonnées de publicité standard sur Android
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Mise en œuvre de métadonnées de publicité standard sur Android{#implement-standard-ad-metadata-on-android}

## Constantes publicitaires

| Nom de constante | Description   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante permettant d’associer des métadonnées publicitaires standard à Ad `MediaObject`. |

## Mise en oeuvre des métadonnées publicitaires standard

Pour les métadonnées publicitaires standard, créez un dictionnaire de paires clé-valeur de métadonnées publicitaires standard à l’aide des clés de votre plateforme :

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

