---
title: Configuration d’iOS pour les médias en flux continu
description: Configurez le SDK mobile Adobe Experience Platform sur iOS pour envoyer des données de médias en flux continu à Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Configuration d’iOS pour les médias en flux continu

L’extension Adobe Streaming Media for Edge Network (`AEPEdgeMedia`) collecte les données de session multimédia dans votre application iOS ou tvOS et les envoie à Edge Network. Cette page traite de la configuration dans le code. Pour configurer le SDK par le biais d’une propriété mobile Balises à la place, voir [Configuration d’iOS pour les médias en flux continu avec les balises](ios-tags.md).

* **Conditions préalables** :
   * Terminez la présentation de l’implémentation d’[](overview.md) (schéma, jeu de données, flux de données avec [!UICONTROL Media Analytics] activé).
   * Ajoutez les extensions `AEPCore`, `AEPEdge`, `AEPEdgeIdentity` et `AEPEdgeMedia` à votre application. Voir [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) pour l’installation et l’enregistrement.

## Configuration de médias pour iOS

Définissez les clés de configuration du média lors de l’initialisation du SDK :

```swift
let configuration = [
  "edgeMedia.channel": "sample_channel",
  "edgeMedia.playerName": "player_name",
  "edgeMedia.appVersion": "app_version"
]
MobileCore.updateConfiguration(configuration)
```

Créez ensuite un dispositif de suivi pour gérer une session multimédia :

```swift
let tracker = Media.createTracker()
```

Pour les clés de configuration et l’API de suivi complet, consultez la référence de l’API [Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Suivi des événements multimédia

Une fois le dispositif de suivi créé, suivez chaque événement multimédia à l’aide de sa méthode de suivi. Voir l’onglet **** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les appels exacts.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations d’Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configuration d’iOS pour les médias en flux continu avec les balises](ios-tags.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
