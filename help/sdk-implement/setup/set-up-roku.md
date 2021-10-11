---
title: Comment configurer le SDK Media pour Roku
description: Suivez les étapes suivantes pour configurer lʼapplication du SDK Media sur Roku.
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e10f705e135cc6b9c630059596994d12fc787866
workflow-type: ht
source-wordcount: '716'
ht-degree: 100%

---

# Configuration de Roku{#set-up-roku}

## Conditions préalables

* **Obtention de paramètres de configuration valides pour Heartbeats** Vous pouvez vous procurer ces paramètres auprès d’un représentant Adobe après avoir configuré votre compte Media Analytics.
* **Fournissez les informations suivantes à votre lecteur multimédia :**
   * _Une API pour vous abonner aux événements du lecteur_ - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.
   * _Une API qui fournit des informations au lecteur_ - Ces informations incluent des éléments tels que le nom du média et la position de la tête de lecture.

Adobe Mobile Services offre une nouvelle interface utilisateur qui réunit les fonctionnalités de marketing mobile pour les applications mobiles issues d’Adobe Experience Cloud. Au départ, le service Mobile intègre de manière transparente les fonctionnalités d’analyse et de ciblage des applications pour les solutions Adobe Analytics et Adobe Target.

Pour en savoir plus, consultez la [Documentation d’Adobe Mobile Services.](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=fr)

Le kit SDK Roku 2.x pour les solutions Experience Cloud vous permet de mesurer les applications Roku écrites en BrightScript, d’exploiter et de collecter les données d’audience par le biais de la gestion de l’audience et de mesurer l’engagement vidéo grâce aux pulsations vidéo.

## Implémentation du SDK

1. Ajoutez la bibliothèque Roku que vous avez [téléchargée](/help/sdk-implement/download-sdks.md#download-2x-sdks) à votre projet.

   1. Le fichier de téléchargement `AdobeMobileLibrary-2.*-Roku.zip` est constitué des composants logiciels suivants :

      * `adbmobile.brs` : Ce fichier de bibliothèque sera inclus dans le dossier source de votre application Roku.

      * `ADBMobileConfig.json` : Ce fichier de configuration SDK est personnalisé pour votre application.
   1. Ajoutez le fichier de bibliothèque et le fichier de configuration JSON à la source de votre projet.

      Le fichier JSON utilisé pour configurer Adobe Mobile comporte une clé exclusive pour les pulsations multimédia appelée `mediaHeartbeat`. C’est à cet endroit que se trouvent les paramètres de configuration des pulsations multimédia.

      >[!TIP]
      >
      >Un exemple de fichier JSON `ADBMobileConfig` est fourni avec le module. Contactez vos représentants Adobe au sujet des paramètres.

      Par exemple :

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
          "offlineEnabled":false,
          "lifecycleTimeout":30,
          "batchLimit":50,
          "privacyDefault":"optedin",
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{
        "clientCode":"",
        "timeout":5
      },
      "audienceManager":{
        "server":""
      },
      "acquisition":{
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{
         "server":"example.com",
         "publisher":"sample-publisher",
         "channel":"sample-channel",
         "ssl":true,
         "ovp":"sample-ovp",
         "sdkVersion":"sample-sdk",
         "playerName":"roku"
         }    
      }
      ```

      | Paramètre de configuration | Description     |
      | --- | --- |
      | `server` | Chaîne représentant l’URL du point de terminaison de suivi sur le serveur principal. |
      | `publisher` | Chaîne représentant l’identifiant unique de l’éditeur de contenu. |
      | `channel` | Chaîne représentant le nom du canal de distribution du contenu. |
      | `ssl` | Valeur booléenne qui indique si SSL doit être utilisé pour le suivi des appels. |
      | `ovp` | Chaîne représentant le nom du fournisseur de lecteur vidéo. |
      | `sdkversion` | Chaîne représentant la version actuelle de l’application/du kit SDK. |
      | `playerName` | Chaîne représentant le nom du lecteur. |

      >[!IMPORTANT]
      >
      >Si `mediaHeartbeat` n’est pas correctement configuré, le module multimédia (VHL) entre dans un état d’erreur et arrête l’envoi des appels de suivi.


1. Configurez l’identifiant visiteur Experience Cloud.

   Le service d’identification des visiteurs Experience Cloud fournit un identifiant visiteur universel pour toutes les solutions Experience Cloud. Le service d’identification des visiteurs est requis par Video Heartbeat et d’autres intégrations Experience Cloud.

   Vérifiez que votre configuration `ADBMobileConfig` contient votre ID d’organisation `marketingCloud`.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
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

   |  Méthode   | Description |
   | --- | --- |
   | `visitorMarketingCloudID` | Récupère l’identifiant visiteur Experience Cloud auprès du service d’identification des visiteurs.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | Avec l’identifiant visiteur d’Experience Cloud, vous pouvez définir d’autres identifiants de client qui peuvent être associés à chaque visiteur. L’API visiteur accepte plusieurs identifiants de client pour un même visiteur, ainsi qu’un identifiant de type client, afin de séparer la portée des différents identifiants de client. Cette méthode correspond à `setCustomerIDs`. Par exemple : <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | Utilisé pour définir l’ID de Roku pour la publicité (RIDA) sur le SDK. Par exemple : <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>Obtenez l’ID Roku pour la publicité (RIDA) à l’aide de l’API [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) du SDK Roku. |
   | `getAllIdentifiers` | Renvoie une liste de tous les identifiants stockés par le SDK, y compris les identifiants Analytics, Visiteur, Audience Manager et personnalisés. <br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   <br/><br/>

   **API publiques supplémentaires**

   **DebugLogging**
|  Method   | Description |
| --- | --- |
| `setDebugLogging` | Utilisé pour activer ou désactiver l’enregistrement de débogage pour le SDK.  <br/><br/>`ADBMobile().setDebugLogging(true)` |
| `getDebugLogging` | Renvoie true si l’enregistrement de débogage est activé.  <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   <br/><br/>

   **PrivacyStatus**
|  Constant   | Description |
| --- | --- |
| `PRIVACY_STATUS_OPT_IN` | Constante à transmettre lors de l’appel de setPrivacyStatus pour l’opt-in. <br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN`|
| `PRIVACY_STATUS_OPT_OUT` | Constante à transmettre lors de l’appel de setPrivacyStatus pour l’opt-out. <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT`|

   <br/>

   |  Méthode   | Description |
   | --- | --- |
   | `setPrivacyStatus` | Définit le statut de confidentialité sur le SDK. <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | Obtient le statut de confidentialité actuel défini sur le SDK. <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   <br/><br/>
   >[!IMPORTANT]
   >
   >Veillez à appeler les fonctions `processMessages` et `processMediaMessages` dans la boucle d’événement principale toutes les 250 ms pour vous assurer que le SDK envoie correctement les pings.

   |  Méthode   | Description |
   | --- | --- |
   | `processMessages` | Responsable de la transmission des événements Analytics au SDK à gérer.  <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | Responsable de la transmission des événements Media au SDK à gérer. <br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
