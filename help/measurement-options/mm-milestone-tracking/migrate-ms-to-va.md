---
seo-title: Migration de Milestone vers Media Analytics
title: Migration de Milestone vers Media Analytics
uuid: fdc 96146-af 63-48 ce-b 938-c 0 ca 70729277
translation-type: tm+mt
source-git-commit: 27740fc1753e8ac9cf5a4b240a56b1c2dd567010

---


# Migration de Milestone vers Media Analytics {#migrating-from-milestone-to-media-analytics}

## Aperçu {#section_ihl_nbz_cfb}

Les concepts principaux de la mesure vidéo sont les mêmes pour Milestone et Media Analytics, qui prend les événements du lecteur vidéo et les associe aux méthodes d’analyse, tout en récupérant les métadonnées et les valeurs du lecteur et en les associant aux variables d’analyse. La solution Media Analytics est basée sur Milestone, donc de nombreuses méthodes et mesures sont identiques. Toutefois, l’approche et le code de configuration ont beaucoup changé. Il devrait être possible de mettre à jour le code des événements du lecteur afin qu’il pointe vers les nouvelles méthodes Media Analytics. See [SDK Overview](../../sdk-implement/setup/setup-overview.md) and [Tracking Overview](../../sdk-implement/track-av-playback/track-core-overview.md) for more details on implementing Media Analytics.

Les tableaux suivants fournissent des correspondances entre la solution Milestone et la solution Media Analytics.

## Guide de migration {#section_iyb_pbz_cfb}

### Référence de variable

| Mesure Milestone | Type de variable | Mesure Media Analytics |
| --- | --- | --- |
| Contenu | eVar<br/><br/>Default expiration: Visit | Contenu |
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
s. Media. contextdatamapping = {« a. media. name » : Evar 2, prop 2, « a. media. segment » : « Evar 3 »,
 « a. contenttype » : « Evar 1 »,
 « a. media. timeplayed » : « event 3 »,
 « a. media. view » : « event 1 »,
 « a. media. segmentview » : « event 2 »,
 « a. media. complete » : « event 7 »,
 « a. media. milestones » : {25
 : « event 4 »,
 50 : « event 5 »,
 75 : « event 6 »}}
 ;
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
s. Media. trackvars = 
 « events,
 prop 2,
 evar 1,
 evar 2,
 evar 3 » ;
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
s. Media. trackevents = 
 « event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7 »
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
  Autotracknetstreams
 = true
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
  Completebycloseoffset
 = true
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
  Completecloseoffsetthreshold
 = 1
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
Clé SDK : Playername ; 
Clé API : media. playername
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
  Trackseconds
 = 15
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
  Trackmilestones
 = « 25,50,75 » ;
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
  Trackoffsetmilestones
 = « 20,40,60 » ;
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
  Segmentbyoffsetmilestones
 = true ;
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
  Adtrackseconds
 = 15
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
  Adtrackmilestones
 = « 25,50,75 » ;
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
  Adtrackoffsetmilestones
 = « 20,40,60 » ;
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
  Adsegmentbymilestones
 = true ;
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
  Adsegmentbyoffsetmilestones
 = true ;
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
Tracksessionstart (mediaobject, 
 Contextdata)
</pre>
</td>
</tr>
<tr>
<td>
Medianame - (Obligatoire) nom de la vidéo tel qu'il
doit apparaître dans les rapports vidéo.
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
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Medialength - (Obligatoire) durée de la vidéo
en secondes.
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
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Mediaplayername - (Obligatoire) nom du lecteur de médias utilisé pour afficher la vidéo, tel qu'il doit apparaître dans les rapports vidéo.
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
Mediaheartbeat. trackevent (mediaheartbeat.
 Événement.
    Adbreakstart, 
 Adbreakobject) ;
…
Trackevent (mediaheartbeat.
 Événement.
    Adstart, 
 Adobject, 
 Adcustommetadata) ;
</pre>
</td>
</tr>
<tr>
<td>
name - (Obligatoire) Nom ou identifiant de la publicité.
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
Createadobject (name, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
length
(obligatoire) durée de la publicité.
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
Createadobject (name, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
Playername - (Obligatoire) nom du lecteur de médias
utilisé pour afficher la publicité.
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
Parentname : nom ou identifiant du contenu principal dans lequel la publicité est incorporée.
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
Parentpod - Position de lecture de la publicité dans le contenu principal.
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
Createadbreakobject (name, 
 position, 
 Starttime)
</pre>
</td>
</tr>
<tr>
<td>
Parentpodposition : position de lecture de la publicité dans la capsule.
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
Createadobject (name, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
CPM
ou CPM chiffré (précédé du préfixe « ~ ») qui s'applique à cette lecture.
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
Trackevent (mediaheartbeat.
 Événement.
  SeekStart)
</pre> ou
<pre>
Trackevent (mediaheartbeat.
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
var customvideometadata = 
{isuserloggedin
 : 
 « false »,
 tvstation : 
 « Sample TV station »,
 programmer : 
 « Sample programmer »}
;
…
var standardvideometadata 
 = {} ;
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   EPISODE] = 
 « Exemple d'épisode » ;
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   SHOW] = "Sample Show" ;
…
Mediaobject. setvalue (mediaheartbeat.
 Mediaobjectkey.
 Standardvideometadata, 
 Standardvideometadata) ;
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

