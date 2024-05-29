---
title: Envoi de données web vers Edge avec le SDK web Adobe Experience Platform
description: Découvrez comment envoyer des données Adobe Streaming Media à Experience Platform Edge avec le SDK Web Adobe Experience Platform.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4e6ae687175b45680d8de071dbc3011f18921a44
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Envoi de données web vers Edge avec le SDK web Adobe Experience Platform

À partir de la version 2.20.0, la variable `streamingMedia` composant de Adobe Experience Platform [SDK Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) vous permet de collecter des données relatives aux sessions multimédia sur votre site web. Les données collectées peuvent inclure des informations sur les lectures multimédia, les pauses, les fins et d’autres événements connexes.

Une fois les données collectées, vous pouvez les envoyer à Adobe Experience Platform et/ou Adobe Analytics pour générer des rapports. Cette fonctionnalité offre une solution complète pour effectuer le suivi et comprendre le comportement de consommation des médias sur votre site web.

Pour les clients qui utilisent le SDK Media JS, le SDK Web fournit un chemin de migration pour passer du SDK Media JS au SDK Web, tout en incluant la prise en charge des fonctionnalités Media JS existantes, telles que la gestion des événements multimédia.

## Conditions préalables {#prerequisites}

Pour utiliser la variable `streamingMedia` du SDK Web, vous devez respecter les conditions préalables suivantes :

* Avant d’envoyer des données Media Analytics à Edge, commencez par suivre les étapes de la rubrique [Installation de Media Analytics avec Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Vérifiez que vous avez accès à Adobe Experience Platform et/ou Adobe Analytics.
* Vous devez utiliser le SDK Web version 2.20.0 ou ultérieure. Voir [Présentation de l’installation du SDK Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) pour découvrir comment installer la dernière version.
* Activez la variable **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** pour le flux de données que vous utilisez.
* Assurez-vous que le schéma utilisé par votre flux de données comprend les champs de schéma Media Collection.
* Configurez la fonction Média en flux continu dans la configuration du SDK Web, comme illustré dans cette page, soit par le biais de la fonction [extension de balise](#tag-extension) ou au moyen de la variable [Bibliothèque JavaScript](#library).

Suivez les étapes décrites dans cette page pour migrer votre mise en oeuvre Analytics pour les médias en streaming de Media JS vers le SDK Web.

### Étape 1 : installation du SDK Web Experience Platform

Voir [documentation dédiée](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) pour savoir comment installer le SDK Web sur vos propriétés web.

### Étape 2 : configuration du SDK Web `streamingMedia` composant.

**Exemple**

Le fragment de code ci-dessous indique comment configurer la collecte de médias dans Media JS.

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

Vous devez plutôt configurer la variable `streamingMedia` dans le SDK Web, comme illustré ci-dessous.

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Voir SDK Web `streamingMedia` component [documentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) pour obtenir des informations complètes sur la configuration.

### Étape 3 : Obtention de l’instance de suivi multimédia lors de la migration à partir du SDK Media JS

Pour les clients qui utilisent le SDK Media JS, le SDK Web fournit un chemin de migration pour passer du SDK Media JS au SDK Web, tout en incluant la prise en charge des fonctionnalités Media JS existantes, telles que la gestion des événements multimédia.

[!DNL Web SDK] comprend une commande pour récupérer un outil de suivi Media Analytics. Vous pouvez utiliser cette commande pour créer une instance d’objet, puis, en utilisant les mêmes API que celles fournies par la variable [Bibliothèque JS Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), effectuez le suivi des événements multimédia.

Voir [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getMediaAnalyticsTracker) documentation pour obtenir des détails complets sur les méthodes prises en charge.

Le fragment de code ci-dessous montre comment récupérer l’instance de suivi multimédia dans Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Utilisez plutôt la variable `getMediaAnalyticsTracker` dans le SDK Web pour obtenir le même résultat, comme illustré ci-dessous.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Toutes les méthodes d’assistance seront disponibles sur la page `Media` . Les méthodes de suivi sont disponibles sur l’instance de suivi, comme illustré ci-dessous.

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
