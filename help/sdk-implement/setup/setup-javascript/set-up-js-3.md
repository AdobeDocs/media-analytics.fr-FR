---
title: Configuration de JavaScript 3.x
description: Configuration de l’application SDK Media pour l’implémentation sur JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 83b38ac8f7fc88f982d194e776efccf8d5b983e4
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 47%

---


# Configuration de JavaScript 3.x{#set-up-javascript}

## Conditions préalables

* **Obtention de paramètres de configuration valides** Vous pouvez vous procurer ces paramètres auprès d’un représentant Adobe après avoir configuré votre compte Analytics.
* **Mise en oeuvre`AppMeasurement`et`Experience Cloud Identity Service`pour JavaScript dans votre application** multimédia Pour plus d’informations, voir [Mise en oeuvre d’Analytics à l’aide de JavaScript](https://docs.adobe.com/content/help/fr-FR/analytics/implementation/js/overview.html) et [Mise en oeuvre d’Experience Cloud Identity Service.](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **Fournissez les informations suivantes à votre lecteur multimédia :**

   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.
   * *Une API qui fournit des informations* sur le lecteur - Elle inclut des informations sur les médias en cours de lecture, les publicités et le chapitre.

1. Ajoutez la bibliothèque que vous avez [téléchargée](/help/sdk-implement/download-sdks.md#download-3x-sdks) à votre projet. Créez des références locales aux classes pour des raisons pratiques.

   1. Développez le fichier `MediaSDK-js-v3*.zip` que vous avez téléchargé.
   1. Vérifiez que le répertoire `libs` contient le fichier `MediaSDK.js`.

   1. Hébergez le fichier `MediaSDK.js`.

      Ce fichier JavaScript principal doit être hébergé sur un serveur web accessible par toutes les pages de votre site. Vous avez besoin du chemin d’accès à ces fichiers pour l’étape suivante.

   1. Référencez `MediaSDK.js` sur toutes les pages du site.

      Insérez `MediaSDK` pour JavaScript en ajoutant la ligne de code suivante dans la balise `<head>` ou `<body>` de chaque page. Par exemple :

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Pour vérifier rapidement que la bibliothèque a bien été importée, la vérification `ADB.Media` est exportée sur l’objet Window.

      >[!NOTE]
      >
      >The JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `MediaSDK.js` can also be used with compatible module loaders.

1. Créez une instance de `AppMeasurement` et configurez `visitor`.

   La configuration du SDK multimédia requiert une instance de `AppMeasurement` avec `visitor` configuré.

```js
var appMeasurement = new AppMeasurement(“<rsid>”);
appMeasurement.visitor = visitor;
appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
```

1. Configuration du SDK multimédia

   Le SDK multimédia doit être configuré une fois par page Web et la configuration s’applique à toutes les instances d’outil de suivi créées.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) utilise l’API Media Collection pour le suivi des médias, qui est différent du point de terminaison HB utilisé dans les SDK 2.x. Contactez votre représentant Adobe pour obtenir plus d’informations.


   Voici un exemple d’ `MediaConfig` initialisation :

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   
1. Créez l’instance `MediaTracker`.

   Après avoir configuré le SDK multimédia, il est possible de créer des instances d’outil de suivi du contenu multimédia à l’aide de `getInstance` l’API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Assurez-vous que votre instance `tracker` est accessible et reste attribuée jusqu’à la fin de la session multimédia. Cette instance sera utilisée pour effectuer le suivi de tous les événements suivants pour cette session.

## Migration de JavaScript 2.x vers 3.x

Pour plus d’informations sur la migration de 2.x vers 3.x, voir [Migration de  2.x vers 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)
