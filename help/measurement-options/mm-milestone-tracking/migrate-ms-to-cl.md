---
title: Migration de Milestone vers les liens personnalisés
description: Migration de Milestone vers les liens personnalisés
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '582'
ht-degree: 100%

---

# Migration de Milestone vers les liens personnalisés {#migrating-from-milestone-to-custom-link}

## Aperçu {#overview}

Les concepts principaux de la mesure vidéo sont les mêmes pour Milestone et le suivi des liens personnalisés, qui prend les événements du lecteur vidéo et les associe aux méthodes d’analyse, tout en récupérant les métadonnées et les valeurs du lecteur et en les associant aux variables d’analyse. L’approche des liens personnalisés doit être considérée comme une simplification de la mise en œuvre et des données collectées. Avec la solution des liens personnalisés, aucune variable ni méthode n’est prédéfinie pour la mesure vidéo. Une configuration personnalisée complète est requise. Il devrait être possible de mettre à jour le code des événements du lecteur afin qu’il pointe vers les appels de suivi des liens personnalisés pour les événements de lecteur de base tels que start et complete. Pour plus d’informations, voir le [Guide de mise en oeuvre des liens personnalisés](/help/measurement-options/cl-in-aa/cl-impl-guide.md).

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
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
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
| mediaLength | `mediaLength` : (obligatoire) durée de la vidéo, en secondes. | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.contextData['video.length']` <br> `  = ”90”;` |
| mediaPlayerName | `mediaPlayerName` : (obligatoire) nom du lecteur vidéo utilisé pour visionner la vidéo, tel que vous souhaitez le voir apparaître dans les rapports vidéo. | Définissez une eVar ou une variable de données contextuelles dans l’appel de lien. | `s.contextData['video.player']` <br> `  = ”CustomPlayer Name”;` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | S.O. | Non disponible. |
| name | `name` : (obligatoire) nom ou identifiant de la vidéo. | S.O. | Non disponible. |
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
