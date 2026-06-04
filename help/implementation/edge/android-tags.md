---
title: Configuration d’Android pour les médias en flux continu avec les balises
description: Configurez la collecte de médias en flux continu pour Android à l’aide de l’extension de balise Adobe Streaming Media for Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 1%

---

# Configuration d’Android pour les médias en flux continu avec les balises

Vous pouvez configurer la collecte de médias en flux continu pour votre application Android par le biais d’une propriété mobile Balises. Les paramètres de médias sont gérés dans l’interface utilisateur de collecte de données. Cette page couvre la configuration Balises. Pour configurer le SDK dans le code à la place, voir [Configurer Android pour les médias en flux continu](android.md).

* **Conditions préalables** :
   * Terminez la présentation de l’implémentation d’[](overview.md) (schéma, jeu de données, flux de données avec [!UICONTROL Media Analytics] activé).
   * Créez une propriété mobile dans l’interface utilisateur de collecte de données. Voir [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/).

## Configurez l’extension

1. Dans l’interface utilisateur de collecte de données, ouvrez votre propriété mobile et sélectionnez **[!UICONTROL Extensions]**.
1. Dans l’onglet **[!UICONTROL Catalogue]**, recherchez l’extension **Adobe Streaming Media for Edge Network** et sélectionnez **[!UICONTROL Installer]**.
1. Définissez les éléments suivants, puis enregistrez :
   * **[!UICONTROL Canal]** : nom du canal signalé pour chaque session.
   * **[!UICONTROL Nom du lecteur]** : nom du lecteur multimédia utilisé.
   * **[!UICONTROL Version de l’application]** : la version de votre application de lecteur.
1. Publiez vos modifications, puis ajoutez les dépendances `Core`, `Edge`, `EdgeIdentity` et `EdgeMedia` à votre application et enregistrez-les avec Mobile Core.

## Suivi des événements multimédia

Une fois la propriété publiée et le dispositif de suivi créé, suivez chaque événement multimédia à l’aide de sa méthode de suivi. Voir l’onglet **** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les appels exacts.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations d’Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configuration d’Android pour les médias en flux continu (dans le code)](android.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
