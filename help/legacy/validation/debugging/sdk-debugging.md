---
title: Débogage du SDK
description: Découvrez le suivi et la journalisation disponibles dans le SDK Media.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/H62IoGbWZ3JPApfb-wFlt9P-oa3rD1kCzalpXEQ4Km0
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 221
ht-degree: 100%

---

# Débogage du SDK{#sdk-debugging}

Vous pouvez activer et désactiver la journalisation. Le SDK Media fournit un mécanisme de suivi/journalisation étendu dans toute la pile de suivi multimédia. Vous pouvez activer ou désactiver cette journalisation de la bibliothèque en assignant l’indicateur `debugLogging` sur l’objet de configuration.

## Exemple de code pour connexion de débogage

### Android

```java
// Media Heartbeat initialization
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.debugLogging = true;

// Use this space for setting other config values
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config);
```

### iOS

```
// Media Heartbeat Initialization
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];
config.debugLogging = YES;

// Use this space for setting other config values
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config];
```

### JavaScript

```js
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.debugLogging = true;
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### OTT (Chromecast, Roku)

La bibliothèque ADBMobile fournit une journalisation de débogage à l’aide de la méthode `setDebugLogging`. La journalisation de débogage doit être définie sur `false` pour toutes les applications de production.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Messages du journal

Les messages du journal suivent ce format :

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **date et heure :** il s’agit de l’heure actuelle du processeur (fuseau horaire GMT)
* **niveau :** il existe quatre niveaux de message définis :
   * INFO - généralement les données d’entrée de l’application (nom du lecteur de validation, ID de vidéo, etc.)
   * DEBUG - journaux de débogage utilisés par les développeurs pour déboguer des problèmes plus complexes
   * WARN - indique des erreurs potentielles d’intégration/de configuration ou des bogues du SDK Heartbeats
   * ERROR - indique d’importantes erreurs d’intégration ou des bogues du SDK Heartbeats
* **balise :** nom du sous-composant qui a émis le message du journal (généralement le nom de classe)
* **message :** le message de trace réel

Vous pouvez utiliser le résultat des journaux de la bibliothèque SDK Media pour vérifier la mise en œuvre. Rechercher la chaîne `#track` parmi les journaux est une bonne stratégie. Cela permet de mettre en évidence touts les appels `track*()` effectués par votre application.

Par exemple, voici à quoi pourraient ressembler les journaux filtrés pour `#track` :

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad()
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart()
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay()
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart()
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart()
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete()
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart()
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause()
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete()
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```
