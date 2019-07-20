---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées de publicité standard sur JavaScript
title: Mise en œuvre de métadonnées de publicité standard sur JavaScript
uuid: 4 ea 10 c 5 a-ae 2 b -45 d 0-aad 3-9 f 10028 ee 7 c 3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Mise en œuvre de métadonnées de publicité standard sur JavaScript{#implement-standard-ad-metadata-on-javascript}

## Constantes publicitaires

| Nom de constante | Description   |
|---|---|
| `StandardAdMetadata` | Constante permettant d’associer des métadonnées de publicité standard à un objet publicitaire |

## Métadonnées publicitaires standard de mise en œuvre

Pour les métadonnées publicitaires standard, créez un dictionnaire des paires clé-valeur des métadonnées publicitaires standard à l'aide des clés de votre plateforme :

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

