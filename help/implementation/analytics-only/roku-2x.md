---
title: Configuration de Roku 2.x pour les médias en flux continu
description: Installez et configurez Adobe Media SDK 2.x pour Roku pour les implémentations de médias en flux continu Analytics uniquement, y compris les canaux SceneGraph.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Configuration de Roku 2.x pour les médias en flux continu

Adobe Media SDK 2.x pour Roku (`adbmobile.brs`) envoie des données de médias en flux continu depuis des canaux Roku écrits en BrightScript directement à Adobe Analytics. Il collecte également des données d’audience via Audience Manager et mesure l’engagement par le biais d’événements multimédia.

>[!NOTE]
>
>Cette page couvre l’application Media SDK 2.x pour Roku réservée à Analytics. Pour les nouvelles mises en œuvre, Adobe recommande le [SDK Roku Edge](/help/implementation/edge/roku.md), qui met les données à la disposition de Customer Journey Analytics, Adobe Journey Optimizer et Real-Time CDP en plus d’Adobe Analytics.

* **Conditions préalables** :
   * Terminez la [présentation de l’implémentation pour Analytics uniquement](overview.md).
   * [Téléchargez Media SDK for Roku](/help/getting-started/download-sdks.md).
   * Incluez une API dans votre lecteur multimédia pour vous abonner aux événements du lecteur, ainsi qu’une API qui fournit des informations sur le lecteur telles que le nom du média et la position de la tête de lecture.

## Installation du SDK

Le téléchargement `AdobeMobileLibrary-2.*-Roku.zip` contient deux composants :

* `adbmobile.brs` : le fichier de bibliothèque. Copiez-le dans le répertoire `pkg:/source/` de votre canal.
* `ADBMobileConfig.json` : le fichier de configuration SDK, personnalisé pour votre application .

Pour les canaux SceneGraph, copiez également `adbmobileTask.brs` et `adbmobileTask.xml` dans votre répertoire `pkg:/components/`. Voir [Prise en charge de SceneGraph](#scenegraph).

## Configuration d’ADBMobileConfig.json

La configuration JSON dispose d’une clé `mediaHeartbeat` exclusive pour les médias en flux continu. Ajoutez des `ADBMobileConfig.json` à la source de votre projet et définissez les valeurs `mediaHeartbeat`, `marketingCloud` et `analytics` :

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| Paramètre de configuration | Description |
| --- | --- |
| `server` | URL du point d’entrée de suivi multimédia. Consultez la [présentation de l’implémentation pour Analytics uniquement](overview.md). |
| `publisher` | Identifiant unique de l’éditeur de contenu. |
| `channel` | Nom du canal de distribution du contenu. Signalé comme [&#x200B; canal de contenu &#x200B;](/help/implementation/variables/core/content-channel.md). |
| `ssl` | Indique si SSL est utilisé pour le suivi des appels. |
| `ovp` | Nom du fournisseur de plateformes vidéo en ligne. |
| `sdkVersion` | Version actuelle de votre application ou SDK. |
| `playerName` | Nom du lecteur. Signalé comme [Nom du lecteur de contenu](/help/implementation/variables/core/content-player-name.md). |

>[!IMPORTANT]
>
>Si `mediaHeartbeat` n’est pas correctement configuré, le module multimédia passe en état d’erreur et arrête l’envoi des appels de suivi. Assurez-vous que la valeur `marketingCloud.org` inclut `@AdobeOrg`.

## Initialiser le SDK et traiter les messages

Obtenez une instance du SDK avec `ADBMobile()`. Le service d’identification des visiteurs Experience Cloud génère un identifiant visiteur inclus dans tous les accès.

>[!IMPORTANT]
>
>Appelez `processMessages` et `processMediaMessages` dans votre boucle d’événement principale toutes les 250 ms afin que le SDK envoie correctement les pings.

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| Méthode | Description |
| --- | --- |
| `processMessages` | Transmet les événements Analytics mis en file d’attente au SDK. |
| `processMediaMessages` | Transmet les événements multimédias en file d’attente au SDK, y compris les pings automatiques. |

## Suivi des événements multimédia

Suivez chaque événement multimédia en appelant sa méthode SDK. Voir l’onglet **Roku 2.x** sur chaque page [event](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les appels, les générateurs et les constantes exacts.

Une session type commence par créer un objet multimédia et appelle `mediaTrackSessionStart` :

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

Les créateurs de `adb_media_init_*` globaux créent les objets de média, d’annonce, de coupure publicitaire, de chapitre et de QoS utilisés par les appels de suivi :

| Constructeur | Signature |
| --- | --- |
| Média | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| Publicité | `adb_media_init_adinfo(name, id, position, length)` |
| Arrêt de la publicité | `adb_media_init_adbreakinfo(name, startTime, position)` |
| Chapitre | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

Les métadonnées standard sont transmises sous la forme d’un tableau associatif de clés `a.media.*` (le SDK définit également des constantes nommées telles que les `MEDIA_VideoMetadataKeySHOW` pour ces clés). Reportez-vous aux pages [Variables](/help/implementation/variables/overview.md) pour la clé qui correspond à chaque dimension.

## Configuration de l’identifiant visiteur, de la confidentialité et de la journalisation Experience Cloud

Les méthodes suivantes sur l’instance `ADBMobile()` gèrent l’identité, la confidentialité et le débogage :

| Méthode | Description |
| --- | --- |
| `visitorMarketingCloudID()` | Récupère l’Experience Cloud ID (ECID). |
| `visitorSyncIdentifiers(identifiers)` | Définit des ID de client supplémentaires pour le même visiteur. |
| `setAdvertisingIdentifier(rida)` | Définit l’identifiant Roku pour Advertising (RIDA). Obtenez-le avec l’API Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic). |
| `getAllIdentifiers()` | Renvoie tous les identifiants stockés par le SDK, y compris les identifiants Analytics, Visiteur, Audience Manager et personnalisés. |
| `setPrivacyStatus(status)` | Définit le statut de confidentialité. Transmettez `adb.PRIVACY_STATUS_OPT_IN` ou `adb.PRIVACY_STATUS_OPT_OUT`. Voir [&#x200B; Confidentialité &#x200B;](/help/implementation/opt-out-privacy.md). |
| `getPrivacyStatus()` | Renvoie le statut de confidentialité actuel. |
| `setDebugLogging(flag)` | Active ou désactive la journalisation du débogage. |
| `getDebugLogging()` | Renvoie `true` si l’enregistrement de débogage est activé. |

## Prise en charge de SceneGraph {#scenegraph}

Le framework XML SceneGraph de Roku ne peut pas appeler directement les API SDK BrightScript héritées, car SDK utilise des composants (tels que des threads) qui ne sont pas disponibles pour une application SceneGraph. Pour combler cette lacune, SDK fournit un connecteur qui renvoie une instance compatible avec SceneGraph exposant les mêmes API, ainsi qu’un mécanisme de rappel pour les API qui renvoient des données.

Le pont se divise en trois parties :

* **`adbmobileTask`nœud** : nœud de tâche SceneGraph qui exécute les API SDK sur un thread d’arrière-plan et renvoie les données à vos scènes.
* **Instance de connecteur** : enveloppe toutes les API publiques héritées et communique avec le nœud `adbmobileTask`.
* **`API_RESPONSE`de rappel** : champ observé par votre application pour recevoir des valeurs de retour des API getter.

Pour initialiser le SDK dans un canal SceneGraph :

1. Importez les `adbmobile.brs` dans votre scène :

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. Créez le nœud `adbmobileTask`, récupérez l’instance du connecteur et chargez les constantes SceneGraph :

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. Enregistrez un rappel pour recevoir des objets de réponse pour les API qui renvoient des données :

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

L’instance de connecteur (`m.adbmobile`) expose les mêmes méthodes de média que le SDK hérité (`mediaTrackSessionStart`, `mediaTrackPlay`, `mediaTrackPause`, `mediaTrackComplete`, `mediaTrackSessionEnd`, `mediaTrackError`, `mediaTrackEvent`, `mediaUpdatePlayhead` et `mediaUpdateQoS`), de sorte que les appels affichés sur les pages d’événement et de variable fonctionnent de la même manière. Les API Setter sont appelées directement ; les API getter renvoient leurs valeurs par le biais du rappel `API_RESPONSE`.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations Analytics uniquement](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Présentation des événements](/help/implementation/events/overview.md)
>* [Présentation des variables](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
