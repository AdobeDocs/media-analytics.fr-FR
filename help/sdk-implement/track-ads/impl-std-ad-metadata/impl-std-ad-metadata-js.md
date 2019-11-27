---
title: Mise en œuvre de métadonnées de publicité standard sur JavaScript
description: Utilisation des métadonnées publicitaires standard dans le suivi des publicités dans les applications de navigateur (JS).
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Mise en œuvre de métadonnées de publicité standard sur JavaScript {#implement-standard-ad-metadata-on-javascript}

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

