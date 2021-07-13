---
title: Débogage du SDK
description: Découvrez le suivi et la journalisation disponibles dans le SDK Media.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 96%

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

## Utilisation d’Adobe Bloodhound pour tester les applications Chromecast

Pendant le développement des applications, Bloodhound permet d’afficher les appels de serveur localement et éventuellement de transférer les données vers les serveurs de collecte Adobe.

<!--
For more information about Bloodhound, see the following guides:

* [Bloodhound 3.x for Mac](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwiimfSUypDpAhVZHzQIHS6WDQIQFjABegQIChAD&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound%2F&usg=AOvVaw3t4s0gcvuWEpLIqBkhKdGH) 
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)
-->

>[!IMPORTANT]
>
>Depuis le 30 avril 2017, Adobe Bloodhound fait l’objet d’une élimination progressive. Depuis le 1er mai 2017, plus aucune amélioration n’y est apportée et aucune assistance d’ingénierie supplémentaire ou assistance Adobe Expert Care n’est fournie.

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
