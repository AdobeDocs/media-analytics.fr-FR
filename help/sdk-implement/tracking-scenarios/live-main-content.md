---
title: Contenu principal en direct
description: Exemple de suivi du contenu en direct à l’aide du SDK Media.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Contenu principal en direct {#live-main-content}

## Scénario {#scenario}

Dans ce scénario, il existe une ressource en direct sans publicité lue pendant 40 secondes après avoir rejoint la diffusion en direct.

| Déclencheur | Méthode Heartbeat | Appels réseau | Remarques   |
|---|---|---|---|
| L’utilisateur clique sur **[!UICONTROL Lecture]**. | `trackSessionStart` | Analytics Content Start, Heartbeat Content Start | Il peut s’agir d’un utilisateur qui clique sur **[!UICONTROL Lecture]** ou d’un événement de lecture automatique. |
| La première image du média s’affiche. | `trackPlay` | Heartbeat Content Play | Cette méthode déclenche le minuteur. Les pulsations sont envoyées toutes les 10 secondes tant que la lecture se poursuit. |
| Le contenu est lu. |  | Content Heartbeats |  |
| La session est terminée. | `trackSessionEnd` |  | `SessionEnd` correspond à la fin d’une session de visionnage. Cette API doit être appelée même si l’utilisateur n’utilise pas le média jusqu’à la fin. |

## Paramètres {#parameters}

Un grand nombre de ces valeurs que vous pouvez voir dans les appels Adobe Analytics Content Start sont également présentes dans les appels Heartbeat Content Start. Adobe utilise également de nombreux autres paramètres pour remplir les différents rapports multimédias dans Adobe Analytics. Nous ne les aborderons pas tous ici, mais seuls les plus importants.

### Heartbeat Content Start

| Paramètre | Valeur | Remarques |
|---|---|---|
| `s:sc:rsid` | &lt;Identifiant de votre suite de rapports Adobe> |  |
| `s:sc:tracking_serve` | &lt;URL de votre serveur de suivi Analytics> |  |
| `s:user:mid` | `s:user:mid` | Doit correspondre à la valeur intermédiaire de l’appel Adobe Analytics Content Start. |
| `s:event:type` | &quot;start&quot; |  |
| `s:asset:type` | &quot;main&quot; |  |
| `s:asset:mediao_id` | &lt;Nom de votre média> |  |
| `s:stream:type` | live |  |
| `s:meta:*` | facultatif | Métadonnées personnalisées définies sur le média |

## Content Heartbeats {#content-heartbeats}

Pendant la lecture du média, un minuteur envoie une ou plusieurs pulsations toutes les 10 secondes pour le contenu principal et toutes les secondes pour les publicités. Ces pulsations contiendront des informations sur la lecture, les publicités, la mise en mémoire tampon, etc. Le contenu exact de chaque pulsation dépasse la portée de ce document. La chose essentielle à valider est que les pulsations sont déclenchées de manière cohérente pendant la lecture.

Dans les pulsations de contenu, recherchez quelques éléments spécifiques :

| Paramètre | Valeur | Remarques |
|---|---|---|
| `s:event:type` | &quot;play&quot; |  |
| `l:event:playhead` | &lt;position du curseur de lecture> par exemple, 50, 60, 70 | Ceci doit indiquer la position actuelle du curseur de lecture. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Il n’y aura pas d’appel complet dans ce scénario, car la diffusion en direct n’a jamais été terminée.

## Paramètres des valeurs du curseur de lecture

Pour les flux LIVE, vous devez définir le curseur de lecture sur un décalage par rapport au début de la programmation, de sorte que, dans le rapport, les analystes puissent déterminer à quel moment les utilisateurs rejoignent et quittent le flux dans une vue de 24 heures.

### Au début

Pour le média LIVE, lorsqu’un utilisateur commence la lecture du flux, vous devez définir `l:event:playhead` sur le décalage actuel, en secondes. Ceci s’oppose à VOD, où vous définissez le curseur de lecture sur « 0 ».

Par exemple, supposons qu’un événement de diffusion LIVE commence à minuit et dure 24 heures (`a.media.length=86400` ; `l:asset:length=86400`). Supposons ensuite qu’un utilisateur commence à lire ce flux en direct à 12h00. Dans ce scénario, vous devez définir `l:event:playhead` sur 43200 (12 heures dans le flux).

### En pause

La même logique de « curseur de lecture en direct » appliquée au début de la lecture doit être appliquée lorsqu’un utilisateur interrompt la lecture. Lorsque l’utilisateur revient pour lire le flux en direct, vous devez définir la valeur `l:event:playhead` sur la nouvelle position du curseur de lecture décalée, _pas_ au point où l’utilisateur a interrompu le flux en direct.

## Exemple de code {#sample-code}

![](assets/live-content-playback.png)

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
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
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
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

Voici la commande API prévue :

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

