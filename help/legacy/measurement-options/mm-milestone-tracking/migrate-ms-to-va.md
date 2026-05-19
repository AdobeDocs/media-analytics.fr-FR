---
title: Découvrez comment migrer de Milestone vers Media Analytics
description: Découvrez comment modifier les variables Milestone en mesures Media Analytics et les méthodes du module Milestone en syntaxe Media Analytics.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ARM-6kkgoa8-xsbZ-Ut-pei0-ZuTX6LgFX5FoRRV0d4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
  - id: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 709
ht-degree: 96%

---

# Migration de Milestone vers Media Analytics {#migrating-from-milestone-to-media-analytics}

## Aperçu {#overview}

Les concepts de base de la mesure vidéo sont les mêmes pour Milestone et Media Analytics, qui prend les événements du lecteur vidéo et les mappe aux méthodes d’analyse, tout en récupérant les métadonnées et les valeurs du lecteur et en les associant aux variables d’analyse. La solution Media Analytics est basée sur Milestone, donc de nombreuses méthodes et mesures sont identiques. Toutefois, l’approche et le code de configuration ont beaucoup changé. Il devrait être possible de mettre à jour le code des événements du lecteur afin qu’il pointe vers les nouvelles méthodes Media Analytics. Voir [Présentation du SDK](/help/legacy/setup/legacy-setup-overview.md) et [Présentation du suivi](/help/use-cases/track-av-playback/track-core-overview.md) pour en savoir plus sur l’implémentation de Media Analytics.

Les tableaux suivants fournissent des correspondances entre la solution Milestone et la solution Media Analytics.

## Guide de migration {#migration-guide}

### Référence de variables

| Mesure Milestone | Type de variable | Mesure Media Analytics |
| --- | --- | --- |
| Contenu | eVar <br>Délai d’expiration par défaut : Visite | Contenu |
| Type de contenu | eVar <br>Délai d’expiration par défaut : page vue | Type de contenu |
| Temps passé sur le contenu | Type <br> d’événement : Compteur | Temps passé sur le contenu |
| Démarrages de vidéo | Type <br> d’événement : Compteur | Démarrages de vidéo |
| La vidéo se termine | Type <br> d’événement : Compteur | Fin de contenu |


### Variables du module média

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | S.O. | Toutes les données Media Analytics sont envoyées uniquement à l’aide de données contextuelles. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | S.O. | Les données contextuelles Media Analytics sont automatiquement renseignées dans des variables réservées. Le mappage à des eVar, des props et des événements n’est plus nécessaire dans le code de mise en œuvre. Les clients peuvent associer des données contextuelles à des variables à l’aide de règles de traitement. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | S.O. | Plus nécessaire, car le mappage se fait via des variables réservées et des règles de traitement. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | S.O. | Plus nécessaire, car le mappage se fait via des variables réservées et des règles de traitement. |

### Variables facultatives

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | S.O. | Nous ne fournissons plus de mappages de lecteur préconfigurés. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | S.O. | Nous ne fournissons plus de mappages de lecteur préconfigurés. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | S.O. | La fin du contenu ne prend en charge qu’un marqueur de progression de 100 %. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | S.O. | La fin du contenu ne prend en charge qu’un marqueur de progression de 100 %. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Clé SDK : playerName ;<br>Clé API : media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | S.O. | Media Analytics est défini sur 10 secondes pour le contenu et 1 seconde pour les publicités. Aucune autre option n’est disponible. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | S.O. | Media Analytics effectue toujours le suivi des marqueurs de progression à 10 %, 25 %, 50 %, 75 % et 95 %. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | S.O. | Media Analytics effectue toujours le suivi des marqueurs de progression à 10 %, 25 %, 50 %, 75 % et 95 %. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |

### Variables de suivi des publicités

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | S.O. | Media Analytics est défini sur 10 secondes pour le contenu et 1 seconde pour les publicités. Aucune autre option n’est disponible. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | S.O. | Les marqueurs de progression ne sont pas fournis par défaut pour les publicités. Utilisez des mesures calculées pour créer des marqueurs de progression des publicités. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | S.O. | Media Analytics est défini sur 1 seconde pour les publicités. Aucune autre option n’est disponible. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | S.O. | Le suivi automatique n’est plus disponible. |

### Méthodes du module média

| Milestone | Syntaxe de Milestone | Media Analytics | Syntaxe Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName` : (obligatoire) nom de la vidéo tel que vous souhaitez le voir apparaître dans les rapports vidéo. | nom | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength` : (obligatoire) durée de la vidéo, en secondes. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName` : (obligatoire) nom du lecteur vidéo utilisé pour visionner la vidéo, tel que vous souhaitez le voir apparaître dans les rapports vidéo. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| nom | `name` : (obligatoire) nom ou identifiant de la vidéo. | nom | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length` : (obligatoire) durée de la publicité. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName` : (obligatoire) nom du lecteur vidéo utilisé pour visionner la publicité. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName` : nom ou identifiant du contenu principal dans lequel la publicité est incorporée. | S.O. | Hérité automatiquement. |
| parentPod | `parentPod` : position de lecture de la publicité dans le contenu principal. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition` : position de lecture de la publicité dans la capsule. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM` : CPM ou CPM chiffré (précédé du préfixe « ~ ») applicable à la lecture. | S.O. | Non disponible par défaut dans Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | S.O. | Utilisez un appel d’analyse de lien personnalisé pour effectuer le suivi des clics. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> ou <br>trackEvent | `trackPause()` <br> ou `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> ou <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilisez des métadonnées personnalisées ou standard pour définir des variables supplémentaires. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | S.O. | La fréquence des appels de suivi est définie automatiquement. |
