---
title: Explication de l’implémentation des SDK Media hérités
description: Découvrez comment configurer le SDK Media 2.x **hérité** pour le suivi des médias dans vos applications mobiles, OTT et de navigateur (JS).
feature: Streaming Media
role: User, Admin, Developer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
TQID: https://experienceleague.adobe.com/8wkHfEeGx3TtATwf9TH7B6exw2lV5xkgOm-z5GCqajQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: c8add8f2-4250-4fd9-9cde-9707036c567did: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 805
ht-degree: 87%

---

# Présentation de la configuration du SDK Streaming Media 2;X hérité{#setup-overview}

Les instructions de cette section s’appliquent aux SDK Media 2;x **hérités**.

* Pour plus d’informations sur l’implémentation de la version 1.x du SDK Media, consultez la [documentation du SDK Media 1.x.](/help/getting-started/download-sdks.md)

* Pour les intégrateurs Primetime, consultez la _documentation du SDK Media Primetime_.

>[!IMPORTANT]
>
>Avec l’abandon de la prise en charge des SDK mobiles de version 4 programmée au 31 août 2021, Adobe cessera également de prendre en charge les SDK Media Analytics pour iOS et Android.  Pour plus d’informations, reportez-vous à la [FAQ sur l’abandon de la prise en charge du SDK Media Analytics](/help/additional-resources/end-of-support-faqs.md).


## Prise en charge de version minimum de plateforme {#minimum-platform-version}

Le tableau suivant décrit les versions minimum de plateforme prises en charge pour chaque SDK, à compter du 19 février 2019.

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
* Media Heartbeat Config : la configuration contient les paramètres de base des rapports.
* Media Heartbeat Delegate : le délégué contrôle la durée de lecture et l’objet QoS.
* Media Heartbeat : la bibliothèque principale contient les membres et les méthodes.

Suivez les étapes de mise en œuvre suivantes :

1. Créez une instance `MediaHeartbeatConfig` et définissez vos valeurs de paramètre de configuration.

   |  Nom de variable  | Description  | Obligatoire |  Valeur par défaut  |
   |---|---|:---:|---|
   | `trackingServer` | Serveur de suivi pour Media Analytics. Différent de votre serveur de suivi Analytics. | Oui | Chaîne vide |
   | `channel` | Nom du canal | Non | Chaîne vide |
   | `ovp` | Nom de la plateforme multimédia en ligne sur laquelle le contenu est distribué. | Non | Chaîne vide |
   | `appVersion` | Version de l’application/du kit SDK du lecteur multimédia | Non | Chaîne vide |
   | `playerName` | Nom du lecteur multimédia en cours d’utilisation ; par exemple, « AVPlayer », « Lecteur HTML5 », « Mon lecteur personnalisé ». | Non | Chaîne vide |
   | `ssl` | Indique si les appels doivent être effectués par HTTPS | Non | false |
   | `debugLogging` | Indique si la journalisation de débogage est activée | Non | false |

1. Mettez en œuvre le `MediaHeartbeatDelegate`.

   |  Nom de méthode  |  Description  | Obligatoire |
   | --- | --- | :---: |
   | `getQoSObject()` | Retourne l’instance `MediaObject` contenant les informations actuelles sur la qualité de service (QoS). Cette méthode est appelée à plusieurs reprises au cours d’une session de lecture. La mise en œuvre du lecteur doit toujours retourner les plus récentes données QoS disponibles. | Oui |
   | `getCurrentPlaybackTime()` | Renvoie la position actuelle du curseur de lecture. <br /> Pour le suivi VOD, la valeur est spécifiée en secondes à partir du début de l’élément média. <br /> Pour la diffusion en direct, si le lecteur ne fournit pas d’informations sur la durée du contenu, la valeur peut être spécifiée comme le nombre de secondes écoulées depuis minuit UTC de ce jour. <br /> Remarque : lors de l’utilisation de marques de progression, la durée du contenu est une donnée obligatoire et le curseur de lecture doit être mis à jour en tant que nombre de secondes écoulées depuis le début de l’élément média, en commençant par 0. | Oui |

   >[!TIP]
   >
   >L’objet Qualité de service (QoS) est facultatif. Si les données QoS sont disponibles pour votre lecteur et que vous souhaitez en effectuer le suivi, les variables suivantes sont requises :

   | Nom de variable | Description   | Obligatoire |
   | --- | --- | :---: |
   | `bitrate` | Débit du média, en bits par seconde. | Oui |
   | `startupTime` | Temps de démarrage du média, en millisecondes. | Oui |
   | `fps` | Images affichées par seconde. | Oui |
   | `droppedFrames` | Nombre de pertes d’images jusqu’ici. | Oui |

1. Créez l’instance `MediaHeartbeat`.

   Utilisez les instances `MediaHertbeatConfig` et `MediaHertbeatDelegate` pour créer l’instance `MediaHeartbeat`.

   >[!IMPORTANT]
   >
   >Assurez-vous que votre instance `MediaHeartbeat` est accessible et reste attribuée jusqu’à la fin de la session. Cette instance sera utilisée pour tous les événements de suivi multimédia suivants.

   >[!TIP]
   >
   >`MediaHeartbeat` requiert une instance de `AppMeasurement` pour envoyer des appels à Adobe Analytics.

1. Combinez tous les éléments.

   L’exemple de code suivant utilise notre SDK JavaScript 2.x pour un lecteur vidéo HTML5 :

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

Les mises en œuvre de suivi Media Analytics génèrent deux types d’appels de suivi :

* Les appels de démarrage du média et de la publicité sont envoyés directement au serveur Adobe Analytics (AppMeasurement).
* Les appels Heartbeat sont envoyés au serveur de suivi Media Analytics (Heartbeats), y sont traités et transmis au serveur Adobe Analytics.

* Serveur **Adobe Analytics (AppMeasurement)**
Pour plus d’informations sur les options du serveur de suivi, voir [Définition correcte des variables trackingServer et trackingServerSecure.](https://helpx.adobe.com/fr/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >Un serveur de suivi RDC ou CNAME se résolvant sur un serveur RDC est requis pour le service d’identifiant visiteur Experience Cloud.

  Le serveur de suivi des analyses doit se terminer par « `.sc.omtrdc.net` » ou être un serveur CNAME.

* ** serveur Media Analytics (pulsations)**
Celui-ci a toujours le format « `[your_namespace].hb.omtrdc.net` ». La valeur de « `[your_namespace]` » indique votre société et est fournie par Adobe.

Le suivi multimédia fonctionne de la même manière sur toutes les plateformes, de poste de travail comme mobiles. Le suivi audio fonctionne actuellement sur les plateformes mobiles. Pour tous les appels de suivi, quelques variables universelles clés doivent être validées :

## Documentation SDK 1.x {#sdk-1x-documentation}

| Kits SDK Video Analytics 1.x  |  Guides du développeur (PDF uniquement) |
| --- | --- |
| Android | [Configurer pour Android](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Configurer pour Apple TV](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configurer pour Chromecast](chromecast_1.x_sdk.pdf) |
| iOS | [Configurer pour iOS](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurer pour JavaScript](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android : [Configuration de Media Analytics](https://helpx.adobe.com/fr/support/primetime.html) </li> <li> DHLS : [Configuration de Media Analytics](https://helpx.adobe.com/fr/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS : [Configuration de Media Analytics](https://helpx.adobe.com/fr/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurer pour TVML](vhl_tvml.pdf) |

## Documentation du SDK Media Primetime {#primetime-docs}

* [Guides de l’utilisateur Primetime](https://helpx.adobe.com/fr/support/primetime.html)
