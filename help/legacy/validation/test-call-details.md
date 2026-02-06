---
title: Détails des appels de test
description: Explorez les appels que vous devez effectuer pour valider votre implémentation.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 80%

---

# Détails des appels de test{#test-call-details}

## Démarrage du lecteur multimédia {#start-the-media-player}

### Appel de démarrage d’Adobe Analytics (AppMeasurement) {#aa-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _&#x200B;**`a.media.name`**&#x200B;_ | _&#x200B;**123456**&#x200B;_ |
| _&#x200B;**`a.media.length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `a.media.playerName` | HTML5 |
| _&#x200B;**`a.media.view`**&#x200B;_ | _&#x200B;**true**&#x200B;_ |
| `a.contentType` | vod |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées personnalisés**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées standard**&#x200B;_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La longueur des flux linéaires doit être définie sur la meilleure estimation pour l&#39;affichage actuel.

### Métadonnées standard dans l’appel de démarrage d’Adobe Analytics (AppMeasurement) {#std-metadata-aa}

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

### Métadonnées personnalisées dans l’appel de démarrage d’Adobe Analytics (AppMeasurement) {#custom-metadata-aa}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `custom.metadataA` | valeur |
| `custom.metadataB` | valeur |

### Appel de démarrage de Media Analytics (pulsations) {#ma-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:event:type` | start |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**0**&#x200B;_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées personnalisés**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées standard**&#x200B;_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La position de la tête de lecture pour les flux linéaires au début de la vidéo doit être définie sur les secondes écoulées depuis le début de l’émission actuelle, et non sur 0.

### Métadonnées standard dans l’appel de démarrage de Media Analytics (pulsations) {#std-metadata-ma}

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

### Métadonnées personnalisées dans l’appel de démarrage de Media Analytics (pulsations) {#custom-metadata-ma}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:meta:custom.metadata` | valeur |
| `s:meta:custom.metadata` | valeur |

### Appel de démarrage Adobe Analytics de Media Analytics (pulsations) {#ma-aa-start}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Remarques :**

* Cet appel indique que le SDK Media a demandé qu’un `pev2=ms_s` appel Adobe Analytics soit envoyé au serveur Adobe Analytics (AppMeasurement).
* Cet appel ne contient pas de métadonnées personnalisées.

## Afficher la lecture de la publicité {#view-ad-playback}

### Appel de démarrage de la publicité d’Adobe Analytics (AppMeasurement) {#aa-ad-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`pev2`**&#x200B;_ | _&#x200B;**msa_s**&#x200B;_ |
| `a.media.name` | 123456 |
| _&#x200B;**`a.media.ad.name`**&#x200B;_ | _&#x200B;**9378**&#x200B;_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _&#x200B;**`a.media.ad.length`**&#x200B;_ | _&#x200B;**15**&#x200B;_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _&#x200B;**`a.media.ad.view`**&#x200B;_ | _&#x200B;**True**&#x200B;_ |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées standard**&#x200B;_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La longueur de l’annonce publicitaire peut être définie sur -1 si elle n’est pas disponible au démarrage de l’annonce.

### Métadonnées standard dans l’appel de démarrage de la publicité d’Adobe Analytics (AppMeasurement) {#std-metadata-aa-ad-start}

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

### Métadonnées personnalisées dans l’appel de démarrage de la publicité d’Adobe Analytics (AppMeasurement) {#custom-metadata-aa-ad-start}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `custom.metadata` | valeur |
| `custom.metadata` | valeur |

### Appel de démarrage de la publicité de Media Analytics (pulsations) {#ma-ad-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _&#x200B;**`l:asset:length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées personnalisés**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Champs de métadonnées standard**&#x200B;_ |

**Remarques :**

* D’autres variables de données contextuelles doivent être présentes et contenir des métadonnées. Voir les détails des métadonnées ci-dessous.
* La longueur de l’annonce publicitaire peut être définie sur -1 si elle n’est pas disponible au démarrage de l’annonce.

### Métadonnées standard dans l’appel de démarrage de la publicité de Media Analytics (pulsations) {#std-metadata-ma-ad-start}

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

### Métadonnées personnalisées dans l’appel de démarrage de la publicité de Media Analytics (pulsations) {#custom-metadata-ma-ad-start}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:meta:custom.metadata` | valeur |
| `s:meta:custom.metadata` | valeur |

### Appel de démarrage de la publicité d’Adobe Analytics de Media Analytics (pulsations) {#ma-aa-ad-start-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_ad_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | publicité |

### Appel de démarrage de la publicité de Media Analytics (pulsations) {#ma-ad-play-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**play**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Appel de pause de la publicité de Media Analytics (pulsations) {#ma-ad-pause-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

### Appel de fin de la publicité d’Adobe Analytics (pulsations) de Media Analytics {#ma-aa-ad-complete-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**complete**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**ad**&#x200B;_ |

## Lire le contenu principal {#play-main-content}

### Appel de lecture de Media Analytics (pulsations) {#ma-play-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| `s:event:type` | play |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| _&#x200B;**`l:event:duration`**&#x200B;_ | _&#x200B;**10189**&#x200B;_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Remarques :**

* La position du curseur de lecteur doit augmenter de 10 secondes à chaque appel de lecture.
* La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

## Pause du contenu principal {#pause-main-content}

### Appel de pause de Media Analytics (pulsations) {#ma-pause-call}

| Paramètre |  Valeur (exemple)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
