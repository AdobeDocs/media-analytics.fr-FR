---
title: Mise en œuvre de métadonnées de publicité standard sur Android
description: Utilisation des métadonnées publicitaires standard dans le suivi des publicités sur Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Mise en œuvre de métadonnées de publicité standard sur Android {#implement-standard-ad-metadata-on-android}

## Constantes publicitaires

| Nom de constante | Description   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | Constante permettant d’associer des métadonnées publicitaires standard à Ad `MediaObject`. |

## Mise en œuvre de métadonnées de publicité standard

Pour les métadonnées de publicité standard, créez un dictionnaire de paires clé-valeur de métadonnées de publicité standard à l’aide des clés pour votre plateforme :

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

