---
seo-title: Détails des appels de test
title: Détails des appels de test
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: d694ced982140c1f8020c0be304492aee0495cdc

---


# Détails des appels de test{#test-call-details}

## Démarrage du lecteur multimédia {#start-the-media-player}

### Appel Démarrer Adobe Analytics (appmeasurement) {#aa-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Champs de métadonnées personnalisés**_ |
| _**`a.media.[value]`**_ | _**Champs de métadonnées standard**_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La durée des diffusions linéaires doit être définie sur la meilleure estimation pour le programme actuel.

### Métadonnées standard dans Adobe Analytics (appmeasurement) Appel start {#std-metadata-aa}

| Paramètre |  Valeur (exemple)  |
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

### Métadonnées personnalisées dans Adobe Analytics (appmeasurement) Appel start {#custom-metadata-aa}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics (pulsations) Appel Démarrer {#ma-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Champs de métadonnées personnalisés**_ |
| _**`s:meta:a.media.[value]`**_ | _**Champs de métadonnées standard**_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La position du curseur de lecture pour les diffusions linéaires au démarrage de la vidéo doit être définie sur le nombre de secondes écoulées depuis le démarrage du programme actuel, et non sur 0.

### Métadonnées standard dans Media Analytics (pulsations) Appel Démarrer {#std-metadata-ma}

| Paramètre |  Valeur (exemple)  |
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

### Métadonnées personnalisées dans Media Analytics (pulsations) Appel Démarrer {#custom-metadata-ma}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Appel de démarrage d'Adobe Analytics (pulsations) {#ma-aa-start}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Remarques :**

* Cet appel indique que le SDK multimédia a demandé qu'un appel Adobe Analytics `pev2=ms_s` soit envoyé au serveur Adobe Analytics (appmeasurement).
* Cet appel ne contient pas de métadonnées personnalisées.

## Afficher la lecture de la publicité {#view-ad-playback}

### Appel de démarrage de publicité Adobe Analytics (appmeasurement) {#aa-ad-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**True**_ |
| _**`custom.[value]`**_ | _**Champs de métadonnées**_ |
| _**`a.media.[value]`**_ | _**Champs de métadonnées standard**_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La durée de la publicité doit être définie sur -1 si elle n’est pas disponible au démarrage de la publicité.

### Standard metadata in Adobe Analytics (AppMeasurement) Ad Start call {#std-metadata-aa-ad-start}

| Paramètre |  Valeur (exemple)  |
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

### Métadonnées personnalisées dans l'appel de démarrage de publicité d'Adobe Analytics (appmeasurement) {#custom-metadata-aa-ad-start}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Appel de démarrage de publicité Media Analytics (pulsations) {#ma-ad-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Champs de métadonnées personnalisés**_ |
| _**`s:meta:a.media.[value]`**_ | _**Champs de métadonnées standard**_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La durée de la publicité doit être définie sur -1 si elle n’est pas disponible au démarrage de la publicité.

### Standard metadata in Media Analytics (heartbeats) Ad Start call {#std-metadata-ma-ad-start}

| Paramètre |  Valeur (exemple)  |
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

### Métadonnées personnalisées dans l'appel de démarrage de publicité de Media Analytics (pulsations) {#custom-metadata-ma-ad-start}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Appel de démarrage de publicité Adobe Analytics (pulsations) {#ma-aa-ad-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Appel Ad Play (pulsations) Media Analytics {#ma-ad-play-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Appel de mise en pause de Media Analytics (pulsations) {#ma-ad-pause-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Appel d'Adobe Analytics Ad Complete à Media Analytics (pulsations) {#ma-aa-ad-complete-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Lire le contenu principal {#play-main-content}

### Appel de lecture Media Analytics (pulsations) {#ma-play-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Remarques :**

* La position du curseur de lecture doit être incrémentée de 10 secondes avec chaque appel play.
* La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

## Suspendre le contenu principal {#pause-main-content}

### Media Analytics (pulsations) Appel Pause {#ma-pause-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |


