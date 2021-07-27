---
title: Découvrez comment implémenter des métadonnées standard sur Android
description: Découvrez comment définir des métadonnées de vidéo et d’annonce publicitaire standard à envoyer avec les appels de suivi sur Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '108'
ht-degree: 100%

---

# Mise en œuvre de métadonnées standard sur Android{#implement-standard-metadata-on-android}

## Constantes de métadonnées standard

| Nom de constante | Description   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante permettant d’associer des métadonnées standard à `MediaObject`. |

## Référence d’API Clés de métadonnées

* Créez un ensemble `HashMap` de paires clé-valeur de métadonnées standard.
   * [Clés de métadonnées vidéo](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Clés de métadonnées audio](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Définissez un `HashMap` de métadonnées standard sur `MediaInfo` en utilisant la constante de métadonnées standard pour les métadonnées.
* Fournissez l’objet `MediaInfo` lorsque vous appelez l’API `trackSessionStart()`.

## Exemples de mise en œuvre

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
