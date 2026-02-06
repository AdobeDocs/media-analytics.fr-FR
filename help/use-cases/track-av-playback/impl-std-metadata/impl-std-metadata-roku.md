---
title: Découvrez comment implémenter des métadonnées standard sur Roku.
description: Découvrez comment définir des métadonnées de vidéo et d’annonce publicitaire standard à envoyer avec les appels de suivi sur Roku.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 69%

---

# Mise en œuvre de métadonnées standard sur Roku{#implement-standard-metadata-on-roku}

Instanciez un objet de métadonnées standard, renseignez les variables souhaitées et définissez l’objet de métadonnées sur l’objet Media Heartbeat.

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

Consultez la liste complète des métadonnées vidéo dans la rubrique [Paramètres audio et vidéo](/help/implementation/variables/audio-video-parameters.md).
