---
seo-title: Descriptions des paramètres Heartbeat
title: Descriptions des paramètres Heartbeat
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 10a5d921953339bef1cde2f802eb9ce0cb1bbe4b

---


# Descriptions des paramètres de Media Analytics (pulsations){#heartbeat-parameter-descriptions}

Liste des paramètres Media Analytics qu'Adobe collecte et traite sur le serveur Media Analytics (pulsations) :

## Tous les événements

| Nom | Source de données |  Description  |
| ---  | --- | --- |
| s:event:type | SDK Media | (Required)<br/><br/>The type of the event being tracked. Types d’événement : <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | SDK Media | (Required)<br/><br/>The timestamp of the last event of the same type in this session. La valeur est -1. |
| l:event:ts | SDK Media | (Required)<br/><br/>The timestamp of the event. |
| l:event:duration | SDK Media | (Required)<br/><br/>This value is set internally (in milliseconds) by the Media SDK, not by the player. Elle permet de calculer les mesures de temps passé sur le serveur principal. Par exemple : a. media. totaltimeplayed correspond à la durée de toutes les pulsations Play (type = play) générées. <br/>*Remarque :* Ce paramètre est défini sur 0 pour certains événements car il s'agit de « events change events » (par exemple, type = complete, type = chapter_ complete ou type = bitrate_ change). |
| l:event:playhead | Videoinfo | (Required)<br/><br/>The playhead was inside the currently active asset (main or ad), when the event was recorded. |
| s:event:sid | SDK Media | (Required)<br/><br/>The session ID (a randomly generated string). Tous les événements d’une même session (vidéo + publicités) doivent être identiques. |
| l : ressource : duration/l : ressource : length <br/>(renommée durée de la durée) | Videoinfo | (Required)<br/><br/>The video asset length of the main asset. |
| s:asset:publisher | MediaHeartbeatConfig | (Required)<br/><br/>The publisher of the asset. |
| s:asset:video_id | Videoinfo | (Required)<br/><br/>An ID uniquely identifying the video in the publisher's catalog. |
| s:asset:type | SDK Media | (Required)<br/><br/>The asset type (main or ad). |
| s:stream:type | Videoinfo | (Obligatoire)<br/><br/>Type de flux. Peut être l'une des suivantes : <ul> <li> live </li> <li> vod </li> <li> linéaire </li> </ul> |
| s:user:id | Objet Config pour mobile, identifiant visiteur VisitorID de mesure d’application | (Optional)<br/><br/>User's specifically set Visitor ID. |
| s:user:aid | Organisation Experience Cloud | (Optional)<br/><br/>The user's Analytics Visitor ID value. |
| s:user:mid | Organisation Experience Cloud | (Required)<br/><br/>The user's Experience cloud visitor ID value. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Optional)<br/><br/>All customer user IDs set on Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:aam:blob | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:sc:rsid | Identifiant(s) de suite(s) de rapports | (Obligatoire)<br/><br/>Adobe Analytics RSID où les rapports doivent être envoyés. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obligatoire)<br/><br/>Serveur de suivi Adobe Analytics. |
| h:sc:ssl | MediaHeartbeatConfig | (Required)<br/><br/>Whether the traffic is over HTTPS (if set to 1) or over HTTP (is set to 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Optional)<br/><br/>Set to "primetime" for Primetime players, or the actual OVP for other players. |
| s:sp:sdk | MediaHeartbeatConfig | (Required)<br/><br/>The OVP version string. |
| s:sp:player_name | Videoinfo | (Required)<br/><br/>Video player name (the actual player software, used to identify the player). |
| s:sp:channel | MediaHeartbeatConfig | (Optional)<br/><br/>The channel where the user is watching the content. Pour une application mobile, nom de l’application. Pour un site Web, nom du domaine. |
| s:sp:hb_version | SDK Media | (Obligatoire)<br/><br/>Numéro de version de la bibliothèque du kit de développement multimédia émettant l'appel. |
| l:stream:bitrate | Qosinfo | (Required)<br/><br/>The current value of the stream bitrate (in bps). |

## Événements d’erreur

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:event:source | SDK Media | (Required)<br/><br/>The source of the error, either player-internal, or the application-level. |
| s:event:id | SDK Media | (Required)<br/><br/>Error ID, uniquely identifies the error. |

## Événements publicitaires

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:asset:ad_id | Adinfo | (Obligatoire)<br/><br/>Nom de la publicité. |
| s:asset:ad_sid | SDK Media | (Required)<br/><br/>A unique identifier generated by the Media SDK, appended to all ad-related pings. |
| s:asset:pod_id | SDK Media | (Required)<br/><br/>Pod ID inside the video. This value is computed automatically based on the following formula: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | Adbreakinfo | (Required)<br/><br/>Index of the ad inside the pod (the first ad has index 0, the second ad has index 1, etc.). |
| s:asset:resolver | Adbreakinfo | (Obligatoire)<br/><br/>Résolveur de publicité. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Optional)<br/><br/>The custom ad metadata. |

## Événements de chapitre

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:stream:chapter_sid | SDK Media | (Required)<br/><br/>The unique identifier associated to the playback instance of the chapter.  <br/> **Remarque :** Un chapitre peut être lu à plusieurs reprises en raison des opérations de recherche vers l’arrière effectuées par l’utilisateur. |
| s:stream:chapter_name | Chapterinfo | (Optional)<br/><br/>The chapter's friendly (i.e., human readable) name. |
| s:stream:chapter_id | SDK Media | (Required)<br/><br/>The unique ID of the chapter. This value is computed automatically based on the following formula: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:chapter_pos | Chapterinfo | (Required)<br/><br/>The chapter's index in the list of chapters (starting with 1). |
| l:stream:chapter_offset | Chapterinfo | (Required)<br/><br/>The chapter's offset (expressed in seconds) inside the main content, excluding ads. |
| l:stream:chapter_length | Chapterinfo | (Required)<br/><br/>The chapter's duration (expressed in seconds). |
| s:meta:custom_chapter_metadata.x | Chapterinfo | (Facultatif)<br/><br/>Métadonnées de chapitre personnalisées. |

## Événement de fin de session

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:event:type=end | SDK Media | (Obligatoire) <br/><br/>`end``close` |

