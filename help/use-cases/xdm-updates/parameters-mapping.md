---
title: Migration des audiences vers le nouveau type de données Adobe Analytics for Streaming Media
description: Découvrez comment migrer des audiences vers le nouveau type de données Adobe Analytics for Streaming Media
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
source-git-commit: 61e5279e6d53b18955424e76d05d440b83dae07e
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 47%

---

# Mappage des paramètres Media Analytics pour Adobe Experience Platform et Customer Journey Analytics

Ce document fournit une liste complète de tous les paramètres Media Analytics utilisés dans Adobe Experience Platform et Customer Journey Analytics. Il est destiné à prendre en charge l’intégration des données importées d’Adobe Analytics vers Platform via le [ Connecteur Source Analytics ](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/analytics) ou le [ Connecteur Source Analytics pour les classifications ](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/classifications), en mappant chaque paramètre à son chemin d’accès au champ XDM correspondant.

## Variables réservées à Media Analytics

Pour toutes les variables réservées Media Analytics, les données ingérées depuis Adobe Analytics dans AEP jusqu’en mai 2025 (inclus) se trouvent sous le « Chemin d’accès actuel au champ XDM » signalé dans les tableaux ci-dessous.

Comme les équipes Media Analytics et ADC travaillent actuellement sur une migration complète vers le « Chemin du champ XDM de création de rapports », une communication officielle sera partagée une fois cette migration terminée et le « Chemin du champ XDM de création de rapports » disponible.

## Paramètres de streaming multimédia

| Nom du champ | Chemin d’accès au champ XDM actuel (obsolète) | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
|--------------------|---------------------------------------------------------------------------|---------------------------------------------------|-----------|-------------------|-----------------------------------------------------------------------|
| Type de diffusion | media.mediaTimed.primaryAssetReference.streamType | mediaReporting.sessionDetails.streamType | Dimension | Type de diffusion |                                                                       |
| Identifiant de contenu | media.mediaTimed.primaryAssetReference._id | mediaReporting.sessionDetails.name | Dimension | Identifiant de contenu |                                                                       |
| Longueur du contenu | media.mediaTimed.primaryAssetReference._xmpDM.duration | mediaReporting.sessionDetails.length | Dimension | Longueur du contenu |                                                                       |
| Type de contenu | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | mediaReporting.sessionDetails.contentType | Dimension | Type de contenu |                                                                       |
| ID de session multimédia | media.mediaTimed.primaryAssetViewDetails._id | mediaReporting.sessionDetails.ID | Dimension | ID de session multimédia |                                                                       |
| Nom du lecteur de contenu | media.mediaTimed.primaryAssetViewDetails.playerName | mediaReporting.sessionDetails.playerName | Dimension | Nom du lecteur de contenu |                                                                       |
| Canal de contenu | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | mediaReporting.sessionDetails.channel | Dimension | Canal de contenu |                                                                       |
| Segment de contenu | media.mediaTimed.primaryAssetViewDetails.videoSegment | mediaReporting.sessionDetails.segment | Dimension | Segment de contenu |                                                                       |
| Nom du contenu | media.mediaTimed.primaryAssetReference._dc.title | mediaReporting.sessionDetails.friendlyName | Dimension | Nom du contenu |                                                                       |
| Chemin de la vidéo | *Non utilisé dans AEP/CJA* |                                                   |           |                   | Propriété spécifique à Adobe Analytics |
| Programme | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | mediaReporting.sessionDetails.show | Dimension | Programme |                                                                       |
| Saison | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | mediaReporting.sessionDetails.season | Dimension | Saison |                                                                       |
| Épisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | mediaReporting.sessionDetails.episode | Dimension | Épisode |                                                                       |
| Genre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | mediaReporting.sessionDetails.genreList | Dimension | non pris en charge | Utiliser le champ mediaReporting |
| Réseau | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | mediaReporting.sessionDetails.network | Dimension | Réseau |                                                                       |
| Type de programme | media.mediaTimed.primaryAssetReference.showType | mediaReporting.sessionDetails.showType | Dimension | Type de programme |                                                                       |
| MVPD | media.mediaTimed.idp | mediaReporting.sessionDetails.mvpd | Dimension | MVPD |                                                                       |
| Autorisé | Non pris en charge | mediaReporting.sessionDetails.authorized | Dimension | Autorisé |                                                                       |
| Partie de la journée | Non pris en charge | mediaReporting.sessionDetails.dayPart | Dimension | Partie de la journée |                                                                       |
| Type de flux multimédia | media.mediaTimed.primaryAssetViewDetails.sourceFeed | mediaReporting.sessionDetails.feed | Dimension | Type de flux multimédia |                                                                       |
| Artiste | media.mediaTimed.primaryAssetReference._xmpDM.artist | mediaReporting.sessionDetails.artist | Dimension | Artiste |                                                                       |
| Album | media.mediaTimed.primaryAssetReference._xmpDM.album | mediaReporting.sessionDetails.album | Dimension | Album |                                                                       |
| Étiquette | Non pris en charge | mediaReporting.sessionDetails.label | Dimension | Étiquette |                                                                       |
| Auteur | Non pris en charge | mediaReporting.sessionDetails.author | Dimension | Auteur |                                                                       |
| Station | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TRSN | mediaReporting.sessionDetails.station | Dimension | Station |                                                                       |
| Éditeur | media.mediaTimed.primaryAssetReference._id3.Audio._id3.TPUB | mediaReporting.sessionDetails.publisher | Dimension | Éditeur |                                                                       |
| Démarrage du contenu multimédia | media.mediaTimed.impressions.value | mediaReporting.sessionDetails.isViewed | Mesure | Démarrage du contenu multimédia |                                                                       |
| Démarrages de contenu | media.mediaTimed.starts.value | mediaReporting.sessionDetails.isPlayed | Mesure | Démarrages de contenu |                                                                       |
| Fin de contenu | media.mediaTimed.completes.value | mediaReporting.sessionDetails.isCompleted | Mesure | Fin de contenu |                                                                       |
| Temps passé sur le contenu | media.mediaTimed.timePlayed.value | mediaReporting.sessionDetails.timePlayed | Mesure | Temps passé sur le contenu |                                                                       |
| Passé sur le média | media.mediaTimed.totalTimePlayed.value | mediaReporting.sessionDetails.totalTimePlayed | Mesure | Passé sur le média |                                                                       |
| Durée de lecture unique | Non pris en charge | mediaReporting.sessionDetails.uniqueTimePlayed | Mesure | Durée de lecture unique |                                                                       |
| Marqueur de progression de 10% | media.mediaTimed.progress10.value | mediaReporting.sessionDetails.hasProgress10 | Mesure | Marqueur de progression de 10% |                                                                       |
| Marqueur de progression de 25% | media.mediaTimed.progress25.value | mediaReporting.sessionDetails.hasProgress25 | Mesure | Marqueur de progression de 25% |                                                                       |
| Marqueur de progression de 50 % | media.mediaTimed.progress50.value | mediaReporting.sessionDetails.hasProgress50 | Mesure | Marqueur de progression de 50 % |                                                                       |
| Marqueur de progression de 75% | media.mediaTimed.progress75.value | mediaReporting.sessionDetails.hasProgress75 | Mesure | Marqueur de progression de 75% |                                                                       |
| Marqueur de progression de 95% | media.mediaTimed.progress95.value | mediaReporting.sessionDetails.hasProgress95 | Mesure | Marqueur de progression de 95% |                                                                       |
| Audience moyenne par minute | Non pris en charge | mediaReporting.sessionDetails.averageMinuteAudience | Mesure | Audience moyenne par minute |                                                                  |
| Secondes depuis le dernier appel | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | mediaReporting.sessionDetails.secondsSinceLastCall | Mesure | Secondes depuis le dernier appel |                                                              |
| Flux touchés en pause | Non pris en charge | mediaReporting.sessionDetails.hasPauseImpactedStreams | Mesure | Flux touchés en pause | nous couvrons mediaTimed en calculant cette valeur à partir d’autres événements |
| Événements de mise en pause | media.mediaTimed.pauses.value | mediaReporting.sessionDetails.pauseCount | Mesure | Événements de mise en pause |                                                                       |
| Durée totale de pause | media.mediaTimed.pauseTime.value | mediaReporting.sessionDetails.pauseTime | Mesure | Durée totale de pause |                                                                       |
| Le contenu reprend | media.mediaTimed.resumes.value | mediaReporting.sessionDetails.hasResume | Mesure | Le contenu reprend |                                                                       |
| Affichages de segments de contenu | media.mediaTimed.mediaSegmentViews.value | mediaReporting.sessionDetails.hasSegmentView | Mesure | Affichages de segments de contenu |                                                                     |

{style="table-layout:auto"}

## Mise à jour des paramètres d’état du lecteur

| Nom du champ | Chemin d’accès au champ XDM actuel (obsolète) | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
|----------------------------|-------------------------------------|----------------------------------|-----------|----------------|--------------------------------------|
| Flux affectés par les états du lecteur | Non pris en charge | mediaReporting.states.isSet | Mesure | non pris en charge | utiliser le champ mediaReporting |
| Nombre d’états du lecteur | Non pris en charge | mediaReporting.states.count | Mesure | non pris en charge | utiliser le champ mediaReporting |
| Durée totale des états du lecteur | Non pris en charge | mediaReporting.states.time | Mesure | non pris en charge | utiliser le champ mediaReporting |
| Nom de l’état du lecteur | Non pris en charge | mediaReporting.states.name | Dimension | non pris en charge | utiliser le champ mediaReporting |

{style="table-layout:auto"}

## Paramètres de chapitre 

| Nom du champ | Chemin d’accès au champ XDM actuel (obsolète) | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
|------------------|--------------------------------------------------------------|-------------------------------------------|-----------|----------------|-----------|
| Chapitre | media.mediaTimed.mediaChapter.chapterAssetReference._id | mediaReporting.chapterDetails.ID | Dimension | Chapitre |           |
| Début du chapitre | media.mediaTimed.mediaChapter.impressions.value | mediaReporting.chapterDetails.isStarted | Mesure | Début du chapitre |           |
| Chapitre terminé | media.mediaTimed.mediaChapter.completes.value | mediaReporting.chapterDetails.isCompleted | Mesure | Chapitre terminé |          |
| Passé sur le chapitre | media.mediaTimed.mediaChapter.timePlayed.value | mediaReporting.chapterDetails.timePlayed | Mesure | Passé sur le chapitre |        |

{style="table-layout:auto"}

## Paramètres de publicité 

| Nom du champ | Chemin d’accès au champ XDM actuel (obsolète) | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
|------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Identifiant de publicité | advertising.adAssetReference._id | mediaReporting.advertisingDetails.name | Dimension | Identifiant de publicité |           |
| Position de la publicité dans la capsule | advertising.adAssetViewDetails.index | mediaReporting.advertisingDetails.podPosition | Dimension | Position de la publicité dans la capsule |     |
| Longueur de la publicité | advertising.adAssetReference._xmpDM.duration | mediaReporting.advertisingDetails.length | Mesure | Longueur de la publicité |           |
| Nom du lecteur de publicités | advertising.adAssetViewDetails.playerName | mediaReporting.advertisingDetails.playerName | Dimension | Nom du lecteur de publicités |           |
| ID de coupure de publicité | advertising.adAssetViewDetails.adBreak._id | mediaReporting.advertisingPodDetails.ID | Dimension | ID de coupure de publicité |           |
| Nom de la publicité | advertising.adAssetReference._dc.title | mediaReporting.advertisingDetails.friendlyName | Dimension | Nom de la publicité |           |
| Annonceur | advertising.adAssetReference.advertiser | mediaReporting.advertisingDetails.advertiser | Dimension | Annonceur |           |
| ID de campagne | advertising.adAssetReference.campaign | mediaReporting.advertisingDetails.campaignID | Dimension | ID de campagne |           |
| Démarrage de publicité | advertising.impressions.value | mediaReporting.advertisingDetails.isStarted | Mesure | Démarrage de publicité |           |
| Publicité terminée | advertising.completes.value | mediaReporting.advertisingDetails.isCompleted | Mesure | Publicité terminée |           |
| passé sur la publicité | advertising.timePlayed.value | mediaReporting.advertisingDetails.timePlayed | Mesure | passé sur la publicité |           |

{style="table-layout:auto"}

## Paramètres de qualité 

| Nom du champ | Chemin d’accès au champ XDM actuel (obsolète) | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
|------------------------|--------------------------------------------------------------|------------------------------------------------|-----------|----------------|-----------|
| Débit moyen | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage.value | mediaReporting.qoeDataDetails.bitrateAverage | Les variables | Débit moyen |           |
| Temps jusqu’au début | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart.value | mediaReporting.qoeDataDetails.timeToStart | Les variables | Temps jusqu’au début |           |
| Perte d’images | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames.value | mediaReporting.qoeDataDetails.droppedFrames | Les variables | Perte d’images |           |
| Événements de mémoire tampon | media.mediaTimed.primaryAssetViewDetails.qoe.buffers.value | mediaReporting.qoeDataDetails.bufferCount | Les variables | Événements de mémoire tampon |           |
| Durée totale de la mémoire tampon | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime.value | mediaReporting.qoeDataDetails.bufferTime | Les variables | Durée totale de la mémoire tampon |     |
| Changements de débit | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges.value | mediaReporting.qoeDataDetails.bitrateChangeCount | Les variables | Changements de débit |         |
| Erreurs / Événements d’erreur | media.mediaTimed.primaryAssetViewDetails.qoe.errors.value | mediaReporting.qoeDataDetails.errorCount | Les variables | Erreurs / Événements d’erreur |  |
| ID d’erreur du SDK du lecteur | media.mediaTimed.primaryAssetViewDetails.qoe.playerSdkErrors | mediaReporting.qoeDataDetails.playerSdkErrors | Dimension | non pris en charge | utiliser le champ mediaReporting |
| ID d’erreur externes | media.mediaTimed.primaryAssetViewDetails.qoe.externalSdkErrors | mediaReporting.qoeDataDetails.externalErrors | Dimension | non pris en charge | utiliser le champ mediaReporting |
| Pertes avant le début | media.mediaTimed.dropBeforeStarts.value | mediaReporting.qoeDataDetails.isDroppedBeforeStart | Mesure | Pertes avant le début |     |
| Flux touchés par la mémoire tampon | Non pris en charge | mediaReporting.qoeDataDetails.hasBufferImpactedStreams | Mesure | Flux touchés par la mémoire tampon | calculé à partir d’autres événements |
| Flux touchés par les changements de débit | Non pris en charge | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams | Mesure | Flux touchés par les changements de débit | calculé à partir d’autres événements |
| Flux touchés par les erreurs | Non pris en charge | mediaReporting.qoeDataDetails.hasErrorImpactedStreams | Mesure | Flux touchés par les erreurs | calculé à partir d’autres événements |
| Flux touchés par la perte d’images | Non pris en charge | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams | Mesure | Flux touchés par la perte d’images | calculé à partir d’autres événements |

{style="table-layout:auto"}

## Classifications Media Analytics

Les classifications Media Analytics sont ingérées dans AEP par le biais d’un flux distinct appelé ACDC. Chaque groupe de classifications répertorié dans le tableau ci-dessous correspond à un jeu de données unique dans AEP. Dans CJA, il est nécessaire d’établir une connexion entre le jeu de données d’événement Media Analytics et chacun des jeux de données de classification.

### Connexion de jeux de données dans Customer Journey Analytics

Pour configurer la connexion dans Customer Journey Analytics :

- Accédez à l’onglet **Connexions** et sélectionnez **Créer une connexion**.
- Dans l’interface Connexions, choisissez **Ajouter des jeux de données** et recherchez le jeu de données d’événement Media Analytics (utilisé pour importer des données multimédia via ADC), ainsi que les quatre jeux de données de classification pertinents.

### Détails de la configuration

Pour chaque jeu de données de recherche (jeu de données de classification), configurez comme suit :

- **jeu de données vidéo** :
   - Clé : `_sandbox.key`
   - Clé correspondante : `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   - Type de source de données : `Web Data`

- **jeu de données videoad** :
   - Clé : `_sandbox.key`
   - Clé correspondante : `Ad ID (advertising.adAssetReference._id)`
   - Type de source de données : `Web Data`

- **jeu de données videoadpod** :
   - Clé : `_sandbox.key`
   - Clé correspondante : `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   - Type de source de données : `Web Data`

- **jeu de données videochapter** :
   - Clé : `_sandbox.key`
   - Clé correspondante : `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   - Type de source de données : `Web Data`

### Considérations relatives aux rapports

Lorsque vous utilisez les jeux de données de classification au cours de la création de rapports, veillez à référencer les chemins d’accès aux champs spécifiques à la classification (`ACDC XDM Path`) au lieu des champs XDM Media Analytics standard.

## Tableau des classifications

| Nom de la classification (groupe) | Nom du champ | Chemin XDM ACDC |
|------------|----------|-------------|
| video | Clé/ID de ressource | `<_sandbox>.key` |
| video | Durée de la vidéo | `<_sandbox>.video_length` |
| video | Nom de la vidéo | `<_sandbox>.video_name` |
| video | ID de ressource | `<_sandbox>.asset_id` |
| video | Date de première diffusion | `<_sandbox>.first_air_date` |
| video | Date de première distribution numérique | `<_sandbox>.first_digital_date` |
| video | Évaluation du contenu | `<_sandbox>.content_rating` |
| video | Créateur | `<_sandbox>.originator` |
| videoad | Clé / ID de publicité | `<_sandbox>.key` |
| videoad | Longueur de la publicité | `<_sandbox>.ad_length` |
| videoad | Nom de la publicité | `<_sandbox>.ad_name` |
| videoad | ID d’élément créatif | `<_sandbox>.creative_id` |
| videoadpod | Clé / ID de capsule publicitaire | `<_sandbox>.key` |
| videoadpod | Position de la capsule | `<_sandbox>.pod_position` |
| videoadpod | Nom de la capsule | `<_sandbox>.pod_name` |
| videochapter | Clé / Chapitre | `<_sandbox>.key` |
| videochapter | Durée du chapitre | `<_sandbox>.chapter_length` |
| videochapter | Décalage de chapitre | `<_sandbox>.chapter_offset` |
| videochapter | Position du chapitre | `<_sandbox>.chapter_position` |
| videochapter | Nom du chapitre | `<_sandbox>.chapter_name` |

{style="table-layout:auto"}

## Variables personnalisées Media Analytics

Dans Adobe Analytics, les variables personnalisées sont affectées à différents événements ou eVars en fonction des règles d’implémentation définies dans chaque suite de rapports. Par conséquent, lorsque ces variables personnalisées sont importées dans Adobe Experience Platform (AEP), elles sont mappées à différents chemins XDM.

- Les événements sont stockés sous le chemin :

  `_experience.analytics.event<x>to<y>.event<number>.value`

- Les eVars sont stockées sous le chemin :

  `_experience.analytics.customDimensions.eVars.eVar<number>`

Dans les deux cas, la `<number>` correspond à l’événement spécifique ou au numéro eVar utilisé dans la configuration d’origine de la suite de rapports Adobe Analytics.

### Variables personnalisées

| Nom du champ | Chemin XDM | Type de données |
|-------------|-------------|-----------|
| Indicateur de média téléchargé | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |
| Version du SDK | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Version de VHL | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Format de diffusion | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Date de première diffusion | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Date de première distribution numérique | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Données fédérées | `_experience.analytics.customDimensions.eVars.eVar<number>` et `_experience.analytics.event<x>to<y>.event<number>.value` | Les variables |
| Diffusions estimées | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |
| Nombre de publicités | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |
| Nombre de chapitres | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |
| ID d’élément créatif | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| ID du site | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| URL de l’élément créatif | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Identifiant de référencement | `_experience.analytics.customDimensions.eVars.eVar<number>` | Dimension |
| Images par seconde | `_experience.analytics.customDimensions.eVars.eVar<number>` et `_experience.analytics.event<x>to<y>.event<number>.value` | Les variables |
| ID d’erreur du SDK Media | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |
| Flux touchés par un blocage | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |
| Événements de blocage | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |
| Durée totale de blocage | `_experience.analytics.event<x>to<y>.event<number>.value` | Mesure |

{style="table-layout:auto"}
