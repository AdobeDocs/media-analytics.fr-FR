---
title: 'Migration de Media SDK autonome vers Adobe Launch : Web (JS)'
description: Découvrez comment migrer du SDK Media vers Launch pour JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/N4Fcbg3R9tT9cjUcaw-kcUm6h-QT8TYwatdCe1IdsaM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c069c44e-5426-4c1a-accc-8028662f2fdeid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 77%

---

# Migration du SDK Media autonome vers Adobe Launch : Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.

## Différences de fonctionnalités

* *Launch* : Launch offre une interface utilisateur qui vous guide tout au long de l’installation, de la configuration et du déploiement de vos solutions de suivi multimédia en ligne. Launch est une version améliorée de Dynamic Tag Management (DTM).
* *SDK Media* : le SDK Media propose des bibliothèques de suivi multimédia conçues pour des plateformes spécifiques (comme Android, iOS, etc.). Adobe recommande le SDK Media pour le suivi de l’utilisation des médias dans vos applications mobiles.

## Configuration

### SDK Media autonome

Dans Media SDK autonome, vous configurez le suivi dans l’application
et transmettez-le au SDK lors de la création du dispositif de suivi.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Outre la configuration `MediaHeartbeat`, la page doit configurer et transmettre .
l’instance `AppMeasurement` et l’instance `VisitorAPI` pour le suivi multimédia dans l’ordre
pour fonctionner correctement.

### Extension de Launch

1. Dans Experience Platform Launch, cliquez sur l’onglet [!UICONTROL Extensions] de votre
propriété web.
1. Dans l’onglet [!UICONTROL  Catalogue ], recherchez Adobe Media Analytics for Audio et
Extension vidéo, puis cliquez sur [!UICONTROL  Installer ].
1. Dans la page des paramètres d’extension, configurez les paramètres de suivi.
L’extension Media utilisera les paramètres configurés pour le suivi.

   ![](assets/launch_config_js.png)

[Guide de l’utilisateur de Launch - Installation et configuration de l’extension Media](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=fr#install-and-configure-the-ma-extension)

## Différences dans la création du dispositif de suivi

### SDK Media

1. Ajoutez la bibliothèque Media Analytics à votre projet de développement.
1. Créez un objet de configuration (`MediaHeartbeatConfig`).
1. Implémentez le protocole délégué exposant les fonctions `getQoSObject()` et `getCurrentPlaybackTime()`.
1. Créez une instance Media Heartbeat (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

### Launch

Launch propose deux méthodes pour créer l’infrastructure de suivi. Les deux méthodes utilisent l’extension Media Analytics pour Launch :

1. Utilisez les API de suivi multimédia d’une page Web.

   Dans cette configuration, l’extension Media Analytics exporte les API de suivi multimédia vers une variable configurée dans l’objet « window » global :

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilisez les API de suivi multimédia d’une autre extension de Launch.

   Dans cette configuration, vous utilisez les API de suivi multimédia exposées par les modules partagés `get-instance` et `media-heartbeat`.

   >[!NOTE]
   >
   >Les modules partagés ne peuvent pas être utilisés dans des pages Web. Vous pouvez uniquement utiliser des modules partagés à partir d’une autre extension.

   Créez une instance `MediaHeartbeat` à l’aide du module partagé `get-instance`.
Transmettez un objet délégué à `get-instance` qui expose les fonctions `getQoSObject()` et `getCurrentPlaybackTime()`.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Accédez aux constantes `MediaHeartbeat` via le module partagé `media-heartbeat`.

## Documentation connexe

### SDK Media

* [Configuration de JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [API JS Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Présentation de Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)
* [Extension Media Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=fr)
