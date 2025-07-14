---
title: Découvrez comment implémenter des métadonnées d’annonce publicitaire standard à l’aide de JavaScript 3.x
description: Comment utiliser les métadonnées d’annonce publicitaire standard dans le suivi publicitaire au sein d’un navigateur à l’aide d’applications JavaScript 3.x.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 100%

---

# Implémentation de métadonnées d’annonce publicitaire standard à l’aide de JavaScript 3.x {#implement-standard-ad-metadata-on-javascript}

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
