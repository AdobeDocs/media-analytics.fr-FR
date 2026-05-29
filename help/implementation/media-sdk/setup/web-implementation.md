---
title: Comment configurer l’implémentation web pour Analytics for Streaming Media
description: Découvrez comment implémenter Adobe Streaming Media pour les applications web.
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
TQID: https://experienceleague.adobe.com/UBY26SeGZbGWHjwOm6-YZNET8fe5Gvvco7aIZ9Z7rZg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 78%

---

# Installation de Media SDK à l’aide de JavaScript {#install-web-sdks}

>[!IMPORTANT]
>
>Cette page traite de l’implémentation de JavaScript Web SDK réservée à Analytics. Pour connaître la mise en œuvre recommandée, voir [Implémentation de Streaming Media à l’aide d’Edge Network](/help/implementation/edge/edge-web-sdk.md).

Les informations de cette page décrivent comment installer le SDK autonome web et configurer JavaScript.

Vous pouvez également utiliser l’extension Adobe Media Analytics pour implémenter des services de médias en flux continu, comme décrit dans la section [Installation de services de médias en flux continu à l’aide de l’extension Media Analytics](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Conditions préalables {#prerequesites}

* **Obtenir des paramètres de configuration valides**

  Vous pouvez obtenir ces paramètres auprès d’un représentant Adobe une fois votre compte d’analyse configuré.

* **Implémenter `AppMeasurement` et `Experience Cloud Identity Service` pour JavaScript dans votre application multimédia**

  Pour plus d’informations, voir [Mise en œuvre d’Analytics avec JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=fr) et [Identification des visiteurs à l’aide d’AppMeasurement](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement).

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

Pour plus d’informations sur la migration de la version 2.x vers la version 3.x, voir [Migration de JS SDK 2.x vers la version 3.x](/help/implementation/media-sdk/setup/migrate-js-2x-to-3x.md).
