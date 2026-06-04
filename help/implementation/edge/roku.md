---
title: Configuration de Roku pour les médias en flux continu
description: Configurez le SDK Roku de Adobe Experience Platform pour envoyer des données de médias en flux continu à Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Configuration de Roku pour les médias en flux continu

Le [SDK Roku Adobe Experience Platform](https://github.com/adobe/aepsdk-roku) (BrightScript) collecte les données de session multimédia dans votre canal Roku et les envoie à Edge Network. Roku est configuré dans le code ; il n’utilise pas de balises.

* **Conditions préalables** :
   * Terminez la présentation de l’implémentation d’[&#128279;](overview.md) (schéma, jeu de données, flux de données avec [!UICONTROL Media Analytics] activé).
   * Téléchargez le SDK à partir des [versions de GitHub](https://github.com/adobe/aepsdk-roku/releases) et ajoutez-le à votre canal, comme décrit dans le [guide de prise en main](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md).

## Configuration d’AEP Roku SDK pour les médias

Initialisez le SDK et définissez la configuration du flux de données et du média :

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

Ouvrez ensuite une session avec `createMediaSession` :

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>Envoyez un événement `media.ping` au moins une fois par seconde avec la dernière valeur du curseur de lecture pendant la lecture. Le SDK Roku d’AEP s’appuie sur ces pings pour fonctionner correctement.

Pour les clés de configuration et l’API complète, consultez la [référence de l’API AEP Roku SDK](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md).

## Suivi des événements multimédia

Une fois la session ouverte, envoyez chaque événement multimédia avec `sendMediaEvent`. Voir l’onglet **Roku** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les payloads exactes.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations d’Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [Présentation des événements](/help/implementation/events/overview.md)
>* [Présentation des variables](/help/implementation/variables/overview.md)
