---
seo-title: Détails des appels de test
title: Détails des appels de test
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: 400c7ada4ab269017c3c2948c9056b4c1031d793

---


# Détails des appels de test{#test-call-details}

## Démarrer le lecteur vidéo {#section_qts_xff_f2b}

### Appel de démarrage de Media Analytics

| Paramètre | Valeur (exemple)   |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | true |
| `a.contentType` | vod |
| `custom.[value]` | Champs de métadonnées personnalisés |
| `a.media.[value]` | Champs de métadonnées standard |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La durée des diffusions linéaires doit être définie sur la meilleure estimation pour le programme actuel.

### Métadonnées standard dans l'appel start de Media Analytics

| Paramètre | Valeur (exemple)   |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Appel de démarrage de Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:name` | Episode Title |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | Champs de métadonnées personnalisés |
| `s:meta:a.media.[value]` | Champs de métadonnées standard |

### Métadonnées vidéo dans l'appel start Media Analytics

| Paramètre | Valeur (exemple)   |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La position du curseur de lecture pour les diffusions linéaires au démarrage de la vidéo doit être définie sur le nombre de secondes écoulées depuis le démarrage du programme actuel, et non sur 0.

### Appel de démarrage de l’analyse Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:name` | Episode Title |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |

### Métadonnées vidéo dans l’appel de démarrage de Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Métadonnées standard dans l’appel de démarrage de Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:meta:a.media.show` | Programme |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

**Remarques :**

* Cet appel indique que la bibliothèque Heartbeat a demandé qu’un appel d’analyse pev2=ms_s soit envoyé au serveur d’analyse.
* Cet appel ne contient pas de métadonnées personnalisées.

## Afficher la lecture de la publicité {#section_wz3_yff_f2b}

### Appel de démarrage de publicité Media Analytics

| Paramètre | Valeur (exemple)   |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| `a.media.ad.view` | True |
| `custom.[value]` | Champs de métadonnées |
| `a.media.[value]` | Champs de métadonnées standard |

**Remarque :** D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.

### Appel de démarrage de la publicité Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `l:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | Champs de métadonnées personnalisés |
| `s:meta:a.media.[value]` | Champs de métadonnées standard |

### Métadonnées vidéo dans l'appel de démarrage de publicité Media Analytics

| Paramètre | Valeur (exemple)   |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Métadonnées standard dans l'appel de démarrage de publicité Media Analytics

| Paramètre | Valeur (exemple)   |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La durée de la publicité doit être définie sur -1 si elle n’est pas disponible au démarrage de la publicité.

### Appel de démarrage de la publicité de l’analyse Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

### Métadonnées vidéo dans l’appel de démarrage de la publicité Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Métadonnées standard dans l’appel de démarrage de la publicité Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:meta:a.media.show` | Programme |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La durée de la publicité doit être définie sur -1 si elle n’est pas disponible au démarrage de la publicité.

### Appel de fin de la publicité Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:event:type` | complete (terminé) |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

### Appel de lecture de la publicité Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `l:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `l:stream:type` | vod |
| `s:asset:type` | ad |

## Lire le contenu principal {#section_u1l_1gf_f2b}

### Appel de lecture de Heartbeat

| Paramètre | Valeur (exemple)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `l:asset:name` | Episode Title |
| `l:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `l:stream:type` | vod |
| `s:asset:type` | main |

**Remarques :**

* La position du curseur de lecteur doit augmenter de 10 à chaque appel de lecture.
* La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

