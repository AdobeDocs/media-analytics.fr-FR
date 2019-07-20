---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées de publicité standard sur Roku
title: Mise en œuvre de métadonnées de publicité standard sur Roku
uuid: 20 a 437 d 7-18 b 8-4099-ac 81-9 f 3628384236
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Mise en œuvre de métadonnées de publicité standard sur Roku{#implement-standard-ad-metadata-on-roku}

## Métadonnées publicitaires standard de mise en œuvre

Pour les métadonnées publicitaires standard, créez un dictionnaire des paires clé-valeur des métadonnées publicitaires standard à l'aide des clés de votre plateforme :

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

