---
title: Mappage des paramètres Media Analytics pour Adobe Experience Platform et Customer Journey Analytics
description: Mappage du chemin d’accès du champ XDM pour les paramètres Media Analytics utilisés avec le connecteur Source Analytics et Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 1325
ht-degree: 20%

---

# Mappage des paramètres Media Analytics pour Adobe Experience Platform et Customer Journey Analytics

Ce document fournit une liste complète de tous les paramètres Media Analytics utilisés dans Adobe Experience Platform et Customer Journey Analytics. Il est destiné à prendre en charge l’intégration des données importées d’Adobe Analytics vers Platform via le [ Connecteur Source Analytics ](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/analytics) ou le [ Connecteur Source Analytics pour les classifications ](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/classifications), en mappant chaque paramètre à son chemin d’accès au champ XDM correspondant.

>[!NOTE]
>
>Cette référence s’applique aux organisations qui utilisent le connecteur source [Analytics](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/analytics) pour importer des données de médias en flux continu d’Adobe Analytics dans Adobe Experience Platform en vue de les utiliser avec la création de rapports Customer Journey Analytics ou d’autres services Platform. Ces modifications n’ont aucune incidence sur Adobe Analytics en tant qu’application autonome, y compris la collecte, le traitement et le compte rendu des performances des données.

## Variables réservées à Media Analytics

Depuis octobre 2025, le chemin d’accès au champ XDM `media.mediaTimed` est entièrement obsolète et remplacé par `mediaReporting`. Les données ingérées après octobre 2025 ne comprennent que des champs `mediaReporting`. Les données antérieures restent disponibles sous le chemin du champ hérité, comme indiqué dans les tableaux ci-dessous sous **Champ XDM hérité**.

### Comportement des appels KeepAlive

Grâce au connecteur source Analytics pour les médias en flux continu, les appels de maintien en vie d’Adobe Analytics sont désormais ingérés dans Adobe Experience Platform. Cela peut avoir une incidence sur les rapports Customer Journey Analytics :

* **Nombre de sessions** : les appels KeepAlive permettent de maintenir les sessions utilisateur actives même sans interactions multimédia directes. Ces appels sont générés toutes les 20 minutes après le dernier événement par lecture multimédia. Pour garantir un suivi de session optimal, configurez l’expiration de visite sur 30 minutes dans la vue de données.

* **Nombre d’événements** : les appels KeepAlive sont désormais comptabilisés dans la mesure Événements Customer Journey Analytics . Pour les exclure, créez un filtre qui exclut les événements avec le type d’événement `media.keepalive`.

## Paramètres de streaming multimédia

| Nom du champ | Champ XDM hérité | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Type de flux]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | Dimension | [[!UICONTROL Type de flux]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL Identifiant du contenu]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | Dimension | [[!UICONTROL Identifiant du contenu]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL Longueur du contenu]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | Dimension | [[!UICONTROL Longueur du contenu]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL  Type de contenu ]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | Dimension | [[!UICONTROL  Type de contenu ]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL ID de session multimédia]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | Dimension | [[!UICONTROL ID de session multimédia]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL Nom du lecteur de contenu]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | Dimension | [[!UICONTROL Nom du lecteur de contenu]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL  Canal de contenu ]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | Dimension | [[!UICONTROL  Canal de contenu ]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL Segment de contenu]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | Dimension | [[!UICONTROL Segment de contenu]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL Nom du contenu]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | Dimension | [[!UICONTROL Nom du contenu]](/help/reporting/dimensions/content-name.md) | |
| Chemin de la vidéo | *Non utilisé dans AEP/CJA* | | | | Propriété spécifique à Adobe Analytics |
| [[!UICONTROL Afficher]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | Dimension | [[!UICONTROL Afficher]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL  Saison ]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | Dimension | [[!UICONTROL  Saison ]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL Épisode]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | Dimension | [[!UICONTROL Épisode]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL Genre]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | Dimension | non pris en charge | Utiliser le champ `mediaReporting` |
| [[!UICONTROL Réseau]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | Dimension | [[!UICONTROL Réseau]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL Afficher le type]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | Dimension | [[!UICONTROL Afficher le type]](/help/reporting/dimensions/show-type.md) | |
| [](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | Dimension | [](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL Autorisé]](/help/reporting/metrics/authorized.md) | Non pris en charge | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | Dimension | [[!UICONTROL Autorisé]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL Jour]](/help/reporting/dimensions/day-part.md) | Non pris en charge | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | Dimension | [[!UICONTROL Jour]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL Type de flux multimédia]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | Dimension | [[!UICONTROL Type de flux multimédia]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL Artiste]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | Dimension | [[!UICONTROL Artiste]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL album]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | Dimension | [[!UICONTROL album]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL Libellé]](/help/reporting/dimensions/label.md) | Non pris en charge | `xdm.mediaReporting.`<br>`sessionDetails.label` | Dimension | [[!UICONTROL Libellé]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL Auteur]](/help/reporting/dimensions/author.md) | Non pris en charge | `xdm.mediaReporting.`<br>`sessionDetails.author` | Dimension | [[!UICONTROL Auteur]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL Station]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | Dimension | [[!UICONTROL Station]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL Éditeur]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | Dimension | [[!UICONTROL Éditeur]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL démarrages du média]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | Mesure | [[!UICONTROL démarrages du média]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL Le contenu démarre]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | Mesure | [[!UICONTROL Le contenu démarre]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL Contenu terminé]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | Mesure | [[!UICONTROL Contenu terminé]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL Durée du contenu]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | Mesure | [[!UICONTROL Durée du contenu]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL Durée des médias]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | Mesure | [[!UICONTROL Durée des médias]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL Durée de lecture unique]](/help/reporting/metrics/unique-time-played.md) | Non pris en charge | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | Mesure | [[!UICONTROL Durée de lecture unique]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL Marqueur de progression de 10 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | Mesure | [[!UICONTROL Marqueur de progression de 10 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marqueur de progression de 25 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | Mesure | [[!UICONTROL Marqueur de progression de 25 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marqueur de progression de 50 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | Mesure | [[!UICONTROL Marqueur de progression de 50 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marqueur de progression de 75 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | Mesure | [[!UICONTROL Marqueur de progression de 75 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marqueur de progression de 95 %]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | Mesure | [[!UICONTROL Marqueur de progression de 95 %]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Audience moyenne par minute]](/help/reporting/metrics/average-minute-audience.md) | Non pris en charge | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | Mesure | [[!UICONTROL Audience moyenne par minute]](/help/reporting/metrics/average-minute-audience.md) | |
| Secondes depuis le dernier appel | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | Mesure | Secondes depuis le dernier appel | |
| [[!UICONTROL Flux Impactés En Pause]](/help/reporting/metrics/paused-impacted-streams.md) | Non pris en charge | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | Mesure | [[!UICONTROL Flux Impactés En Pause]](/help/reporting/metrics/paused-impacted-streams.md) | nous couvrons mediaTimed en calculant cette valeur à partir d’autres événements |
| [[!UICONTROL Événements Pause]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | Mesure | [[!UICONTROL Événements Pause]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL Durée totale de la pause]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | Mesure | [[!UICONTROL Durée totale de la pause]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL Reprise du contenu]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | Mesure | [[!UICONTROL Reprise du contenu]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL Vues de segments de contenu]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | Mesure | [[!UICONTROL Vues de segments de contenu]](/help/reporting/metrics/content-segment-views.md) | |

## Mise à jour des paramètres d’état du lecteur

| Nom du champ | Champ XDM hérité | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
| --- | --- | --- | --- | --- | --- |
| Flux affectés par les états du lecteur | Non pris en charge | `xdm.mediaReporting.`<br>`states.isSet` | Mesure | non pris en charge | utiliser le champ `mediaReporting` |
| Nombre d’états du lecteur | Non pris en charge | `xdm.mediaReporting.`<br>`states.count` | Mesure | non pris en charge | utiliser le champ `mediaReporting` |
| Durée totale des états du lecteur | Non pris en charge | `xdm.mediaReporting.`<br>`states.time` | Mesure | non pris en charge | utiliser le champ `mediaReporting` |
| Nom de l’état du lecteur | Non pris en charge | `xdm.mediaReporting.`<br>`states.name` | Dimension | non pris en charge | utiliser le champ `mediaReporting` |

## Paramètres de chapitre

| Nom du champ | Champ XDM hérité | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Chapitre]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | Dimension | [[!UICONTROL Chapitre]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL Début du chapitre]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | Mesure | [[!UICONTROL Début du chapitre]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL Chapitre terminé]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | Mesure | [[!UICONTROL Chapitre terminé]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL Durée du chapitre]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | Mesure | [[!UICONTROL Durée du chapitre]](/help/reporting/metrics/chapter-time-spent.md) | |

## Paramètres de publicité

| Nom du champ | Champ XDM hérité | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL ID de publicité]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | Dimension | [[!UICONTROL ID de publicité]](/help/reporting/dimensions/ad.md) | |
| [[!UICONTROL Position de la publicité dans la capsule]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | Dimension | [[!UICONTROL Position de la publicité dans la capsule]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL durée de l’annonce publicitaire]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | Mesure | [[!UICONTROL durée de l’annonce publicitaire]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL Nom du lecteur de publicités]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | Dimension | [[!UICONTROL Nom du lecteur de publicités]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL ID de coupure publicitaire]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | Dimension | [[!UICONTROL ID de coupure publicitaire]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL Nom de la publicité]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | Dimension | [[!UICONTROL Nom de la publicité]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL Publicitaire]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | Dimension | [[!UICONTROL Publicitaire]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL ID de campagne]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | Dimension | [[!UICONTROL ID de campagne]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL Démarrage de publicité]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | Mesure | [[!UICONTROL Démarrage de publicité]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL Fin de la publicité]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | Mesure | [[!UICONTROL Fin de la publicité]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL Temps passé sur la publicité]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | Mesure | [[!UICONTROL Temps passé sur la publicité]](/help/reporting/metrics/ad-time-spent.md) | |

## Paramètres de qualité

| Nom du champ | Champ XDM hérité | Chemin d’accès du champ XDM de création de rapports | Type de données | Champs dérivés | Notes |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Débit moyen]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | Les deux | [[!UICONTROL Débit moyen]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL Heure De Commencer]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | Les deux | [[!UICONTROL Heure De Commencer]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL Images perdues]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | Les deux | [[!UICONTROL Images perdues]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL Événements de mémoire tampon]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | Les deux | [[!UICONTROL Événements de mémoire tampon]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL Durée totale de la mémoire tampon]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | Les deux | [[!UICONTROL Durée totale de la mémoire tampon]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL Changements de débit]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | Les deux | [[!UICONTROL Changements de débit]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL Erreurs / Événements d’erreur]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | Les deux | [[!UICONTROL Erreurs / Événements d’erreur]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL ID d’erreur du lecteur SDK]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | Dimension | non pris en charge | utiliser le champ `mediaReporting` |
| [[!UICONTROL ID d’erreur externe]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | Dimension | non pris en charge | utiliser le champ `mediaReporting` |
| [[!UICONTROL Pertes avant le début]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | Mesure | [[!UICONTROL Pertes avant le début]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL Flux impactés par la mise en mémoire tampon]](/help/reporting/metrics/buffer-impacted-streams.md) | Non pris en charge | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | Mesure | [[!UICONTROL Flux impactés par la mise en mémoire tampon]](/help/reporting/metrics/buffer-impacted-streams.md) | calculé à partir d’autres événements |
| [[!UICONTROL Flux Impactés Par Le Changement De Débit]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | Non pris en charge | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | Mesure | [[!UICONTROL Flux Impactés Par Le Changement De Débit]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | calculé à partir d’autres événements |
| [[!UICONTROL Flux impactés par l’erreur]](/help/reporting/metrics/error-impacted-streams.md) | Non pris en charge | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | Mesure | [[!UICONTROL Flux impactés par l’erreur]](/help/reporting/metrics/error-impacted-streams.md) | calculé à partir d’autres événements |
| [[!UICONTROL Flux Impactés Par L’Image Perdue]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | Non pris en charge | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | Mesure | [[!UICONTROL Flux Impactés Par L’Image Perdue]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | calculé à partir d’autres événements |

## Classifications Media Analytics

Les classifications Media Analytics sont ingérées dans AEP par le biais d’un flux distinct appelé ACDC. Chaque groupe de classifications répertorié dans le tableau ci-dessous correspond à un jeu de données unique dans AEP. Dans CJA, il est nécessaire d’établir une connexion entre le jeu de données d’événement Media Analytics et chacun des jeux de données de classification.

### Connexion de jeux de données dans Customer Journey Analytics

Pour configurer la connexion dans Customer Journey Analytics :

* Accédez à l’onglet **Connexions** et sélectionnez **Créer une connexion**.
* Dans l’interface Connexions, choisissez **Ajouter des jeux de données** et recherchez le jeu de données d’événement Media Analytics (utilisé pour importer des données multimédia via ADC), ainsi que les quatre jeux de données de classification pertinents.

### Détails de la configuration

Pour chaque jeu de données de recherche (jeu de données de classification), configurez comme suit :

* **jeu de données vidéo** :
   * Clé : `_sandbox.key`
   * Clé correspondante : `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * Type de source de données : `Web Data`

* **jeu de données videoad** :
   * Clé : `_sandbox.key`
   * Clé correspondante : `Ad ID (advertising.adAssetReference._id)`
   * Type de source de données : `Web Data`

* **jeu de données videoadpod** :
   * Clé : `_sandbox.key`
   * Clé correspondante : `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * Type de source de données : `Web Data`

* **jeu de données videochapter** :
   * Clé : `_sandbox.key`
   * Clé correspondante : `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * Type de source de données : `Web Data`

### Considérations relatives aux rapports

Lorsque vous utilisez les jeux de données de classification au cours de la création de rapports, veillez à référencer les chemins d’accès aux champs spécifiques à la classification (`ACDC XDM Path`) au lieu des champs XDM Media Analytics standard.

## Tableau des classifications

| Nom de la classification (groupe) | Nom du champ | Chemin XDM ACDC |
| --- | --- | --- |
| video | Clé/ID de ressource | `xdm.<_sandbox>.key` |
| video | Durée de la vidéo | `xdm.<_sandbox>.video_length` |
| video | Nom de la vidéo | `xdm.<_sandbox>.video_name` |
| video | [[!UICONTROL ID de ressource]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| video | [[!UICONTROL Date de première diffusion]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| video | [[!UICONTROL Première date numérique]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| video | [[!UICONTROL Évaluation du contenu]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| video | [[!UICONTROL Originator]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | Clé / ID de publicité | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL durée de l’annonce publicitaire]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL Nom de la publicité]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | Clé / ID de capsule publicitaire | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL Position de la capsule]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL Nom de la capsule]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | Clé / Chapitre | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL Longueur du chapitre]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL décalage de chapitre]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL Position du chapitre]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL Nom du chapitre]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Variables personnalisées Media Analytics

Dans Adobe Analytics, les variables personnalisées sont affectées à différents événements ou eVars en fonction des règles d’implémentation définies dans chaque suite de rapports. Par conséquent, lorsque ces variables personnalisées sont importées dans Adobe Experience Platform (AEP), elles sont mappées à différents chemins XDM.

* Les événements sont stockés sous le chemin :

  `_experience.analytics.event<x>to<y>.event<number>.value`

* Les eVars sont stockées sous le chemin :

  `_experience.analytics.customDimensions.eVars.eVar<number>`

Dans les deux cas, la `<number>` correspond à l’événement spécifique ou au numéro eVar utilisé dans la configuration d’origine de la suite de rapports Adobe Analytics.

### Variables personnalisées

| Nom du champ | Chemin XDM | Type de données |
| --- | --- | --- |
| [[!UICONTROL  Indicateur de média téléchargé ]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
| Version du SDK | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| Version de Media Library | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Format de flux]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Date de première diffusion]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Première date numérique]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Federated Data]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>et<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Les deux |
| [[!UICONTROL Flux estimés]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
| [[!UICONTROL Nombre de publicités]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
| [[!UICONTROL Nombre de chapitres]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
| [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL Identifiant du site]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL URL ]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| [[!UICONTROL ID d’emplacement]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimension |
| Images par seconde | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>et<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Les deux |
| ID d’erreur du SDK Media | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
| [[!UICONTROL Blocage des flux impactés]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
| [[!UICONTROL Événements de blocage]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
| [[!UICONTROL Durée totale du blocage]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Mesure |
