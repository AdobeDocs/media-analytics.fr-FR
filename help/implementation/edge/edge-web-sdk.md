---
title: Envoi de données Web à Edge avec le SDK Web de Adobe Experience Platform
description: Découvrez comment envoyer des données Adobe Streaming Media à Experience Platform Edge avec le SDK Web Adobe Experience Platform.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: de40ebd9-46be-4a52-866f-7bb2589fce28
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Envoi de données Web à Edge avec le SDK Web de Adobe Experience Platform

À partir de la version 2.20.0, le composant `streamingMedia` du [SDK Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) de Adobe Experience Platform permet de collecter des données relatives aux sessions multimédia sur votre site Web. Les données collectées peuvent inclure des informations sur les lectures multimédia, les pauses, les fins et d’autres événements connexes.

Une fois les données collectées, vous pouvez les envoyer à Adobe Experience Platform et/ou Adobe Analytics pour générer des rapports. Cette fonctionnalité offre une solution complète pour effectuer le suivi et comprendre le comportement de consommation des médias sur votre site web.

Pour les clients qui utilisent le SDK Media JS, le SDK Web fournit un chemin de migration pour passer du SDK Media JS au SDK Web, tout en incluant la prise en charge des fonctionnalités Media JS existantes, telles que la gestion des événements multimédia.

## Conditions préalables {#prerequisites}

Pour utiliser le composant `streamingMedia` du SDK Web, les conditions préalables suivantes doivent être remplies :

* Avant d’envoyer des données multimédia en flux continu à Edge, suivez d’abord les étapes de la section [Installation du module complémentaire de collecte de médias en flux continu avec Edge Experience Platform](/help/implementation/edge/implementation-edge.md).
* Vérifiez que vous avez accès à Adobe Experience Platform et/ou Adobe Analytics.
* Vous devez utiliser le SDK Web version 2.20.0 ou ultérieure. Pour découvrir comment installer la dernière version, consultez la [présentation de l’installation du SDK Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview).
* Activez l’option **[[!UICONTROL Media Analytics]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** pour la banque de données que vous utilisez.
* Assurez-vous que le schéma utilisé par votre flux de données comprend les champs de schéma Media Collection.
* Configurez la fonction Média en flux continu dans la configuration du SDK Web, comme indiqué dans cette page, soit par l’ [extension de balise](#tag-extension) soit par l’ [bibliothèque JavaScript](#library).

Suivez les étapes décrites dans cette page pour migrer votre mise en oeuvre du module complémentaire Collection de médias en flux continu de Media JS vers le SDK Web.

### Étape 1 : installation du SDK Web Experience Platform

Consultez la [documentation dédiée](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) pour savoir comment installer le SDK Web sur vos propriétés web.

### Étape 2 : Configuration du composant SDK Web `streamingMedia`.

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

Vous devez plutôt configurer le composant `streamingMedia` dans le SDK Web comme illustré ci-dessous.

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

Pour plus d’informations sur la configuration du SDK Web `streamingMedia` composant [, consultez la ](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) documentation .

### Étape 3 : Obtention de l’instance de suivi multimédia lors de la migration à partir du SDK Media JS

Pour les clients qui utilisent le SDK Media JS, le SDK Web fournit un chemin de migration pour passer du SDK Media JS au SDK Web, tout en incluant la prise en charge des fonctionnalités Media JS existantes, telles que la gestion des événements multimédia.

[!DNL Web SDK] comprend une commande pour récupérer un outil de suivi Media Analytics. Vous pouvez utiliser cette commande pour créer une instance d’objet, puis, en utilisant les mêmes API que celles fournies par la [ bibliothèque Media JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), effectuer le suivi des événements de média.

Consultez la documentation [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getmediaanalyticstracker) pour obtenir des détails complets sur les méthodes prises en charge.

Le fragment de code ci-dessous montre comment récupérer l’instance de suivi multimédia dans Media JS.

```javascript
var tracker = ADB.Media.getInstance();
```

Utilisez plutôt la commande `getMediaAnalyticsTracker` du SDK Web pour obtenir le même résultat, comme illustré ci-dessous.

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

Toutes les méthodes d’assistance seront disponibles sur l’objet `Media`. Les méthodes de suivi sont disponibles sur l’instance de suivi, comme illustré ci-dessous.

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
