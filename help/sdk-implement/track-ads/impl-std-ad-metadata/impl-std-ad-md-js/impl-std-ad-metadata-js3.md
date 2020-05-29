---
title: Mise en oeuvre des métadonnées publicitaires standard à l’aide de JavaScript 3.x
description: Utilisation des métadonnées publicitaires standard dans le suivi des publicités dans un navigateur à l’aide d’applications JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 83b38ac8f7fc88f982d194e776efccf8d5b983e4
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 44%

---


# Mise en oeuvre des métadonnées publicitaires standard à l’aide de JavaScript 3.x{#implement-standard-ad-metadata-on-javascript}

## Mise en œuvre de métadonnées de publicité standard

Pour les métadonnées de publicité standard, créez un dictionnaire de paires clé-valeur de métadonnées de publicité standard à l’aide des clés pour votre plateforme :

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
