---
title: Reprise des sessions inactives
description: Découvrez comment effectuer la reprise dʼune session inactive.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 38%

---

# Reprise des sessions inactives{#resuming-inactive-sessions}

## Longues pauses

Le SDK Media surveille automatiquement la durée de la lecture multimédia dans l’un des états inactifs suivants :

* En pause
* Recherche en cours
* Bloqué
* Mise en mémoire tampon

Si une session de suivi multimédia reste inactive pendant plus de 30 minutes, celle-ci se fermera automatiquement. Si l’utilisateur ou l’utilisatrice reprend une session de suivi vidéo précédemment inactive (`trackPlay`), Media Heartbeat crée automatiquement une nouvelle session vidéo à l’aide des informations et des métadonnées précédentes et envoie une reprise d’événement de pulsation.

## Transfert entre appareils à l’aide de l’indicateur de reprise

Le même mécanisme de reprise qui gère la continuation de session sur une seule application s’applique également lorsqu’un spectateur transfère la lecture entre appareils (par exemple, la diffusion d’une vidéo à partir d’un téléphone mobile vers un téléviseur ou un récepteur Chromecast). Comme chaque appareil exécute sa propre instance Media SDK, le transfert crée plusieurs sessions par défaut. Utilisez l’indicateur de reprise pour les regrouper en une suite logique, de sorte qu’Analytics signale l’affichage combiné comme un élément unique de l’engagement plutôt que comme des démarrages de média distincts.

**Mise en œuvre :**

1. Sur l’**appareil source** (par exemple, le téléphone), appelez `trackSessionEnd` lorsque la visionneuse lance le cast. Ne pas appeler `trackComplete` — le contenu n&#39;est pas terminé, il est déplacé vers un autre appareil.
2. Sur l’appareil **de destination** (par exemple, le Chromecast), appelez le `trackSessionStart` avec l’indicateur de reprise défini sur `true` et les mêmes métadonnées de contenu (nom, ID, longueur) utilisées sur l’appareil source. Transmettez la position de la tête de lecture à l’endroit où la visionneuse s’est arrêtée sur l’appareil source.
3. Si la visionneuse renvoie ultérieurement la lecture à l’appareil source, répétez le même modèle : `trackSessionEnd` sur la destination et `trackSessionStart` avec l’indicateur de reprise sur la source.

La définition de l’indicateur de reprise entraîne l’incrémentation d’Adobe Analytics [Reprises du contenu](/help/reporting/metrics/content-resumes.md) plutôt que [Débuts du média](/help/reporting/metrics/media-starts.md) pour la deuxième étape et les étapes suivantes du transfert. Comme il n’existe aucun mécanisme intégré pour partager l’ID de session entre les instances SDK, l’indicateur de reprise est une déclaration côté client que vous transmettez en fonction de la logique de votre application lorsque vous savez que la visionneuse poursuit une session précédente.

## Reprise manuelle d’une session précédemment fermée

Le SDK Media procédera uniquement à la reprise automatique des sessions si l’application n’a pas été fermée. Si l’application stocke des données utilisateur et permet de procéder à la reprise d’un média précédemment fermé, il est possible de déclencher manuellement un événement de reprise. Lorsque vous démarrez la session de suivi vidéo, configurez la propriété facultative Video Resumed.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true
public void onmediaLoad(Observable observable, Object data) {

  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD
  );

  // Set to true if this is a resume playback scenario
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);

  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification {
  //Replace <MEDIA_NAME> with the media name.
  //Replace <MEDIA_ID> with a media unique identifier.
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                       mediaId:<MEDIA_ID>
                       length:<MEDIA_LENGTH>
                       streamType:ADBMediaHeartbeatStreamTypeVOD];

  //Set to YES if this user is resuming a previously closed media session
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata];
}
```

### JavaScript

```js
_onmediaLoad = function () {
  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session
  mediaObject.setValue(MediaObjectKey.mediaResumed, true);
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
