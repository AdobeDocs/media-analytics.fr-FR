---
title: Mise en œuvre de métadonnées standard sur Roku
description: Décrit la définition des métadonnées vidéo et publicitaires standard à envoyer avec les appels de suivi sur Roku.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Mise en œuvre de métadonnées standard sur Roku {#implement-standard-metadata-on-roku}

Instanciez un objet de métadonnées standard, renseignez les variables désirées et définissez l’objet de métadonnées sur l’objet Media Heartbeat.

**Vidéo :**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**Audio :**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

Consultez la liste complète des métadonnées vidéo dans la rubrique [Paramètres audio et vidéo](/help/metrics-and-metadata/audio-video-parameters.md).

