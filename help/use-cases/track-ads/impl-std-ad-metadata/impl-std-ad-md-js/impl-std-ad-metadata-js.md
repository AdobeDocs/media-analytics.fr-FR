---
title: Découvrez comment implémenter des métadonnées d’annonce publicitaire standard à l’aide de JavaScript 2.x
description: Comment utiliser des métadonnées d’annonce publicitaire standard dans le suivi publicitaire au sein d’un navigateur à l’aide d’applications JavaScript 2.x.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 100%

---

# Implémentation de métadonnées d’annonce publicitaire standard à l’aide de JavaScript 2.x {#implement-standard-ad-metadata-on-javascript}

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
