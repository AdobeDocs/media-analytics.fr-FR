---
title: Présentation des clés de métadonnées Chromecast
description: Découvrez comment définir des métadonnées vidéo et publicitaires standard à envoyer avec les appels de suivi sur Chromecast.
uuid: c446ad41-51b8-46d6-9bc1-abfae866023f
exl-id: ccc717ae-d846-4349-8282-5e3511ddeb9b
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 100%

---

# Clés de métadonnées Chromecast{#chromecast-metadata-keys}

Les métadonnées de vidéo et de publicité standard peuvent être définies respectivement sur les objets info de multimédia et de publicité. À l’aide des clés constantes des métadonnées vidéo/de publicité, définissez le dictionnaire contenant les métadonnées standard sur l’objet info avant d’appeler les API de suivi. Consultez les tableaux ci-dessous pour obtenir la liste complète des constantes de métadonnées standard, suivies d’un exemple.

## Constantes de métadonnées {#video-metadata-constants}

| Nom de métadonnées | Clé de données contextuelles | Nom de constante |
| --- | --- | --- |
| Programme | `a.media.show` | `ADBMobile.media.VideoMetadataKeys.SHOW` |
| Saison | `a.media.season` | `ADBMobile.media.VideoMetadataKeys.SEASON` |
| Épisode | `a.media.episode` | `ADBMobile.media.VideoMetadataKeys.EPISODE` |
| Ressource | `a.media.asset` | `ADBMobile.media.VideoMetadataKeys.TMS_ID` |
| Genre | `a.media.genre` | `ADBMobile.media.VideoMetadataKeys.GENRE` |
| Date de première diffusion | `a.media.airDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` |
| Date de première diffusion numérique | `a.media.digitalDate` | `ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE` |
| Évaluation | `a.media.rating` | `ADBMobile.media.VideoMetadataKeys.RATING` |
| Créateur | `a.media.originator` | `ADBMobile.media.VideoMetadataKeys.ORIGINATOR` |
| Réseau | `a.media.network` | `ADBMobile.media.VideoMetadataKeys.NETWORK` |
| Type de programme | `a.media.type` | `ADBMobile.media.VideoMetadataKeys.SHOW_TYPE` |
| Chargement de publicité | `a.media.adLoad` | `ADBMobile.media.VideoMetadataKeys.AD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `ADBMobile.media.VideoMetadataKeys.MVPD` |
| Autorisé | `a.media.pass.auth` | `ADBMobile.media.VideoMetadataKeys.AUTHORIZED` |
| Partie de la journée | `a.media.dayPart` | `ADBMobile.media.VideoMetadataKeys.DAY_PART` |
| Flux | `a.media.feed` | `ADBMobile.media.VideoMetadataKeys.FEED` |
| Format de diffusion | `a.media.format` | `ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT` |

## Constantes de métadonnées de publicité {#ad-metadata-constants}

| Nom de métadonnées | Clé de données contextuelles | Nom de constante |
| --- | --- | --- |
| Annonceur | `a.media.ad.advertiser` | `ADBMobile.media.AdMetadataKeys.ADVERTISER` |
| ID de campagne | `a.media.ad.campaign` | `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` |
| ID d’élément créatif | `a.media.ad.creative` | `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` |
| Identifiant de référencement | `a.media.ad.placement` | `ADBMobile.media.AdMetadataKeys.PLACEMENT_ID` |
| ID du site | `a.media.ad.site` | `ADBMobile.media.AdMetadataKeys.SITE_ID` |
| URL de l’élément créatif | `a.media.ad.creativeURL` | `ADBMobile.media.AdMetadataKeys.CREATIVE_URL` |

## Exemples de mise en œuvre pour Chromecast {#sample-implementations-for-chromecast}

### Vidéo

```js
// setting Standard Video Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["videotype"] = "episode"; 
 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "sample show"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SEASON] = "sample season"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.EPISODE] = "sample episode"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.TMS_ID] = "sample tms_id"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "sample genre"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "sample first_air_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "sample first_digital_date"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.RATING] = "sample rating"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.ORIGINATOR] = "sample originator"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.NETWORK] = "sample network"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.SHOW_TYPE] = "sample show type"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "sample ad load"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.MVPD] = "sample mvpd"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.AUTHORIZED] = "sample authorized"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.DAY_PART] = "sample day_part"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.FEED] = "sample feed"; 
standardVideoMetadata[ADBMobile.media.VideoMetadataKeys.STREAM_FORMAT] = "sample format"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Audio

```js
// setting Standard Audio Metadata as context data on trackLoad API mediaContextData = { } 
mediaMetadata["audiotype"] = "podcast"; 
var standardAudioMetadata = {}; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ARTIST] = "sample artist"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "sample album" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.LABEL] = "sample label"; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.AUTHOR] = "sample author" ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.STATION] = "sample station " ; 
standardAudioMetadata[ADBMobile.media.AudioMetadataKeys.PUBLISHER] = "sample publisher"; 
 
var mediaObject = ADBMobile.media.createMediaObject(content.name, content.id, content.length, content.streamType, content.mediaType); 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudiooMetadata] = standardAudiooMetadata; 
ADBMobile.media.trackSessionStart(mediaObject, mediaMetadata); 
```

### Publicités

```js
// setting Standard Ad Metadata as context data on ad start event 
var standardAdMetadata = {}; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "sample campaign"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "sample advertiser" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "sample creativeid"; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.PLACEMENT_ID] = "sample placement id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.SITE_ID] = "sample site id" ; 
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_URL] = "sample creative url"; 
 
var adObject = ADBMobile.media.createAdObject(ad.name, ad.id, ad.position, ad.length); 
adObject[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardVideoMetadata; 
 
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, this._player.getAdInfo(), adContextData);
```
