---
description: valeur nulle
seo-description: valeur nulle
seo-title: Mise en œuvre de métadonnées standard sur Android
title: Mise en œuvre de métadonnées standard sur Android
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 46797deb402fed1c4d4781507c279407f8c13f2e

---


# Mise en œuvre de métadonnées standard sur Android{#implement-standard-metadata-on-android}

## Constantes de métadonnées standard

| Nom de constante | Description   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante permettant d’associer des métadonnées standard à `MediaObject`. |

## Référence de l’API Clés de métadonnées

* Créez un ensemble `HashMap` de paires clé-valeur de métadonnées standard.
   * [Touches de métadonnées vidéo](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Clés de métadonnées audio](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Définissez un `HashMap` de métadonnées standard sur `MediaInfo` en utilisant la constante de métadonnées standard pour les métadonnées.
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

## Exemples d’implémentation

### Vidéo

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Audio

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
