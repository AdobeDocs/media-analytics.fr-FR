---
seo-title: Configuration de Chromecast
title: Configuration de Chromecast
uuid: d 664 e 394-02 a 2-4985-bbad-be 1 bcc 44 fb 2 b
translation-type: tm+mt
source-git-commit: bb3a303edba724c8f444d612b3be9d7250eea363

---


# Configuration de Chromecast{#set-up-chromecast}

## FAQ

_Dois-je utiliser le SDK JavaScript Chromecast ou puis-je utiliser le SDK JavaScript standard ?_

La réponse correcte est « Chromecast » pour les raisons suivantes :
* Les bibliothèques AppMeasurement et VisitorAPI dans le SDK JS standard ne sont pas certifiées pour fonctionner sur les plates-formes OTT. Dans le SDK JS Chromecast, la bibliothèque Video Heartbeats (VHL), Analytics et VisitorAPI sont tous intégrés au SDK unique, unifié et certifié pour Chromecast.
* Le SDK Chromecast est bien plus léger que le SDK JS standard. Ce point est essentiel pour le matériel bas de gamme utilisé par les plates-formes OTT.

## Conditions préalables

* **Obtention des paramètres de configuration valides pour les pulsations**
Ces paramètres peuvent être obtenus auprès d'un représentant Adobe après avoir configuré votre compte Analytics.
* **Fournissez les fonctionnalités suivantes dans votre lecteur multimédia :**
   * *Une API pour vous abonner aux événements de lecteur* : Le kit SDK Media vous oblige à appeler une série d’API simples lorsque des événements ont lieu dans votre lecteur.
   * *Une API fournissant des informations sur le lecteur* : Ces informations comprennent des détails tels que le nom du média et la position du curseur de lecture.

Adobe Mobile Services offre une nouvelle interface utilisateur qui réunit les fonctionnalités de marketing pour les applications mobiles issues d’Adobe Experience Cloud. Au début, le service Mobile offrait une intégration transparente des fonctionnalités d’analyse et de ciblage d’applications issues des solutions Adobe Analytics et Adobe Target. Pour en savoir plus, consultez la [Documentation d’Adobe Mobile Services.](https://marketing.adobe.com/resources/help/en_US/mobile/)

Le kit SDK Chromecast 2.x pour les solutions Experience Cloud vous permet de mesurer les applications Chromecast écrites dans JavaScript, d’exploiter et de collecter les données des utilisateurs grâce à la gestion de l’audience, et de mesurer l’engagement vidéo au moyen de pulsations vidéo.

## Implémentation du SDK

1. Ajoutez la bibliothèque Chromecast que vous avez [téléchargée](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) à votre projet.

   1. Le fichier `AdobeMobileLibrary-Chromecast-[version]`.zip est constitué des composants logiciels suivants :

      * `adbmobile-chromecast.min.js`:

         Ce fichier de bibliothèque sera inclus dans le dossier source de votre application Chromecast.

      * `ADBMobileConfig` config

         Ce fichier de configuration SDK est personnalisé pour votre application. Un exemple de mise en œuvre `ADBMobileConfig` est fourni avec le SDK (sous `samples/`). Obtenez les paramètres appropriés auprès d’un représentant Adobe.
   1. Ajoutez le fichier de bibliothèque à votre fichier `index.html` et créez la variable globale `ADBMobileConfig` comme suit (la variable globale utilisée pour configurer Adobe Mobile for Heartbeats comporte une clé exclusive appelée `mediaHeartbeat`) :

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >If `mediaHeartbeat` is incorrectly configured, the media module (VHL) enters an error state and will stop sending tracking calls.

      Paramètres de configuration ADBMobile pour la clé mediaHeartbeat :
   | Paramètre de configuration | Description     |
   | --- | --- |
   | `server` | Chaîne représentant l’URL du point de terminaison de suivi sur le serveur principal. |
   | `publisher` | Chaîne représentant l’identifiant unique de l’éditeur de contenu. |
   | `channel` | Chaîne représentant le nom du canal de distribution du contenu. |
   | `ssl` | Valeur booléenne qui indique si SSL doit être utilisé pour le suivi des appels. |
   | `ovp` | Chaîne représentant le nom du fournisseur de lecteur vidéo. |
   | `sdkversion` | Chaîne représentant la version actuelle de l’application/du kit SDK. |
   | `playerName` | Chaîne représentant le nom du lecteur. |


1. Configurez l’identifiant visiteur Experience Cloud.

   Le service d’identifiant visiteur Experience Cloud fournit un identifiant visiteur universel pour toutes les solutions Experience Cloud. Le service d’identifiant visiteur est requis par Video Heartbeat et d’autres intégrations de Experience Cloud.

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   Une fois la configuration terminée, un identifiant visiteur Experience Cloud est généré et inclus sur tous les accès. Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Méthodes du service d’identifiant visiteur Experience Cloud**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | Méthode | Description |
   | --- | --- |
   | `getMarketingCloudID()` | Récupère l’identifiant visiteur Experience Cloud auprès du service d’identifiant visiteur.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Avec l’identifiant visiteur Experience Cloud, vous pouvez définir des identifiants de client supplémentaires pouvant être associés à chaque visiteur. L’API visiteur accepte plusieurs identifiants de client pour le même visiteur, ainsi qu’un identifiant de type Client, afin de séparer la portée des différents identifiants de client. Cette méthode correspond aux identifiants `setCustomerIDs()` dans la bibliothèque JavaScript.  For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

