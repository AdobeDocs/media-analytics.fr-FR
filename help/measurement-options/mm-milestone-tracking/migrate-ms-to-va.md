---
seo-title: Migration de Milestone vers Media Analytics
title: Migration de Milestone vers Media Analytics
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Migration de Milestone vers Media Analytics {#migrating-from-milestone-to-media-analytics}

## Aperçu {#section_ihl_nbz_cfb}

Les concepts principaux de la mesure vidéo sont les mêmes pour Milestone et Media Analytics, qui prend les événements du lecteur vidéo et les associe aux méthodes d’analyse, tout en récupérant les métadonnées et les valeurs du lecteur et en les associant aux variables d’analyse. La solution Media Analytics est basée sur Milestone, donc de nombreuses méthodes et mesures sont identiques. Toutefois, l’approche et le code de configuration ont beaucoup changé. Il devrait être possible de mettre à jour le code des événements du lecteur afin qu’il pointe vers les nouvelles méthodes Media Analytics. Voir Présentation [du](/help/sdk-implement/setup/setup-overview.md) SDK et Présentation [du](/help/sdk-implement/track-av-playback/track-core-overview.md) suivi pour en savoir plus sur l’implémentation de Media Analytics.

Les tableaux suivants fournissent des correspondances entre la solution Milestone et la solution Media Analytics.

## Guide de migration {#section_iyb_pbz_cfb}

### Référence de variable

| Mesure Milestone | Type de variable | Mesure Media Analytics |
| --- | --- | --- |
| Contenu | Expiration<br/><br/>eVarDefault : Visite | Contenu |
| Type de contenu | eVar<br/><br/> Default expiration: Page view | Type de contenu |
| Temps passé sur le contenu | Event<br/><br/> Type: Counter | Temps passé sur le contenu |
| Démarrages de vidéo | Event<br/><br/> Type: Counter | Démarrages de vidéo |
| La vidéo se termine | Event<br/><br/> Type: Counter | Fin de contenu |

### Variables du module média

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Syntaxe Milestone
</th>
<th>Media Analytics
</th>
<th>Syntaxe Media Analytics
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
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>S.O.
</td>
<td>Toutes les données Media Analytics sont envoyées uniquement à l’aide de données contextuelles.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.segment.media.View":"event2", "a.media.complete":"event7", "a.media.milestones": { 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>S.O.
</td>
<td>Les données contextuelles Media Analytics sont automatiquement renseignées dans des variables réservées. Le mappage à des eVar, des props et des événements n’est plus nécessaire dans le code de mise en œuvre. Les clients peuvent associer des données contextuelles à des variables à l’aide de règles de traitement.
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
<td>S.O.
</td>
<td>Plus nécessaire, car le mappage se fait via des variables réservées et des règles de traitement.
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
<td>S.O.
</td>
<td>Plus nécessaire, car le mappage se fait via des variables réservées et des règles de traitement.
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
<th>Media Analytics
</th>
<th>Syntaxe Media Analytics
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
<td>Nous ne fournissons plus de mappages de lecteur préconfigurés.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams = true
</pre>
</td>
<td>S.O.
</td>
<td>Nous ne fournissons plus de mappages de lecteur préconfigurés.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset = true
</pre>
</td>
<td>S.O.
</td>
<td>Fin de contenu ne prend en charge qu’un marqueur de progression de 100 %.
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
<td>Fin de contenu ne prend en charge qu’un marqueur de progression de 100 %.
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
Clé SDK : playerName; 
Clé API : media.playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds = 15
</pre>
</td>
<td>S.O.
</td>
<td>Media Analytics est défini sur 10 secondes pour le contenu et 1 seconde pour les publicités. Aucune autre option n’est disponible.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestones = "25,50,75";
</pre>
</td>
<td>S.O.
</td>
<td>Media Analytics effectue toujours le suivi des marqueurs de progression à 10 %, 25 %, 50 %, 75 % et 95 %.
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>S.O.
</td>
<td>Media Analytics effectue toujours le suivi des marqueurs de progression à 10 %, 25 %, 50 %, 75 % et 95 %.
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
<td>Le suivi automatique n’est plus disponible.
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
<td>Le suivi automatique n’est plus disponible.
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
<th>Media Analytics
</th>
<th>Syntaxe Media Analytics
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
s.Media.
  adTrackSeconds = 15
</pre>
</td>
<td>S.O.
</td>
<td>Media Analytics est défini sur 10 secondes pour le contenu et 1 seconde pour les publicités. Aucune autre option n’est disponible.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestones = "25,50,75";
</pre>
</td>
<td>S.O.
</td>
<td>Les marqueurs de progression ne sont pas fournis par défaut pour les publicités. Utilisez des mesures calculées pour créer des marqueurs de progression des publicités.
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
<td>Media Analytics est défini sur 1 seconde pour les publicités. Aucune autre option n’est disponible.
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
<td>Le suivi automatique n’est plus disponible.
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
<td>Le suivi automatique n’est plus disponible.
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
<th>Media Analytics
</th>
<th>Syntaxe Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart( mediaObject, contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName - (Obligatoire) nom de la vidéo tel qu’il doit apparaître dans les rapports vidéo.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject( name, mediaId, length, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength - (Obligatoire) durée de la vidéo en secondes.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject( name, mediaId, length, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName - (Obligatoire) nom du lecteur multimédia utilisé pour visionner la vidéo, tel que vous le souhaitez dans les rapports vidéo.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
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
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent( MediaHeartbeat.
    Événement.
    AdBreakStart, adBreakObject); ...trackEvent( MediaHeartbeat.
    Événement.
    AdStart, adObject, adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (Obligatoire) nom ou identifiant de la publicité.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject( nom, IDpublicité, position, longueur)
</pre>
</td>
</tr>
<tr>
<td>
length(Obligatoire) Longueur de la publicité.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject( nom, IDpublicité, position, longueur)
</pre>
</td>
</tr>
<tr>
<td>
playerName - (Obligatoire) nom du lecteur média utilisé pour afficher la publicité.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName : nom ou ID du contenu principal dans lequel la publicité est incorporée.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>S.O.
</td>
<td>Hérité automatiquement
</td>
</tr>
<tr>
<td>
parentPod - Position dans le contenu principal où la publicité a été lue.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject( nom, position, startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition : position dans le module où la publicité est lue.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject( nom, IDpublicité, position, longueur)
</pre>
</td>
</tr>
<tr>
<td>
CPMTle CPM ou CPM chiffré (précédé du préfixe "~") qui s’applique à cette lecture.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>S.O.
</td>
<td>Non disponible par défaut dans Media Analytics
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
<td>S.O.
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
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
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
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> ou 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
ou
<pre>
trackEvent( MediaHeartbeat.
  Événement.
  SeekStart)
</pre> ou
<pre>
trackEvent( MediaHeartbeat.
  Événement.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Utilisez des métadonnées personnalisées ou standard pour définir des variables supplémentaires
</td>
<td>
<pre>
var customVideoMetadata = { isUserLoggingIn: 
    "false", tvStation: 
    "Sample TV station", programmeur : 
    "Sample programmer"}; ...
var standardVideoMetadata = {};
standardVideoMetadata [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = "Sample Episode";
standardVideoMetadata [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Sample Show"; ...
mediaObject.setValue( MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>S.O.
</td>
<td>Le suivi de la fréquence des appels est défini automatiquement.
</td>
</tr>
</tbody>
</table>

