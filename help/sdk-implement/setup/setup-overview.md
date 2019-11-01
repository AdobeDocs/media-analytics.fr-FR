---
title: Présentation de la configuration
description: Présentation de la configuration du SDK multimédia pour le suivi des médias dans vos applications mobiles, OTT et de navigateur (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Présentation de la configuration{#setup-overview}

>[!IMPORTANT]
>
>Les instructions suivantes s’appliquent aux SDK de média 2.x. Si vous mettez en œuvre une version 1.x du SDK Media, consultez la [Documentation du SDK Media 1.x.](/help/sdk-implement/download-sdks.md) Pour les intégrateurs Primetime, voir Documentation _du SDK multimédia_ Primetime ci-dessous.


## Prise en charge de la version minimale de la plateforme {#minimum-platform-version}

Le tableau suivant décrit les versions minimales de plateformes prises en charge pour chaque SDK, à compter du 19 février 2019.

| OS/Navigateur | Version min requise |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Instructions générales de mise en œuvre {#general-implementation-guidelines}

Trois composants principaux du SDK sont impliqués dans le suivi multimédia :
* Media Heartbeat Config : La configuration contient les paramètres de base des rapports.
* Media Heartbeat Delegate : Le délégué contrôle la durée de lecture et l’objet QoS.
* Media Heartbeat : La bibliothèque principale contient les membres et les méthodes.

Suivez les étapes de mise en oeuvre suivantes :

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  Nom de variable  | Description  | Obligatoire |  Valeur par défaut  |
   |---|---|:---:|---|
   | `trackingServer` | Serveur de suivi pour Media Analytics. Différent de votre serveur de suivi Analytics. | Oui | Chaîne vide |
   | `channel` | Nom du canal | Non | Chaîne vide |
   | `ovp` | Nom de la plate-forme multimédia en ligne sur laquelle le contenu est distribué | Non | Chaîne vide |
   | `appVersion` | Version de l’application/du kit SDK du lecteur multimédia | Non | Chaîne vide |
   | `playerName` | Nom du lecteur multimédia en cours d’utilisation ; par exemple, « AVPlayer », « Lecteur HTML5 », « Mon lecteur personnalisé ». | Non | Chaîne vide |
   | `ssl` | Indique si les appels doivent être effectués par HTTPS | Non | false |
   | `debugLogging` | Indique si la journalisation de débogage est activée | Non | false |

1. Implement the `MediaHeartbeatDelegate`.

   |  Nom de méthode  |  Description  | Obligatoire |
   | --- | --- | :---: |
   | `getQoSObject()` | Retourne l’instance `MediaObject` contenant les informations actuelles sur la qualité de service (QoS). Cette méthode est appelée à plusieurs reprises au cours d’une session de lecture. La mise en œuvre du lecteur doit toujours retourner les plus récentes données QoS disponibles. | Oui |
   | `getCurrentPlaybackTime()` | Renvoie la position actuelle du curseur de lecture. Pour le suivi VOD, la valeur est indiquée en secondes à partir du début de l’élément média. Pour le suivi LINEAR/LIVE, la valeur est indiquée en secondes à partir du début du programme. | Oui |

   >[!TIP]
   >
   >L’objet QoS (Quality of Service) est facultatif. Si les données QoS sont disponibles pour votre lecteur et que vous souhaitez en effectuer le suivi, les variables suivantes sont requises :

   | Nom de variable | Description   | Obligatoire |
   | --- | --- | :---: |
   | `bitrate` | Débit du média, en bits par seconde. | Oui |
   | `startupTime` | Temps de démarrage du média, en millisecondes. | Oui |
   | `fps` | Images affichées par seconde. | Oui |
   | `droppedFrames` | Nombre de pertes d’images jusqu’ici. | Oui |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. Cette instance sera utilisée pour tous les événements de suivi multimédia suivants.

   >[!TIP]
   >
   >`MediaHeartbeat` nécessite une instance de `AppMeasurement` pour envoyer des appels à Adobe Analytics.

1. Combinez tous les éléments.

   L’exemple de code suivant utilise notre SDK JavaScript 2.x pour un lecteur vidéo HTML5 :

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Validation {#validate}

Les implémentations de suivi des analyses multimédia génèrent deux types d’appels de suivi :

* Les appels Media et Ad Start sont envoyés directement au serveur Adobe Analytics (AppMeasurement).
* Les appels de pulsation sont envoyés au serveur de suivi Media Analytics (pulsations), y sont traités et transmis au serveur Adobe Analytics.

* **Serveur** Adobe Analytics (AppMeasurement) Pour plus d’informations sur les options du serveur de suivi, voir [Définition correcte des variables trackingServer et trackingServerSecure.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Une résolution CNAME ou un serveur de suivi RDC sur un serveur RDC est requise pour le service d’identification des visiteurs d’Experience Cloud.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** Serveur Media Analytics (Heartbeats)**Il a toujours le format "`[your_namespace].hb.omtrdc.net`". La valeur de "`[your_namespace]`" indique votre société et est fournie par Adobe.

Le suivi multimédia fonctionne de la même manière sur toutes les plates-formes, de poste de travail comme mobiles. Le suivi audio fonctionne actuellement sur les plateformes mobiles. Pour tous les appels de suivi, quelques variables universelles clés doivent être validées :

## Documentation SDK 1.x {#sdk-1x-documentation}

| SDK d’Analytics vidéo 1.x |  Guides du développeur (PDF uniquement) |
| --- | --- |
| Android | [Configuration pour Android ](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Configuration pour Apple TV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configuration pour Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Configuration pour iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configuration pour JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configuration pour TVML ](vhl_tvml.pdf) |

## Documentation du SDK Media Primetime {#primetime-docs}

* [Guides de l’utilisateur Primetime](https://helpx.adobe.com/primetime/user-guide.html)
