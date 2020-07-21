---
title: Migration de Milestone vers Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: aa2a230daa96b823f9963345ac4578799e59d3f5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 80%

---


# Migration de Milestone vers Media Analytics {#migrating-from-milestone-to-media-analytics}

## Aperçu {#overview}

Les concepts de base de la mesure vidéo sont les mêmes pour Milestone et Media Analytics, qui prend les événements du lecteur vidéo et les mappe aux méthodes d’analyse, tout en récupérant les métadonnées et les valeurs du lecteur et en les associant aux variables d’analyse. La solution Media Analytics est basée sur Milestone, donc de nombreuses méthodes et mesures sont identiques. Toutefois, l’approche et le code de configuration ont beaucoup changé. Il devrait être possible de mettre à jour le code des événements du lecteur afin qu’il pointe vers les nouvelles méthodes Media Analytics. Voir [Présentation du SDK](/help/sdk-implement/setup/setup-overview.md) et [Présentation du suivi](/help/sdk-implement/track-av-playback/track-core-overview.md) pour en savoir plus sur l’implémentation de Media Analytics.

Les tableaux suivants fournissent des correspondances entre la solution Milestone et la solution Media Analytics.

## Guide de migration {#migration-guide}

### Référence de variables

| Mesure Milestone | Type de variable | Mesure Media Analytics |
| --- | --- | --- |
| Contenu | eVar <br>Délai d’expiration par défaut : Visite | Contenu |
| Type de contenu | eVar <br>Délai d’expiration par défaut : page vue | Type de contenu |
| Temps passé sur le contenu | Type <br>d’événement : Compteur | Temps passé sur le contenu |
| Démarrages de vidéo | Type <br>d’événement : Compteur | Démarrages de vidéo |
| La vidéo se termine | Type <br>d’événement : Compteur | Fin de contenu |

### Variables du module média

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | S.O. | Toutes les données Media Analytics sont envoyées uniquement à l’aide de données contextuelles. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | S.O. | Les données contextuelles Media Analytics sont automatiquement renseignées dans des variables réservées. Le mappage à des eVar, des props et des événements n’est plus nécessaire dans le code de mise en œuvre. Les clients peuvent associer des données contextuelles à des variables à l’aide de règles de traitement. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | S.O. | Plus nécessaire, car le mappage se fait via des variables réservées et des règles de traitement. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | S.O. | Plus nécessaire, car le mappage se fait via des variables réservées et des règles de traitement. |

### Variables facultatives

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | S.O. | Nous ne fournissons plus de mappages de lecteur préconfigurés. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | S.O. | Nous ne fournissons plus de mappages de lecteur préconfigurés. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | S.O. | La fin du contenu ne prend en charge qu’un marqueur de progression de 100 %. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | S.O. | La fin du contenu ne prend en charge qu’un marqueur de progression de 100 %. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | S.O. | Media Analytics est défini sur 10 secondes pour le contenu et 1 seconde pour les publicités. Aucune autre option n’est disponible. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | S.O. | Media Analytics effectue toujours le suivi des marqueurs de progression à 10 %, 25 %, 50 %, 75 % et 95 %. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | S.O. | Media Analytics effectue toujours le suivi des marqueurs de progression à 10 %, 25 %, 50 %, 75 % et 95 %. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |

### Variables de suivi des publicités

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | S.O. | Media Analytics est défini sur 10 secondes pour le contenu et 1 seconde pour les publicités. Aucune autre option n’est disponible. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | S.O. | Les marqueurs de progression ne sont pas fournis par défaut pour les publicités. Utilisez des mesures calculées pour créer des marqueurs de progression des publicités. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | S.O. | Media Analytics est défini sur 1 seconde pour les publicités. Aucune autre option n’est disponible. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |

### Méthodes du module média

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName - (Required) <br> The name of the video as you want it to appear in video reports. | `mediaName` | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength - (Required) <br> The length of the video in seconds. | `mediaLength` | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName - (Required) <br> The name of the media player used to view the video, as you want it to appear in video reports. | `mediaPlayerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name - (Required) <br> The name or ID of the ad. | `name` | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length - (Required) <br> The length of the ad. | `length` | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName - (Required) <br> The name of the media player used to view the ad. | `playerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName <br> The name or ID of the primary content where the ad is embedded. | `parentName` | S.O. | Hérité automatiquement |
| parentPod <br> The position in the primary content the ad was played. | `parentPod` | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition <br> The position within the pod where the ad is played. | `parentPodPosition` | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM <br> The CPM or encrypted CPM (prefixed with a &quot;~&quot;) that applies to this playback. | `CPM` | S.O. | Non disponible par défaut dans Media Analytics. |
| Media.click | `s.Media.click(` <br> `  name,` <br> `  offset)` | S.O. | Utilisez un appel d’analyse de lien personnalisé pour effectuer le suivi des clics. |
| Media.close | `s.Media.close(` <br> `  mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | trackPause<br> ou <br>trackEvent | `trackPause()` <br> ou `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> ou <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilisez des métadonnées personnalisées ou standard pour définir des variables supplémentaires. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | S.O. | La fréquence des appels de suivi est définie automatiquement. |

