---
title: Contenu principal en direct avec suivi séquentiel
description: Exemple de suivi du contenu en direct avec suivi séquentiel à l’aide du SDK Media.
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
exl-id: 277a72b8-453b-41e5-b640-65c43587baf8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oCoZuJHBMNOe3I6ITBqIQO6BSTNSWpbsjzXGuzd9KyU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
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
source-wordcount: 526
ht-degree: 98%

---

# Contenu principal en direct avec suivi séquentiel{#live-main-content-with-sequential-tracking}

## Scénario {#scenario}

Dans ce scénario, il existe une ressource en direct sans publicité lue pendant 40 secondes après avoir rejoint la diffusion en direct.

Il s’agit du même scénario que le scénario [Lecture VOD sans publicité](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md), mais une partie du contenu est parcourue en défilement et une recherche est effectuée d’un point du contenu principal à un autre.

| Déclencheur | Méthode Heartbeat |  Appels réseau  |  Notes   |
| --- | --- | --- | --- |
| L’utilisateur clique sur [!UICONTROL Lecture]. | trackSessionStart | Analytics Content Start, Heartbeat Content Start | Étant donné que la bibliothèque de mesures ignore la présence d’une publicité preroll, ces appels réseau sont identiques au scénario [Lecture VOD sans publicité](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md). |
| La première image du contenu s’affiche. | trackPlay | Heartbeat Content Play | Lorsque le contenu du chapitre est lu avant le contenu principal, le Heartbeats commence lorsque le chapitre commence. |
| Le contenu est lu | | Content Heartbeats | Il s’agit du même appel réseau que le scénario [Lecture VOD sans publicité](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md). |
| Fin de la session (fin de l’épisode 1) | trackComplete / trackSessionEnd | Heartbeat Content Complete | Complete signifie que la session 1 du 1er épisode a été atteinte et visionnée complètement. Avant de commencer la session pour le prochain épisode, cette session doit être terminée. |
| Démarrage de l’épisode 2 (démarrage de la session 2) | trackSessionStart | Analytics Content Start Heartbeat Content Start | Cela se produit lorsqu’un utilisateur a visionné un premier épisode suivi d’un autre épisode. |
| 1re image du média | trackPlay | Heartbeat Content Play | Cette méthode déclenche le retardateur et, à partir de ce moment, les pulsations sont envoyées toutes les 10 secondes tant que la lecture se poursuit. |
| Le contenu est lu | | Content Heartbeats | |
| Fin de la session (fin de l’épisode 2) | trackComplete / trackSessionEnd | Heartbeat Content Complete | Complete signifie que la session 2 du 2e épisode a été atteinte et visionnée complètement. Avant de commencer la session pour le prochain épisode, cette session doit être terminée. |

## Paramètres {#parameters}

### Heartbeat Content Start

| Paramètre | Valeur | Remarques |
|---|---|---|
| `s:sc:rsid` | &lt;Identifiant de votre suite de rapports Adobe> |  |
| `s:sc:tracking_serve` | &lt;URL de votre serveur de suivi Analytics> |  |
| `s:user:mid` | `s:user:mid` | Doit correspondre à la valeur intermédiaire de l’appel Adobe Analytics Content Start. |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;Nom de votre média> |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *facultatif* | Métadonnées personnalisées définies sur le média |

## Heartbeat Content Play {#heartbeat-content-play}

Cela devrait ressembler presque exactement à l’appel Heartbeat Content Start, mais avec une différence majeure dans le paramètre « s:event:type ». Tous les paramètres devraient toujours être en place ici.

| Paramètre | Valeur | Remarques |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## Content Heartbeats {#content-heartbeats}

Pendant la lecture du média, un retardateur envoie une ou plusieurs pulsations toutes les 10 secondes pour le contenu principal et toutes les secondes pour les publicités. Ces pulsations contiendront des informations sur la lecture, les publicités, la mise en mémoire tampon, etc. Le contenu exact de chaque pulsation dépasse la portée de ce document. La chose essentielle à valider est que les pulsations sont déclenchées de manière cohérente pendant la lecture.

Dans les pulsations de contenu, recherchez quelques éléments spécifiques :

| Paramètre | Valeur | Remarques |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;position du curseur de lecture> par exemple, 50, 60, 70 | Ceci doit indiquer la position actuelle du curseur de lecture. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Une fois la lecture d’un épisode donné terminée (le curseur de lecture franchit la limite de l’épisode), un appel Heartbeat Content Complete est envoyé. Cela ressemble aux autres appels Heartbeat, avec tout de même quelques éléments spécifiques :

| Paramètre | Valeur | Remarques |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## Exemple de code {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

### Android

Voici la commande API prévue :

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., when there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing 1st episode/session.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2 /episode 2 of the same live stream.  
// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
//    start of session 2 
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue similarly tracking further sessions in the live stream if required 
```

### iOS

Voici la commande API prévue :

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
  
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
  
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
  
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing the first 
//    episode/session. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 4. Call trackSessionEnd to end session 1 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Start tracking session 2 / episode 2 of the same live stream, No need to  
// reinstantiate mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 5. Call trackSessionStart when the playhead reaches a point that denotes  
//    start of session 2 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 6. Call trackPlay to start tracking session 2 playback 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 7. Call trackComplete when the playback reaches the end of session 2,  
//    i.e., when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 
 
// 8. Call trackSessionEnd to end the session 2 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

### JavaScript

Voici la commande API prévue :

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of a session,  
//    i.e., whn playback completes and finishes playing the 1st episode/session. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2/episode 2 of the same live stream. There is no need  
// to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
var mediaInfo2 = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

var mediaMetadata2 = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes  
//    the start of session 2 
this._mediaHeartbeat.trackSessionStart(mediaInfo2, mediaMetadata2); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```
