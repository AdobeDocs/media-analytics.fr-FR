---
title: Envoyer des données web à Edge avec Adobe Experience Platform Web SDK
description: Découvrez comment envoyer des données Adobe Streaming Media vers Experience Platform Edge avec Adobe Experience Platform Web SDK.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 1%

---

# Envoyer des données web à Edge avec Adobe Experience Platform Web SDK

À partir de la version 2.20.0, le composant `streamingMedia` de Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/home) vous permet de collecter des données relatives aux sessions multimédia sur votre site Web. Les données collectées peuvent inclure des informations sur les lectures de médias, les pauses, les terminaisons et d’autres événements associés.

Une fois les données collectées, vous pouvez les envoyer à Adobe Experience Platform et/ou Adobe Analytics pour générer des rapports. Cette fonctionnalité fournit une solution complète pour suivre et comprendre le comportement de consommation des médias sur votre site web.

Pour les clients qui utilisent le SDK Media JS, Web SDK fournit un chemin de migration permettant de passer de Media JS SDK à Web SDK, tout en incluant la prise en charge des fonctionnalités Media JS existantes, telles que la gestion des événements multimédia.

## Conditions préalables {#prerequisites}

Pour utiliser le composant `streamingMedia` de Web SDK, les conditions préalables suivantes doivent être remplies :

* Avant d’envoyer des données de médias en flux continu à Edge, suivez d’abord les étapes de la section [Installation de la collection de médias en flux continu avec Experience Platform Edge](/help/implementation/edge/implementation-edge.md).
* Assurez-vous d’avoir accès à Adobe Experience Platform et/ou Adobe Analytics.
* Vous devez utiliser Web SDK version 2.20.0 ou ultérieure. Voir la [présentation de l’installation de Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/install/overview) pour savoir comment installer la dernière version.
* Activez l’option **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/fr/docs/experience-platform/datastreams/configure)** pour le flux de données que vous utilisez.
* Assurez-vous que le schéma utilisé par votre flux de données comprend les champs de schéma Media Collection.
* Configurez la fonction Streaming Media dans la configuration de Web SDK, comme illustré sur cette page, soit par le biais de l’extension [tag](#tag-extension), soit par le biais de la bibliothèque [JavaScript](#library).

Suivez les étapes décrites dans cette page pour migrer votre implémentation de Streaming Media Collection de Media JS vers Web SDK.

### Étape 1 : Installer Experience Platform Web SDK

Consultez la [documentation dédiée](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/install/overview) pour savoir comment installer Web SDK sur vos propriétés web.

### Étape 2 : configurer le composant `streamingMedia` de Web SDK.

**Exemple**

L’extrait de code ci-dessous indique comment configurer la collecte de médias dans Media JS.

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

Vous devez plutôt configurer le composant `streamingMedia` dans le SDK Web, comme illustré ci-dessous.

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

Consultez le composant `streamingMedia` de Web SDK [documentation](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) pour obtenir des informations complètes sur sa configuration.

### Étape 3 : obtenir l’instance de suivi multimédia lors de la migration depuis Media JS SDK

Pour les clients qui utilisent le SDK Media JS, Web SDK fournit un chemin de migration permettant de passer de Media JS SDK à Web SDK, tout en incluant la prise en charge des fonctionnalités Media JS existantes, telles que la gestion des événements multimédia.

[!DNL Web SDK] comprend une commande permettant de récupérer un dispositif de suivi Media Analytics. Vous pouvez utiliser cette commande pour créer une instance d’objet, puis, à l’aide des mêmes API que celles fournies par la [bibliothèque JS Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), effectuer le suivi des événements multimédia.

Consultez la documentation [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) pour plus d’informations sur les méthodes prises en charge.

Le fragment de code ci-dessous indique comment récupérer l’instance de suivi multimédia dans Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Utilisez plutôt la commande `getMediaAnalyticsTracker` dans Web SDK pour obtenir le même résultat, comme illustré ci-dessous.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Toutes les méthodes d&#39;assistance seront disponibles sur l&#39;objet `Media`. Les méthodes de suivi sont disponibles sur l’instance de suivi, comme illustré ci-dessous.

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
