---
title: Découvrez comment mettre en oeuvre des métadonnées de publicité standard sur Android
description: Utilisation des métadonnées publicitaires standard dans le suivi des publicités sur Android.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 86%

---

# Mise en œuvre de métadonnées de publicité standard sur Android{#implement-standard-ad-metadata-on-android}

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
