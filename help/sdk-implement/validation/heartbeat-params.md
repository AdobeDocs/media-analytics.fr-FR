---
title: Descriptions des paramètres Heartbeat
description: Liste des paramètres Heartbeat que Adobe collecte et traite sur le serveur Media Analytics (pulsations).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Descriptions des paramètres Media Analytics (pulsations) {#heartbeat-parameter-descriptions}

Liste des paramètres Media Analytics collectés et traités par Adobe sur le serveur Media Analytics (pulsations) :

## Tous les événements

| Nom | Source de données |  Description  |
| ---  | --- | --- |
| s:event:type | SDK Media | (Obligatoire)<br/><br/>Type d’événement suivi. Types d’événement : <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | SDK Media | (Obligatoire)<br/><br/>Horodatage du dernier événement du même type dans cette session. La valeur est -1. |
| l:event:ts | SDK Media | (Obligatoire)<br/><br/>Horodatage de l’événement. |
| l:event:duration | SDK Media | (Obligatoire)<br/><br/>Cette valeur est définie en interne (en millisecondes) par le SDK Media et non par le lecteur. Elle permet de calculer les mesures de temps passé sur le serveur principal. Par exemple, a.media.totalTimePlayed est calculé en tant que somme de la durée de toutes les pulsations Play (type=play) générées. <br/>*Remarque :*ce paramètre est défini sur 0 pour certains événements, car il s’agit d’« événements de changement d’état » (par exemple, type=complete, type=chapter_complete ou type=bitrate_change). |
| l:event:playhead | VideoInfo | (Obligatoire)<br/><br/>Curseur de lecture présent dans la ressource active (principale ou publicité) lorsque l’événement a été enregistré. |
| s:event:sid | SDK Media | (Obligatoire)<br/><br/>ID de session (chaîne générée de manière aléatoire). Tous les événements d’une même session (vidéo + publicités) doivent être identiques. |
| l:asset:length / l:asset:length <br/>(renommé à partir de la durée) | VideoInfo | (Obligatoire)<br/><br/>Durée de la ressource vidéo de la ressource principale. |
| s:asset:publisher | MediaHeartbeatConfig | (Obligatoire)<br/><br/>Éditeur de la ressource. |
| s:asset:video_id | VideoInfo | (Obligatoire)<br/><br/>Identifiant qui identifie de manière unique la vidéo dans le catalogue de l’éditeur. |
| s:asset:type | SDK Media | (Obligatoire)<br/><br/>Type de ressource (principale ou publicité). |
| s:stream:type | VideoInfo | (Obligatoire)<br/><br/>Type de flux. Peut être l’un des paramètres suivants : <ul> <li> live </li> <li> vod </li> <li> linéaire </li> </ul> |
| s:user:id | Objet Config pour mobile, identifiant visiteur VisitorID de mesure d’application | (Facultatif)<br/><br/>Identifiant de visiteur spécifique à l’utilisateur. |
| s:user:aid | Organisation Experience Cloud | (Facultatif)<br/><br/>Valeur de l’identifiant de visiteur Analytics de l’utilisateur. |
| s:user:mid | Organisation Experience Cloud | (Obligatoire)<br/><br/>Valeur de l’identifiant visiteur Experience Cloud de l’utilisateur. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Facultatif)<br/><br/>Tous les identifiants d’utilisateur client définis sur Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Obligatoire)<br/><br/>Données AAM transmises à chaque charge utile après aa_start. |
| s:aam:blob | MediaHeartbeatConfig | (Obligatoire)<br/><br/>Données AAM transmises à chaque charge utile après aa_start. |
| s:sc:rsid | Identifiant(s) de suite(s) de rapports | (Obligatoire)<br/><br/>RSID Adobe Analytics où les rapports doivent être envoyés. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obligatoire)<br/><br/>Serveur de suivi Adobe Analytics. |
| h:sc:ssl | MediaHeartbeatConfig | (Obligatoire)<br/><br/>Indique si le trafic s’effectue par HTTPS (s’il est défini sur 1) ou par HTTP (s’il est défini sur 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Facultatif)<br/><br/>Défini sur « primetime » pour les lecteurs Primetime ou sur l’OVP réel pour les autres lecteurs. |
| s:sp:sdk | MediaHeartbeatConfig | (Obligatoire)<br/><br/>Chaîne de version OVP. |
| s:sp:player_name | VideoInfo | (Obligatoire)<br/><br/>Nom du lecteur vidéo (logiciel du lecteur réel, sert à identifier le lecteur). |
| s:sp:channel | MediaHeartbeatConfig | (Facultatif)<br/><br/>Canal sur lequel l’utilisateur visionne le contenu. Pour une application mobile, nom de l’application. Pour un site web, nom du domaine. |
| s:sp:hb_version | SDK Media | (Obligatoire)<br/><br/>Numéro de version de la bibliothèque du SDK Media qui émet l’appel. |
| l:stream:bitrate | QoSInfo | (Obligatoire)<br/><br/>Valeur actuelle du débit de diffusion (en bit/s). |

## Événements d’erreur

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:event:source | SDK Media | (Obligatoire)<br/><br/>Source de l’erreur, interne au lecteur ou au niveau de l’application. |
| s:event:id | SDK Media | (Obligatoire)<br/><br/>Identifiant d’erreur, identifie l’erreur de manière unique. |

## Événements publicitaires

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Obligatoire)<br/><br/>Nom de la publicité. |
| s:asset:ad_sid | SDK Media | (Obligatoire)<br/><br/>Identifiant unique généré par le SDK Media, ajouté à tous les pings de publicité. |
| s:asset:pod_id | SDK Media | (Obligatoire)<br/><br/>Identifiant de la capsule dans la vidéo. Cette valeur est calculée automatiquement à partir de la formule suivante : <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Obligatoire)<br/><br/>Index de la publicité dans la capsule (la première publicité affiche index 0, la deuxième publicité affiche index 1, etc.). |
| s:asset:resolver | AdBreakInfo | (Obligatoire)<br/><br/>Résolveur de la publicité. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Facultatif)<br/><br/>Métadonnées de publicité personnalisées. |

## Événements de chapitre

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:stream:chapter_sid | SDK Media | (Obligatoire)<br/><br/>Identifiant unique associé à l’instance de lecture du chapitre. <br/> **Remarque :** Un chapitre peut être lu à plusieurs reprises en raison des opérations de recherche vers l’arrière effectuées par l’utilisateur. |
| s:stream:chapter_name | ChapterInfo | (Facultatif)<br/><br/>Nom convivial (c-à-d., lisible par un humain) du chapitre. |
| s:stream:chapter_id | SDK Media | (Obligatoire)<br/><br/>Identifiant unique du chapitre. Cette valeur est calculée automatiquement à partir de la formule suivante : <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:chapter_pos | ChapterInfo | (Obligatoire)<br/><br/>Index du chapitre parmi la liste de chapitres (commençant par 1). |
| l:stream:chapter_offset | ChapterInfo | (Obligatoire)<br/><br/>Décalage du chapitre (exprimé en secondes) à l’intérieur du contenu principal, à l’exception des publicités. |
| l:stream:chapter_length | ChapterInfo | (Obligatoire)<br/><br/>Durée du chapitre (exprimée en secondes). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Facultatif)<br/><br/>Métadonnées personnalisées du chapitre. |

## Événement de fin de session

| Nom | Source de données | Description   |
| ---  | --- | --- |
| s:event:type=end | SDK Media | (Obligatoire)<br/><br/> Le `end``close` |

