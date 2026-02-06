---
title: En savoir plus sur la migration de Milestone vers les liens personnalisés
description: Découvrez comment modifier les variables Milestone en liens personnalisés et les méthodes du module Milestone en syntaxe de lien personnalisé.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 79%

---

# Migration de Milestone vers les liens personnalisés{#migrating-from-milestone-to-custom-link}

## Aperçu  {#overview}

Les concepts de base de la mesure vidéo sont les mêmes pour le suivi des liens jalonnés et personnalisés, qui prend des événements de lecteur vidéo et les mappe aux méthodes d’analyse, tout en saisissant les métadonnées et les valeurs du lecteur et en les mappant aux variables d’analyse. L’approche Lien personnalisé doit être considérée comme une réduction et une simplification de l’implémentation et des données collectées. Avec la solution Lien personnalisé, aucune variable ou méthode n’est prédéfinie pour la mesure vidéo, elle nécessite une configuration personnalisée complète. Il devrait être possible de mettre à jour le code d’événement du lecteur pour qu’il pointe vers les appels de suivi des liens personnalisés pour les événements de lecteur de base tels que le début et la fin. Pour plus d’informations, voir le [Guide de mise en oeuvre des liens personnalisés](/help/legacy/measurement-options/cl-in-aa/cl-impl-guide.md).

Les tableaux suivants fournissent des correspondances entre la solution Milestone et la solution des liens personnalisés.

## Guide de migration {#migration-guide}

### Référence de variables vidéo

| Mesure Milestone | Type de variable | Lien personnalisé |
| --- | --- | --- |
| Contenu | eVar <br>Délai d’expiration par défaut : Visite | Définissez votre propre eVar. |
| Type de contenu | eVar <br>Délai d’expiration par défaut : page vue | Définissez votre propre eVar. |
| Temps passé sur le contenu | Type <br> d’événement : Compteur | Définissez votre propre événement. |
| Démarrages de vidéo | Type <br> d’événement : Compteur | Définissez votre propre événement. |
| La vidéo se termine | Type <br> d’événement : Compteur | Définissez votre propre événement. |

### Variables du module média

| Milestone | Syntaxe de Milestone | Lien personnalisé | Syntaxe du lien personnalisé |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | S.O. | Le mappage de données contextuelles à des eVar, des props et des événements s’effectue désormais par le biais de règles de traitement. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Variables facultatives

| Milestone | Syntaxe de Milestone | Lien personnalisé | Syntaxe du lien personnalisé |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | S.O. | Non disponible. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | S.O. | Non disponible. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | S.O. | Non disponible. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | S.O. | Non disponible. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | S.O. | Non disponible. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | S.O. | Non disponible. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | S.O. | Non disponible. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | S.O. | Non disponible. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | S.O. | Non disponible. |

### Variables de suivi des publicités

| Milestone | Syntaxe de Milestone | Lien personnalisé | Syntaxe du lien personnalisé |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | S.O. | Non disponible. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | S.O. | Non disponible. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | S.O. | Non disponible. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | S.O. | Non disponible. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | S.O. | Non disponible. |

### Méthodes du module média

| Milestone | Syntaxe de Milestone | Lien personnalisé | Syntaxe du lien personnalisé |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName` : (obligatoire) nom de la vidéo tel que vous souhaitez le voir apparaître dans les rapports vidéo. | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength` : (obligatoire) durée de la vidéo, en secondes. | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.contextData['video.length']` <br> `  = "90";` |
| mediaPlayerName | `mediaPlayerName` : (obligatoire) nom du lecteur vidéo utilisé pour visionner la vidéo, tel que vous souhaitez le voir apparaître dans les rapports vidéo. | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | S.O. | Non disponible. |
| nom | `name` : (obligatoire) nom ou identifiant de la vidéo. | S.O. | Non disponible. |
| length | `length` : (obligatoire) durée de la publicité. | S.O. | Non disponible. |
| playerName | `playerName` : (obligatoire) nom du lecteur vidéo utilisé pour visionner la publicité. | S.O. | Non disponible. |
| parentName | `parentName` : nom ou identifiant du contenu principal dans lequel la publicité est incorporée. | S.O. | Non disponible. |
| parentPod | `parentPod` : position de lecture de la publicité dans le contenu principal. | S.O. | Non disponible. |
| parentPodPosition | `parentPodPosition` : position de lecture de la publicité dans la capsule. | S.O. | Non disponible. |
| CPM | `CPM` : CPM ou CPM chiffré (précédé du préfixe « ~ ») applicable à la lecture. | S.O. | Non disponible. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Utilisez un appel d’analyse de lien personnalisé pour effectuer le suivi des clics. |
| Media.close | `s.Media.close(mediaName)` | S.O. | Non disponible. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | S.O. | Non disponible. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | S.O. | Non disponible. |
| Media.monitor | `s.Media.monitor(s, media)` | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | S.O. | Non disponible. |
