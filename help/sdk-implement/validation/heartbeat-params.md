---
seo-title: Descriptions des paramètres Heartbeat
title: Descriptions des paramètres Heartbeat
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Descriptions des paramètres de Media Analytics (Heartbeat){#heartbeat-parameter-descriptions}

Liste des paramètres Media Analytics qu'Adobe collecte et traite sur le serveur des pulsations :

## Tous les événements

| Nom | Obligatoire / Facultatif | Source de données | Description   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | SDK Media | Type d’événement suivi. Types d’événement : <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | SDK Media | Horodatage du dernier événement du même type dans cette session. La valeur est `-1` |
| `l:event:ts` | R | SDK Media | Horodatage de l’événement. |
| `l:event:duration` | R | SDK Media | Cette valeur est définie en interne (en millisecondes) par la bibliothèque VHL et non par le lecteur. Elle permet de calculer les mesures de temps passé sur le serveur principal. For example `a.media.totalTimePlayed` `type=play` Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., `type=complete` `type=chapter_complete` `type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | Curseur de lecture présent dans la ressource active (principale ou publicité) lorsque l’événement a été enregistré. |
| `s:event:sid` | R | SDK Media | ID de session (chaîne générée de manière aléatoire). Tous les événements d’une même session (vidéo + publicités) doivent être identiques. |
| `l:asset:duration / l:asset:length` (Renommé de `length``duration` | R | `VideoInfo` | Durée de la ressource vidéo de la ressource principale. |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | Éditeur de la ressource. |
| `s:asset:video_id` | R | `VideoInfo` | Identifiant qui identifie de manière unique la vidéo dans le catalogue de l’éditeur. |
| `s:asset:type` | R | SDK Media | Type de ressource (principale ou publicité). |
| `s:stream:type` | R | `VideoInfo` | Type de diffusion ; peut être l’un des suivants : <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>. |
| `s:user:id` | O | Objet Config pour mobile, identifiant visiteur VisitorID de mesure d’application | Identifiant de visiteur spécifique à l’utilisateur. |
| `s:user:aid` | O | Organisation Experience Cloud | Valeur de l’identifiant de visiteur Analytics de l’utilisateur. |
| `s:user:mid` | R | Organisation Experience Cloud | Valeur de l’identifiant visiteur Experience Cloud de l’utilisateur. |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | Tous les identifiants d’utilisateur client définis sur Audience Manager. |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | Identifiant(s) de suite(s) de rapports | Adobe Analytics RSID où les rapports doivent être envoyés. |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | Serveur de suivi Adobe Analytics. |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | Indique si le trafic s’effectue par HTTPS (s’il est défini sur 1) ou par HTTP (s’il est défini sur 0). |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | Défini sur « primetime » pour les lecteurs Primetime ou sur l’OVP réel pour les autres lecteurs. |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | Chaîne de version OVP. |
| `s:sp:player_name` | R | `VideoInfo` | Nom du lecteur vidéo (logiciel du lecteur réel, sert à identifier le lecteur). |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | Canal sur lequel l’utilisateur visionne le contenu. Pour une application mobile, nom de l’application. Pour un site Web, nom du domaine. |
| `s:sp:hb_version` | R | SDK Media | Numéro de la version de la bibliothèque VideoHeartbeat émettant l’appel. |
| `l:stream:bitrate` | R | `QoSInfo` | Valeur actuelle du débit de diffusion (en bit/s). |

## Événements d’erreur

| Nom | Obligatoire / Facultatif | Source de données | Description   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | SDK Media | Source de l’erreur, interne au lecteur ou au niveau de l’application. |
| `s:event:id` | R | SDK Media | Identifiant d’erreur, identifie l’erreur de manière unique. |

## Événements publicitaires

| Nom | Obligatoire / Facultatif | Source de données | Description   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | Nom de la publicité. |
| `s:asset:ad_sid` | R | SDK Media | Identifiant unique généré par le kit SDK Media, ajouté à tous les pings de publicité. |
| `s:asset:pod_id` | R | SDK Media | Identifiant de la capsule dans la vidéo. Cette valeur est calculée automatiquement à partir de la formule suivante : `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | Index de la publicité dans la capsule (la première publicité affiche index 0, la deuxième publicité affiche index 1, etc.). |
| `s:asset:resolver` | R | `AdBreakInfo` | Résolveur de publicité. |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | Métadonnées de publicité personnalisées. |

## Événements de chapitre

| Nom | Obligatoire / Facultatif | Source de données | Description   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | SDK Media | Identifiant unique associé à l’instance de lecture du chapitre.  Remarque : Un chapitre peut être lu à plusieurs reprises en raison des opérations de recherche vers l’arrière effectuées par l’utilisateur. |
| `s:stream:chapter_name` | O | `ChapterInfo` | Nom convivial (p. ex., lisible par un humain) du chapitre. |
| `s:stream:chapter_id` | R | SDK Media | Identifiant unique du chapitre. Cette valeur est calculée automatiquement à partir de la formule suivante : `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | Index du chapitre parmi la liste de chapitres (commençant par 1). |
| `l:stream:chapter_offset` | R | `ChapterInfo` | Décalage du chapitre (exprimé en secondes) à l’intérieur du contenu principal, à l’exception des publicités. |
| `l:stream:chapter_length` | R | `ChapterInfo` | Durée du chapitre (exprimée en secondes). |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | Métadonnées de chapitre personnalisées. |

## Événement de fin de session

| Nom | Obligatoire / Facultatif | Source de données | Description   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | SDK Media | Le `end` `close` |

