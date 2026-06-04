---
title: Configuration de JavaScript pour les médias en flux continu
description: Installez et configurez Media SDK for JavaScript (3.x) pour les implémentations de médias en flux continu Analytics uniquement.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%

---

# Configuration de JavaScript pour les médias en flux continu

Media SDK for JavaScript (3.x) envoie directement des données de médias en flux continu à Adobe Analytics. Cette page traite de l’installation manuelle de JavaScript. Pour déployer le SDK par le biais de balises à la place, voir [Configuration de l’extension de balise Media Analytics](javascript-tags.md). Pour les nouvelles mises en œuvre, pensez à utiliser le [Web SDK](/help/implementation/edge/web-sdk.md) pour envoyer des données à Adobe Analytics par le biais d’un flux de données Edge Network.

* **Conditions préalables** :
   * Terminez la [présentation de l’implémentation pour Analytics uniquement](overview.md).
   * Implémentez [&#128279;](https://experienceleague.adobe.com/fr/docs/analytics/implementation/js/overview) et le [service d’identification des visiteurs](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement).
   * [Téléchargez Media SDK for JavaScript](/help/getting-started/download-sdks.md).

## Installation et configuration de SDK

1. Hébergez `MediaSDK.js` (à partir du répertoire `libs` téléchargé) sur un serveur web accessible à toutes les pages, et référencez-le sur chaque page :

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. Configurez Media SDK une fois par page, en transmettant l’instance `appMeasurement` que vous avez configurée comme condition préalable :

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >La variable `mediaConfig.trackingServer` est votre **serveur de collecte de médias** (par exemple, `[namespace].hb-api.omtrdc.net`). Ce serveur de collecte est distinct du serveur de suivi Analytics configuré dans l’instance AppMeasurement.

1. Créez une instance de suivi avec `getInstance`. Gardez l’instance accessible pour l’ensemble de la session multimédia :

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## Suivi des événements multimédia

Une fois le dispositif de suivi créé, suivez chaque événement multimédia à l’aide de sa méthode de suivi. Consultez l’onglet **Media SDK JS 3.x** sur chaque page [event](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les appels exacts.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations Analytics uniquement](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Référence de l’API Media SDK for JavaScript 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [Migration de JS SDK 2.x vers 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [Configurer l’extension de balise Media Analytics](javascript-tags.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
