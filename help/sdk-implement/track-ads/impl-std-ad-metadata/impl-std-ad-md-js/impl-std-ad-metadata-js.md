---
title: Mise en oeuvre des métadonnées publicitaires standard à l’aide de JavaScript 2.x
description: Utilisation des métadonnées publicitaires standard dans le suivi des publicités dans un navigateur à l’aide d’applications JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 55%

---


# Mise en oeuvre des métadonnées publicitaires standard à l’aide de JavaScript 2.x{#implement-standard-ad-metadata-on-javascript}

## Constantes publicitaires

| Nom de constante | Description   |
|---|---|
| `StandardAdMetadata` | Constante permettant d’associer des métadonnées de publicité standard à un objet publicitaire |

## Mise en œuvre de métadonnées de publicité standard

Pour les métadonnées de publicité standard, créez un dictionnaire de paires clé-valeur de métadonnées de publicité standard à l’aide des clés pour votre plateforme :

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
