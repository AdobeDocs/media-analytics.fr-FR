---
seo-title: Débogage du SDK
title: Débogage du SDK
uuid: a 5972 d 87-c 593-4 b 4 f-a 56 f-dca 6 e 25268 e 1
translation-type: tm+mt
source-git-commit: 6b6caa59ac9ea14a42337e2f133ecb31f30491c7

---


# Débogage du SDK{#sdk-debugging}

Vous pouvez activer et désactiver la journalisation. Le kit de développement multimédia fournit un mécanisme de suivi/journalisation étendu mis en place dans toute la pile de suivi vidéo. You can enable or disable this logging by setting the `debugLogging` flag on the Config object.

## Exemple de code pour la journalisation du débogage

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

**Utilisation d’Adobe Bloodhound pour tester les applications Chromecast -**

Pendant le développement des applications, Bloodhound permet d’afficher les appels de serveur localement et éventuellement de transférer les données vers les serveurs de collecte Adobe. Pour obtenir plus d’informations sur Bloodhound, consultez les guides suivants :

* [Bloodhound 3.x pour Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 pour Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>Depuis le 30 avril 2017, Adobe Bloodhound est un coucher de soleil. Depuis le 1er mai 2017, plus aucune amélioration n’y est apportée et aucune assistance d’ingénierie supplémentaire ou assistance Adobe Expert Care n’est fournie.

### Messages du journal

Les messages du journal suivent ce format :

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp :** (horodatage) heure actuelle du processeur (fuseau horaire GMT)
* **level :** (niveau) il existe 4 niveaux de message définis :
   * INFO – (information) Généralement, données saisies dans l’application (nom du lecteur de validation, identifiant vidéo, etc.)
   * DEBUG – (débogage) Journaux de débogage utilisés par les développeurs pour déboguer des problèmes plus complexes
   * WARN – (avertissement) Erreurs potentielles d’intégration/de configuration ou bogues SDK de pulsation
   * ERROR – (erreur) Erreurs d’intégration ou bogues SDK de pulsation importants
* **tag :** nom du sous-composant qui a émis le message du journal (généralement le nom de classe)
* **message :** message de trace

Vous pouvez utiliser le résultat des journaux de la bibliothèque Video Heartbeat pour vérifier la mise en œuvre. A good strategy is to search through the logs for the string `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

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

