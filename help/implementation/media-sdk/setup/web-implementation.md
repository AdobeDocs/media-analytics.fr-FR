---
title: Comment configurer l’implémentation web pour Analytics for Streaming Media
description: Découvrez comment implémenter Adobe Streaming Media pour les applications web.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 92%

---

# Installation de Media SDK à l’aide de JavaScript {#install-web-sdks}

Les informations de cette page décrivent comment installer le SDK autonome web et configurer JavaScript.

Vous pouvez également utiliser l’extension Adobe Media Analytics pour implémenter des services de médias en flux continu, comme décrit dans la section [Installation de services de médias en flux continu à l’aide de l’extension Media Analytics](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Conditions préalables {#prerequesites}

* **Obtenir des paramètres de configuration valides**

  Vous pouvez obtenir ces paramètres auprès d’un représentant Adobe une fois votre compte d’analyse configuré.

* **Implémenter `AppMeasurement` et `Experience Cloud Identity Service` pour JavaScript dans votre application multimédia**

  Pour plus d’informations, consultez [Implémentation d’Analytics avec JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=fr) et [Implémentation du service d’identité Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=fr).

* **Incluez les API suivantes dans votre lecteur multimédia**

   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.
   * *Une API qui fournit des informations sur le lecteur* - Elle inclut des informations sur les médias en cours de lecture, les publicités et le chapitre.

## Configurer JavaScript 3.x {#set-up-javascript}

1. Ajoutez la bibliothèque que vous avez [téléchargée](/help/getting-started/download-sdks.md) à votre projet. Créez des références locales aux classes pour des raisons pratiques.

   1. Développez le fichier `MediaSDK-js-v3*.zip` que vous avez téléchargé.
   1. Vérifiez que le répertoire `libs` contient le fichier `MediaSDK.js`.

   1. Hébergez le fichier `MediaSDK.js`.

      Ce fichier JavaScript principal doit être hébergé sur un serveur web accessible par toutes les pages de votre site. Vous avez besoin du chemin d’accès à ces fichiers pour l’étape suivante.

   1. Référencez `MediaSDK.js` sur toutes les pages du site.

      Insérez `MediaSDK` pour JavaScript en ajoutant la ligne de code suivante dans la balise `<head>` ou `<body>` de chaque page. Par exemple :

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Pour vérifier rapidement que la bibliothèque a bien été importée, contrôlez que `ADB.Media` est exporté sur l’objet Window.

      >[!NOTE]
      >
      >Le SDK JavaScript est conforme aux spécifications du module AMD et CommonJS, et `MediaSDK.js` peut également être utilisé avec les chargeurs de module compatibles.

1. Créez une instance d’`AppMeasurement` et configurez `visitor`.

   La configuration du SDK Media requiert une instance d’`AppMeasurement` avec `visitor` configuré.

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. Configuration du SDK Media

   Le SDK Media doit être configuré une fois par page web, et la configuration s’applique à toutes les instances de dispositif de suivi créées.

   >[!IMPORTANT]
   >
   > Media SDK (3.x) utilise l’API Media Collection pour effectuer le suivi des médias, qui est distincte du point d’entrée HB utilisé dans les SDK 2.x. Prenez contact avec votre représentant Adobe pour obtenir plus d’informations.

   Voici un exemple d’initialisation de `MediaConfig` :

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
   ```

1. Créez l’instance `MediaTracker`.

   Après avoir configuré le SDK Media, il est possible de créer des instances de dispositifs de suivi du contenu multimédia à l’aide de l’API `getInstance`.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Assurez-vous que votre instance `tracker` est accessible et reste attribuée jusqu’à la fin de la session multimédia. Cette instance sera utilisée pour effectuer le suivi de tous les événements suivants pour cette session.

## Migration de JavaScript 2.x vers 3.x

Pour plus d’informations sur la migration de 2.x vers 3.x, voir [Migration de 2.x vers 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

Pour le contenu hérité, consultez [Implémentations héritées](/help/legacy/media-sdk/setup/setup-overview.md).
