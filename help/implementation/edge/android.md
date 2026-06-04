---
title: Configuration d’Android pour les médias en flux continu
description: Configurez le SDK mobile Adobe Experience Platform sur Android pour envoyer des données de médias en flux continu à Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Configuration d’Android pour les médias en flux continu

L’extension Adobe Streaming Media for Edge Network (`EdgeMedia`) collecte les données de session multimédia dans votre application Android et les envoie vers Edge Network. Cette page traite de la configuration dans le code. Pour configurer le SDK par le biais d’une propriété mobile Balises à la place, voir [Configuration d’Android pour les médias en flux continu avec les balises](android-tags.md).

* **Conditions préalables** :
   * Terminez la présentation de l’implémentation d’[](overview.md) (schéma, jeu de données, flux de données avec [!UICONTROL Media Analytics] activé).
   * Ajoutez les extensions `Core`, `Edge`, `EdgeIdentity` et `EdgeMedia` à votre application. Voir [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) pour l’installation et l’enregistrement.

## Configuration de médias pour Android

Définissez les clés de configuration du média lors de l’initialisation du SDK :

```kotlin
val configuration = mapOf(
  "edgeMedia.channel" to "sample_channel",
  "edgeMedia.playerName" to "player_name",
  "edgeMedia.appVersion" to "app_version"
)
MobileCore.updateConfiguration(configuration)
```

Créez ensuite un dispositif de suivi pour gérer une session multimédia :

```kotlin
val tracker = Media.createTracker()
```

Pour les clés de configuration et l’API de suivi complet, consultez la référence de l’API [Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Suivi des événements multimédia

Une fois le dispositif de suivi créé, suivez chaque événement multimédia à l’aide de sa méthode de suivi. Voir l’onglet **** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les appels exacts.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations d’Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configuration d’Android pour les médias en flux continu avec les balises](android-tags.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
