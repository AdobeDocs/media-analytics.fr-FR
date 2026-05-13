---
title: Contenu principal en direct
description: Exemple de suivi du contenu en direct à l’aide du SDK Media.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oOshJZEQmXqgNh5l10-qhLMO8dmph6Tz9mpH0a4FePU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 590
ht-degree: 98%

---

# Contenu principal en direct{#live-main-content}

## Scénario {#scenario}

Dans ce scénario, il existe une ressource en direct sans publicité lue pendant 40 secondes après avoir rejoint la diffusion en direct.

| Déclencheur | Méthode Heartbeat | Appels réseau | Notes   |
|---|---|---|---|
| L’utilisateur clique sur **[!UICONTROL Lecture]**. | `trackSessionStart` | Analytics Content Start, Heartbeat Content Start | Il peut s’agir d’un utilisateur qui clique sur **[!UICONTROL Lecture]** ou d’un événement de lecture automatique. |
| La première image du média s’affiche. | `trackPlay` | Heartbeat Content Play | Cette méthode déclenche le retardateur. Les pulsations sont envoyées toutes les 10 secondes tant que la lecture se poursuit. |
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

Pendant la lecture du média, un retardateur envoie une ou plusieurs pulsations toutes les 10 secondes pour le contenu principal et toutes les secondes pour les publicités. Ces pulsations contiendront des informations sur la lecture, les publicités, la mise en mémoire tampon, etc. Le contenu exact de chaque pulsation dépasse la portée de ce document. La chose essentielle à valider est que les pulsations sont déclenchées de manière cohérente pendant la lecture.

Dans les pulsations de contenu, recherchez quelques éléments spécifiques :

| Paramètre | Valeur | Remarques |
|---|---|---|
| `s:event:type` | &quot;play&quot; |  |
| `l:event:playhead` | &lt;position du curseur de lecture> par exemple, 50, 60, 70 | Ceci doit indiquer la position actuelle du curseur de lecture. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Il n’y aura pas d’appel complet dans ce scénario, car la diffusion en direct n’a jamais été terminée.

## Paramètres des valeurs du curseur de lecture

Pour les flux en direct, vous devez définir la valeur du curseur de lecture comme étant le nombre de secondes écoulées depuis minuit UTC ce jour-là, de sorte que dans le compte rendu des performances, les analystes puissent déterminer à quel moment les utilisateurs rejoignent et quittent le flux en direct sur une période de 24 heures.

### Au début

Pour les flux en direct, lorsquʼun utilisateur commence la lecture du flux, vous devez définir `l:event:playhead` sur le nombre de secondes écoulées depuis minuit UTC ce jour-là. Contrairement à VOD, où vous définissez le curseur de lecture sur « 0 ». Remarque : lors de l’utilisation de marques de progression, la durée du contenu est une donnée obligatoire et le curseur de lecture doit être mis à jour en tant que nombre de secondes écoulées depuis le début de l’élément média, en commençant par 0.

Par exemple, supposons qu’un événement de diffusion LIVE commence à minuit et dure 24 heures (`a.media.length=86400` ; `l:asset:length=86400`). Supposons ensuite qu’un utilisateur commence à lire ce flux en DIRECT à 12 :00pm. Dans ce scénario, vous devez définir `l:event:playhead` sur 43200 (12 heures écoulées depuis minuit UTC ce jour-là, en secondes).

### En pause

La même logique de « curseur de lecture en direct » appliquée au début de la lecture doit être appliquée lorsqu’un utilisateur interrompt la lecture. Lorsque lʼutilisateur revient pour lire le flux en direct, vous devez définir la valeur `l:event:playhead` par rapport au nouveau nombre de secondes écoulées depuis minuit UTC, _pas_ au point où lʼutilisateur a interrompu le flux en direct.

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
