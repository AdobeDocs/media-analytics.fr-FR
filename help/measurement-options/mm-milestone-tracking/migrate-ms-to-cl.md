---
title: Migration de Milestone vers les liens personnalisés
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Migration de Milestone vers les liens personnalisés{#migrating-from-milestone-to-custom-link}

## Aperçu {#overview}

Les concepts principaux de la mesure vidéo sont les mêmes pour Milestone et le suivi des liens personnalisés, qui prend les événements du lecteur vidéo et les associe aux méthodes d’analyse, tout en récupérant les métadonnées et les valeurs du lecteur et en les associant aux variables d’analyse. L’approche des liens personnalisés doit être considérée comme une simplification de la mise en œuvre et des données collectées. Avec la solution des liens personnalisés, aucune variable ni méthode n’est prédéfinie pour la mesure vidéo. Une configuration personnalisée complète est requise. Il devrait être possible de mettre à jour le code des événements du lecteur afin qu’il pointe vers les appels de suivi des liens personnalisés pour les événements de lecteur de base tels que start et complete. Consultez le [Guide de mise en œuvre d’un lien personnalisé](/help/measurement-options/cl-in-aa/cl-impl-guide.md) et la rubrique [Suivi d’un lien manuel à l’aide d’un code de lien personnalisé](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) pour en savoir plus.

Les tableaux suivants fournissent des correspondances entre la solution Milestone et la solution des liens personnalisés.

## Guide de migration {#migration-guide}

### Référence de variables vidéo

<table>
<thead>
<tr>
<th><strong>Mesure Milestone</strong></th>
<th><strong>Type de variable</strong></th>
<th><strong>Lien personnalisé</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Types de</td>
<td>
<p>eVar</p>
<p>Délai d’expiration par défaut : Visite</p>
</td>
<td>Définissez votre propre eVar</td>
</tr>
<tr>
<td>Type de contenu</td>
<td>
<p>eVar</p>
<p>Délai d’expiration par défaut : page vue</p>
</td>
<td>Définissez votre propre eVar</td>
</tr>
<tr>
<td>Temps passé sur le contenu</td>
<td>
<p>Événement</p>
<p>Type : compteur</p>
</td>
<td>Définissez votre propre événement</td>
</tr>
<tr>
<td>Démarrages de vidéo</td>
<td>
<p>Événement</p>
<p>Type : compteur</p>
</td>
<td>Définissez votre propre événement</td>
</tr>
<tr>
<td>La vidéo se termine</td>
<td>
<p>Événement</p>
<p>Type : compteur</p>
</td>
<td>Définissez votre propre événement</td>
</tr>
</tbody>
</table>

### Variables du module média

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Syntaxe Milestone
</th>
<th>Lien personnalisé
</th>
<th>Syntaxe  du lien personnalisé
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData[‘video.name’] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = { "a.media.name" :
    "eVar2,prop2", "a.media.segment" :
    "eVar3", "a.contentType" :
    "eVar1", "a.media.timePlayed" :
    "event3", "a.media.view" :
    "event1", "a.media.segmentView" :
    "event2", "a.media.complete" :
    "event7", "a.media.milestones" :{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>S.O.
</td>
<td>Le mappage de données contextuelles à des eVar, des props et des événements s’effectue désormais par le biais de règles de traitement.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Syntaxe Milestone
</th>
<th>Lien personnalisé
</th>
<th>Syntaxe  du lien personnalisé
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.
  trackUsingContextData = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, contextData.video.name'; 
s.contextData[‘video.name’] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segment.media.View":"event2", "a.media.complete":"event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>S.O.
</td>
<td>Le mappage de données contextuelles à des eVar, des props et des événements s’effectue désormais par le biais de règles de traitement.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15, contextData.
       video.name, contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

### Variables facultatives

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Syntaxe Milestone
</th>
<th>Lien personnalisé
</th>
<th>Syntaxe  du lien personnalisé
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold = 1
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Nom du lecteur personnalisé"
</pre>
</td>
<td>
Définissez une eVar ou une variable de données contextuelles dans l’appel de lien
</td>
<td>
<pre>
s.contextData['video.player'] ="Nom du lecteur personnalisé";
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones = true;
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
</tbody>
</table>

### Variables de suivi des publicités

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Syntaxe Milestone
</th>
<th>Lien personnalisé
</th>
<th>Syntaxe  du lien personnalisé
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones = true;
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones = true;
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
</tbody>
</table>

### Méthodes du module média

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Syntaxe Milestone
</th>
<th>Lien personnalisé
</th>
<th>Syntaxe  du lien personnalisé
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.video.name, contextData.video.view';
s.linkTrackEvents = 'event2';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event2';
s.contextData['video.name'] = mediaName;
s.contextData['video.view'] = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b></b> mediaName : (obligatoire) nom de la vidéo tel qu’il doit apparaître dans les rapports vidéo.</td>
<td>Définissez une eVar ou une variable de données contextuelles dans l’appel de lien</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name'] = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b></b> mediaLength : (obligatoire) durée de la vidéo en secondes.
</td>
<td>
Définissez une eVar ou une variable de données contextuelles dans l’appel de lien
</td>
<td>
<pre>
s.contextData['video.length'] ="90";
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b></b> mediaPlayerName : (obligatoire) nom du lecteur de médias utilisé pour afficher la vidéo, comme vous le souhaitez dans les rapports vidéo.
</td>
<td>
Définissez une eVar ou une variable de données contextuelles dans l’appel de lien
</td>
<td>
<pre>
s.contextData['video.player'] ="Nom du lecteur personnalisé";
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible</td>
</tr>
<tr>
<td>name</td>
<td><b></b> name : (obligatoire) nom ou identifiant de la publicité.</td>
<td>S.O.</td>
<td>Non disponible</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b></b> length : (obligatoire) durée de la publicité.
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b></b> playerName : (obligatoire) nom du lecteur de médias utilisé pour afficher la publicité.
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName</b> : nom ou identifiant du contenu principal dans lequel la publicité est incorporée.
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod</b> : position de lecture de la publicité dans le contenu principal.
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition</b> : position de lecture de la publicité dans la capsule.
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM</b> : CPM ou CPM chiffré (précédé du préfixe « ~ ») applicable à la lecture.
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
</td>
<td>Utilisez un appel d’analyse de lien personnalisé pour effectuer le suivi des clics
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
s.tl()
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.complete';
s.linkTrackEvents = 'event3';
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.eVar12 = "video";
s.eVar15 = mediaPlayerName;
s.events = 'event3';
s.contextData['video.name'] = mediaName;
s.contextData['video.complete'] = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>S.O. 
</td>
<td>Non disponible
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Définissez une eVar ou une variable de données contextuelles dans l’appel de lien
</td>
<td>
<pre>
s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar15, contextData.
       video.name, contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible
</td>
</tr>
</tbody>
</table>

