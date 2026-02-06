---
title: Comment configurer le SDK Media pour Chromecast
description: Pour configurer l’application du SDK Media sur Chromecast, procédez comme suit.
uuid: d664e394-02a2-4985-bbad-be1bcc44fb2b
exl-id: 5dfe3407-2858-48c0-a70c-8ea87967ac47
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 97%

---

# Configurer le SDK mobile v3.x pour Chromecast {#set-up-chromecast}

Cette section décrit les conditions préalables à la configuration d’une installation Chromecast pour les services de streaming multimédia Adobe.

## Conditions préalables

* **Obtenir des paramètres de configuration valides**

  Vous pouvez obtenir ces paramètres auprès d’un représentant Adobe une fois votre compte Media Analytics configuré.
* **Inclure les API suivantes dans votre lecteur multimédia**

   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.
   * *Une API qui fournit des informations au lecteur* - Ces informations incluent des éléments tels que le nom du média et la position de la tête de lecture.

Adobe Mobile Services offre une nouvelle interface utilisateur qui réunit les fonctionnalités de marketing mobile pour les applications mobiles issues d’Adobe Experience Cloud. Au départ, le service Mobile intègre de manière transparente les fonctionnalités d’analyse et de ciblage des applications pour les solutions Adobe Analytics et Adobe Target. Pour en savoir plus, consultez la [Documentation d’Adobe Mobile Services.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=fr)

La bibliothèque mobile Adobe pour Chromecast v3.x pour les solutions Experience Cloud vous permet de mesurer les applications Chromecast écrites en JavaScript, d’exploiter et de collecter les données d’audience grâce à la gestion de l’audience et de mesurer l’engagement vidéo.

## Mise en œuvre de la bibliothèque/du SDK mobile

1. Ajoutez la bibliothèque Chromecast que vous avez téléchargée à votre projet.

   1. Le fichier `AdobeMobileLibrary-Chromecast-[version]`.zip est constitué des composants logiciels suivants :

      * `adbmobile-chromecast.min.js` :

        Ce fichier de bibliothèque sera inclus dans le dossier source de votre application Chromecast.

      * Fichier de configuration `ADBMobileConfig`

        Ce fichier de configuration SDK est personnalisé pour votre application. Un exemple de mise en œuvre `ADBMobileConfig` est fourni avec le SDK (sous `samples/`). Obtenez les paramètres appropriés auprès d’un représentant Adobe.

   1. Ajoutez le fichier de bibliothèque à votre fichier `index.html` et créez la variable globale `ADBMobileConfig` comme suit (la variable globale utilisée pour configurer Adobe Mobile pour Media Analytics comporte une clé exclusive appelée `mediaHeartbeat`) :

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
              "rsids": "example.sample.player",
              "server": "example.sc.omtrc.net",
              "ssl": true,
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
              "server": "example.hb-api.omtrdc.net",
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg",
              "channel": "test-channel-chromecast",
              "ssl": true,
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
      >Si `mediaHeartbeat` n’est pas correctement configuré, le module multimédia passe en état d’erreur et arrête l’envoi des appels de suivi.

      Paramètres de configuration ADBMobile pour la clé mediaHeartbeat :

   | Paramètre de configuration | Description     |
   | --- | --- |
   | `server` | Chaîne représentant l’URL du point d’entrée de suivi sur le serveur principal. |
   | `publisher` | Chaîne représentant l’identifiant unique de l’éditeur de contenu. |
   | `channel` | Chaîne représentant le nom du canal de distribution du contenu. |
   | `ssl` | Valeur booléenne qui indique si SSL doit être utilisé pour le suivi des appels. |
   | `ovp` | Chaîne représentant le nom du fournisseur de lecteur vidéo. |
   | `sdkversion` | Chaîne représentant la version actuelle de l’application/du kit SDK. |
   | `playerName` | Chaîne représentant le nom du lecteur. |


1. Configurez l’identifiant visiteur Experience Cloud.

   Le service d’identification des visiteurs Experience Cloud fournit un identifiant visiteur universel pour toutes les solutions Experience Cloud. Le service d’identifiant visiteur est requis par Media Analytics et d’autres intégrations Marketing Cloud.

   Vérifiez que votre configuration `ADBMobileConfig` contient votre ID d’organisation `marketingCloud`.

   ```
   "marketingCloud": {
       "org": "YOUR-MCORG-ID"
   }
   ```

   Les identifiants d’organisation d’Experience Cloud identifient de manière unique chaque entreprise cliente dans Adobe Experience Cloud et ressemblent à ceci : `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Veillez à inclure `@AdobeOrg`.

   Une fois la configuration terminée, un identifiant visiteur Experience Cloud est généré et inclus sur tous les accès. D’autres identifiants visiteur, tels que `custom` et `automatically-generated`, continuent à être envoyés avec chaque accès.

   **Méthodes du service d’identifiant visiteur Experience Cloud**

   >[!TIP]
   >
   >Les méthodes d’identification des visiteurs Experience Cloud sont précédées du préfixe `visitor`.

   | Méthode | Description |
   | --- | --- |
   | `getMarketingCloudID()` | Récupère l’identifiant visiteur Experience Cloud auprès du service d’identification des visiteurs.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | Avec l’identifiant visiteur d’Experience Cloud, vous pouvez définir d’autres identifiants de client qui peuvent être associés à chaque visiteur. L’API visiteur accepte plusieurs identifiants de client pour un même visiteur, ainsi qu’un identifiant de type client, afin de séparer la portée des différents identifiants de client. Cette méthode correspond aux identifiants `setCustomerIDs()` dans la bibliothèque JavaScript.  Par exemple : <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |

1. Pour le suivi des médias, mettez en œuvre le protocole MediaDelegate.

   ```js
    var delegate = {
      // Replace <currentPlaybackTime> with the video player current playback time
      getCurrentPlaybackTime = function() {
        return <currentPlaybackTime>;
      },
      // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.
      getQoSObject = function() {
         return ADBMobile.media.createQoSObject(<bitrate>, <startupTime>, <fps>, <droppedFrames>);
      }
    }
   
    ADBMobile.media.setDelegate(delegate);
   }
   ```

<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
