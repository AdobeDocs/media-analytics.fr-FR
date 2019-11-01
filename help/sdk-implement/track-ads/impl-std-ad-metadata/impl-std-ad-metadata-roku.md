---
title: Mise en œuvre de métadonnées de publicité standard sur Roku
description: Utilisation des métadonnées publicitaires standard dans le suivi des publicités sur Roku.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Mise en œuvre de métadonnées de publicité standard sur Roku{#implement-standard-ad-metadata-on-roku}

## Mise en oeuvre des métadonnées publicitaires standard

Pour les métadonnées publicitaires standard, créez un dictionnaire de paires clé-valeur de métadonnées publicitaires standard à l’aide des clés de votre plateforme :

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

