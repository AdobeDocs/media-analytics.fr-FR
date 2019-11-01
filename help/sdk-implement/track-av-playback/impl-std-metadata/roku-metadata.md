---
title: Clés de métadonnées Roku
description: Cette rubrique décrit les clés de métadonnées de Roku disponibles.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Clés de métadonnées Roku{#roku-metadata-keys}

Les métadonnées vidéo, audio et publicitaires standard peuvent être définies sur les objets d’informations sur les médias et les publicités, respectivement. À l’aide des clés constantes des métadonnées vidéo/de publicité, définissez le dictionnaire contenant les métadonnées standard sur l’objet info avant d’appeler les API de suivi. Consultez les tableaux ci-dessous pour obtenir la liste complète des constantes de métadonnées standard, suivies d’un exemple.

## Constantes de métadonnées vidéo {#video-metadata-constants}

| Nom de métadonnées | Clé de données contextuelles | Nom de constante |
| --- | --- | --- |
| Programme | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Saison | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Épisode | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Ressource | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Genre | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Date de première diffusion | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Date de première diffusion numérique | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Évaluation | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Créateur | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Réseau | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Type de programme | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Chargement de publicité | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Autorisé | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Partie de la journée | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Flux | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Format de diffusion | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Constantes de métadonnées audio {#audio-metadata-constants}

| Nom de métadonnées | Clé de données contextuelles | Nom de constante |
| --- | --- | --- |
| Artiste | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Album | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Étiquette | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Auteur | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Station | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Éditeur | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Constantes de métadonnées de publicité {#ad-metadata-constants}

| Nom de métadonnées | Clé de données contextuelles | Nom de constante |
| --- | --- | --- |
| Annonceur | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| ID de campagne | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| ID d’élément créatif | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| Identifiant de référencement | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| ID du site | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| URL de l’élément créatif | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Constantes {#constants}

Vous pouvez utiliser les constantes suivantes pour suivre les événements de média :

### Autres constantes

| Constante | Description   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Constante pour la source d’erreur résidant dans le lecteur |

### Constantes MediaObjectkey (utilisées comme clés dans les instances MediaObject)

| Constante | Description   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Constante permettant de définir des métadonnées sur le `MediaInfo``trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Constante permettant de définir les métadonnées publicitaires sur la `EventData` variable `trackEvent` |
| `MEDIA_RESUMED` | Constante pour envoyer un heartbeat repris par vidéo. To resume video tracking of previously stopped content, you need to set the `MEDIA_RESUMED` property on the `mediaInfo` object when you call `mediaTrackLoad`. (`MEDIA_RESUMED` is not an event that you can track using the `mediaTrackEvent` API.) La propriété `MEDIA_RESUMED` doit être définie sur true lorsqu’une application souhaite continuer à suivre le contenu que l’utilisateur a arrêté de regarder mais qu’il désire continuer à regarder. <br/><br/>Par exemple, supposons qu’un utilisateur regarde 30 % du contenu, puis ferme l’application. La session est alors terminée. Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they left off, then the application should set `MEDIA_RESUMED` to "true" while calling the `mediaTrackLoad` API. Il en résulte que ces deux sessions multimédia distinctes correspondant au même contenu vidéo peuvent être liées. Exemple : <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>Cette opération crée une nouvelle session pour la vidéo, mais elle provoque également l’envoi par le kit SDK d’une demande de pulsation avec le type d’événement « resume », qui peut être utilisé dans les rapports pour relier deux sessions multimédia différentes. |

### Constantes de type de contenu

| Constante | Description   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Constante pour le type de diffusion LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Constante pour le type de diffusion VOD |

### Constantes de type d’événement (utilisées pour l’appel trackEvent)

| Constante | Description   |
|---|---|
| `MEDIA_BUFFER_START` | Type d’événement pour le début de la mémoire tampon |
| `MEDIA_BUFFER_COMPLETE` | Type d’événement pour la fin de la mémoire tampon |
| `MEDIA_SEEK_START` | Type d’événement pour le début de la recherche |
| `MEDIA_SEEK_COMPLETE` | Type d’événement pour la fin de la recherche |
| `MEDIA_BITRATE_CHANGE` | Type d’événement pour le changement de débit binaire |
| `MEDIA_CHAPTER_START` | Type d’événement pour le début du chapitre |
| `MEDIA_CHAPTER_COMPLETE` | Type d’événement pour la fin du chapitre |
| `MEDIA_CHAPTER_SKIP` | Type d’événement pour le début de la publicité |
| `MEDIA_AD_BREAK_START` | Type d’événement pour le début de la publicité |
| `MEDIA_AD_BREAK_COMPLETE` | Type d’événement pour la fin de l’AdBreak |
| `MEDIA_AD_BREAK_SKIP` | Type d’événement pour le saut de l’AdBreak |
| `MEDIA_AD_START` | Type d’événement pour le début de la publicité |
| `MEDIA_AD_COMPLETE` | Type d’événement pour la fin de la publicité |
| `MEDIA_AD_SKIP` | Type d’événement pour le saut de la publicité |

