---
title: Mise en oeuvre du module complémentaire Collection de médias en flux continu à l’aide de l’Edge Network
description: Découvrez comment le module complémentaire de collecte de médias en flux continu peut être mis en oeuvre avec Edge Experience Platform.
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 9%

---

# Mise en oeuvre du module complémentaire Collection de médias en flux continu à l’aide de l’Edge Network

Le réseau Edge d&#39;Adobe Experience Platform vous permet d’envoyer des données destinées à plusieurs produits vers un emplacement centralisé. Experience Edge transfère les informations appropriées aux produits souhaités. Ce concept vous permet de consolider les efforts de mise en œuvre, en particulier sur plusieurs solutions de données.

Le graphique suivant illustre la manière dont le module complémentaire de collecte de médias en flux continu Adobe peut être mis en oeuvre pour utiliser Edge Experience Platform afin de rendre les données disponibles dans Analysis Workspace, que ce soit dans Adobe Analytics ou dans Customer Journey Analytics :

![Workflow CJA](assets/streaming-media-edge.png)

Pour une présentation de toutes les options de mise en oeuvre, y compris les méthodes de mise en oeuvre qui n’utilisent pas Edge Experience Platform, voir [Mise en oeuvre du module complémentaire de collecte de médias en flux continu](/help/implementation/overview.md).

Que vous utilisiez le SDK Web de Adobe Experience Platform, le SDK Mobile de Adobe Experience Platform, le SDK Roku de Adobe Experience Platform ou l’API pour mettre en oeuvre le module complémentaire de collecte de médias en flux continu avec Experience Edge, vous devez d’abord suivre les sections suivantes :

## Configuration du schéma dans Adobe Experience Platform

Pour normaliser la collecte de données à utiliser dans les applications qui utilisent Adobe Experience Platform, Adobe a créé la norme ouverte et accessible au public, Modèle de données d’expérience (XDM).

Pour créer et configurer un schéma :

1. Dans Adobe Experience Platform, commencez à créer le schéma comme décrit dans [Création et modification de schémas dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

1. Sur la page des détails du schéma lors de la création du schéma, sélectionnez [!UICONTROL **Experience Event**] lors du choix de la classe de base pour le schéma.

   ![Ajout de groupes de champs](assets/schema-experience-event.png)

1. Sélectionnez [!UICONTROL **Suivant**].

1. Indiquez un nom d’affichage et une description du schéma, puis sélectionnez [!UICONTROL **Terminer**].

1. Dans la zone [!UICONTROL **Composition**], dans la section [!UICONTROL **Groupes de champs**], sélectionnez [!UICONTROL **Ajouter**], puis recherchez et ajoutez les nouveaux groupes de champs suivants au schéma :
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   Une fois les groupes de champs ajoutés, ils doivent s’afficher dans la section [!UICONTROL **Groupes de champs**], comme suit :

   ![Ajout de groupes de champs](assets/schema-field-groups-added.png)

1. Sélectionnez [!UICONTROL **Enregistrer**] pour enregistrer vos modifications.

1. (Facultatif) Vous pouvez masquer certains champs qui ne sont pas utilisés par l’API Media Edge. Le masquage de ces champs facilite la lecture et la compréhension du schéma, mais il n’est pas obligatoire. Ces champs font uniquement référence à ceux du groupe de champs `MediaAnalytics Interaction Details`.

+++ Développez ici pour afficher des instructions sur les champs que vous pouvez masquer.

   1. Dans la zone [!UICONTROL **Structure**], sélectionnez le champ `Media Collection Details`, puis sélectionnez [!UICONTROL **Gérer les champs associés**].

      ![manage-related-fields](assets/manage-related-fields.png)

   1. Activez l’option [!UICONTROL **Afficher les noms d’affichage pour les champs**], puis mettez à jour le schéma comme suit :

      * Dans le champ `Media Collection Details` > `Advertising Details` , masquez les champs de création de rapports suivants : `Ad Completed`, `Ad Started` et `Ad Time Played`.

      * Dans le champ `Media Collection Details` > `Advertising Pod Details` , masquez le champ de rapport suivant : `Ad Break ID`

      * Dans le champ `Media Collection Details` > `Chapter Details` , masquez les champs de création de rapports suivants : `Chapter Completed`, `Chapter ID`, `Chapter Started` et `Chapter Time Played`.

      * Dans le champ `Media Collection Details` , masquez le champ `List Of States`.

        ![masquer les états de collection de médias](assets/schema-hide-media-collection-states.png)

      * Dans le champ `Media Collection Details` > `List Of States End` et `Media Collection Details` > `List Of States Start` , masquez les champs de création de rapports suivants : `Player State Count`, `Player State Set` et `Player State Time`.

        ![champs à masquer](assets/schema-hide-listofstates.png)

      * Dans le champ `Media Collection Details` > `Qoe Data Details`, masquez les champs de création de rapports suivants : `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Impacted Streams`, `Buffer Events`, `Dropped Frame Impacted Streams`, `Drops Before Starts`, `Errors`, `External Error IDs`, `Error Impacted Streams`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Impacted Streams`, `Stalling Events`, `Total Buffer Duration` et `Total Stalling Duration` 8}.

      * Dans le champ `Media Collection Details` > `Session Details`, masquez les champs de création de rapports suivants : `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Content Completes`, `Chapter Count`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Segment Views`, `Media Downloaded Flag`, `Media Starts`, `Media Session ID` 8}, `Media Session Server Timeout`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pev3`, `Pccr`, `Total Pause Duration`, `Unique Time Played` et `Video Segment`.

   1. Sélectionnez [!UICONTROL **Confirmer**] pour enregistrer vos modifications.

   1. Dans la zone [!UICONTROL **Structure**], activez l’option [!UICONTROL **Afficher les noms d’affichage des champs**], puis sélectionnez le champ `List Of Media Collection Downloaded Content Events`.

   1. Sélectionnez [!UICONTROL **Gérer les champs associés**], puis mettez à jour le schéma comme suit :


      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` , masquez les champs de création de rapports suivants : `Ad Completed`, `Ad Started` et `Ad Time Played`.

      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` , masquez le champ de création de rapports suivant : `Ad Break ID`

      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` , masquez les champs de création de rapports suivants : `Chapter Completed`, `Chapter ID`, `Chapter Started` et `Chapter Time Played`.

      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` , masquez le champ `List Of States` .

      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` et `Media Collection Details` > `List Of States Start` , masquez les champs de création de rapports suivants : `Player State Count`, `Player State Set` et `Player State Time`.

      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details`, masquez les champs de création de rapports suivants : `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Change Impacted Streams`, `Bitrate Changes`, `Buffer Events`, `Buffer Impacted Streams`, `Drops Before Starts`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Errors`, `External Error IDs`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`, `Stalling Impacted Streams`, `Total Buffer Duration` 8} et `Total Stalling Duration`.

      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details`, masquez les champs de création de rapports suivants : `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Content Completes`, `Content Starts`, `Content Time Spent`, `Estimated Streams`, `Federated Data`, `Media Downloaded Flag`, `Media Segment Views`, `Media Session ID` 8}, `Media Session Server Timeout`, `Media Starts`, `Media Time Spent`, `Pause Events`, `Pause Impacted Streams`, `Pccr`, `Pev3`, `Total Pause Duration`, `Unique Time Played` et `Video Segment`.

      * Dans le champ `List Of Media Collection Downloaded Content Events` > `Media Details` , masquez le champ `Media Session ID` .

   1. Sélectionnez [!UICONTROL **Confirmer**] pour enregistrer vos modifications.

   1. Dans la zone [!UICONTROL **Structure**], sélectionnez le champ `Media Reporting Details`, puis [!UICONTROL **Gérer les champs associés**].

   1. Activez l’option [!UICONTROL **Afficher les noms d’affichage pour les champs**], puis mettez à jour le schéma comme suit :

      * Dans le champ `Media Reporting Details` , masquez les champs suivants : `Error Details`, `List Of States End`, `List of States Start` et `Media Session ID`.

   1. Sélectionnez [!UICONTROL **Confirmer**] > [!UICONTROL **Enregistrer**] pour enregistrer vos modifications.

1. Poursuivez en [créant un jeu de données dans Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

## Création d’un jeu de données dans Adobe Experience Platform

1. Assurez-vous de configurer un schéma comme décrit dans [Configuration du schéma dans Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Dans Adobe Experience Platform, commencez à créer le jeu de données comme décrit dans le [guide de l’interface utilisateur des jeux de données](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=fr#create).

   Lors de la sélection d’un schéma pour votre jeu de données, choisissez le schéma que vous avez précédemment créé, comme décrit dans la section [Configuration du schéma dans Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform).

1. Passez à [Configuration d’un flux de données en Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

## Configuration d’un flux de données dans Adobe Experience Platform

1. Veillez à créer un jeu de données comme décrit dans [Création d’un jeu de données dans Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

1. Créez un flux de données comme décrit dans [Configuration d’un flux de données](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=fr).

   Lors de la création du flux de données, veillez à effectuer les sélections de configuration suivantes :

   * Dans le champ [!UICONTROL **Event Schema**] lors de la création de la banque de données, veillez à sélectionner le schéma que vous avez créé dans [Configuration du schéma dans Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform). Sélectionnez [!UICONTROL **Enregistrer**].

     >[!IMPORTANT]
     >
         >     Ne sélectionnez pas [!UICONTROL **Save and Add Mapping**], car cela entraînera des erreurs de mappage pour le champ Timestamp.
     
     ![Créer un flux de données et sélectionner un schéma](assets/datastream-create-schema.png)

   * Ajoutez l’un des services suivants au flux de données, selon que vous utilisez Adobe Analytics ou Customer Journey Analytics :

      * [!UICONTROL **Adobe Analytics**] (si vous utilisez Adobe Analytics)

        Si vous utilisez Adobe Analytics, veillez à définir une suite de rapports, comme décrit dans la section [Créer une suite de rapports](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

      * [!UICONTROL **Adobe Experience Platform**] (en cas d’utilisation de Customer Journey Analytics)

     Pour plus d’informations sur l’ajout d’un service à un flux de données, reportez-vous à la section &quot;Ajout de services à un flux de données&quot; dans [Configuration d’un flux de données](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![Ajout du service Adobe Analytics](assets/datastream-add-service.png)

   * Développez [!UICONTROL **Options avancées**], puis activez l’option [!UICONTROL **Media Analytics**].

     ![Option Media Analytics](assets/datastream-media-check.png)

1. Vous êtes maintenant prêt à mettre en oeuvre l’[ API Media Edge](/help/implementation/edge/implementation-edge-api.md) ou le [ SDK Media Edge](/help/implementation/edge/edge-mobile-sdk.md) pour commencer à collecter des données d’analyse multimédia.

   Une fois que vous avez collecté certaines données, vous pouvez [créer une connexion dans Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

## Créer une connexion dans Customer Journey Analytics

>[!NOTE]
>
>La procédure suivante n’est requise que si vous utilisez Customer Journey Analytics.


1. Veillez à créer un flux de données comme décrit dans [Configuration d’un flux de données dans Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform).

1. Dans Customer Journey Analytics, créez une connexion comme décrit dans [Créer une connexion](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=fr).

   Lors de la création de la connexion, les sélections de configuration suivantes sont requises pour la mise en oeuvre du module complémentaire Collection de médias en flux continu :

   1. Sélectionnez le jeu de données que vous avez précédemment créé, comme décrit dans [Création d’un jeu de données dans Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform).

   1. Assurez-vous que le paramètre [!UICONTROL **Importer toutes les nouvelles données**] est activé.

1. Poursuivez en [créant une vue de données dans Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

## Création d’une vue de données dans Customer Journey Analytics

>[!NOTE]
>
>La procédure suivante n’est requise que si vous utilisez Customer Journey Analytics.

1. Vérifiez que vous avez créé une connexion en Customer Journey Analytics comme décrit dans [Création d’une connexion en Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

1. Dans Customer Parcours Analytics, créez une vue de données comme décrit dans [Création ou modification d’une vue de données](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=fr).

   Lors de la création de la vue de données, les sélections de configuration suivantes sont requises pour la mise en oeuvre du module complémentaire Collection de médias en flux continu :

   1. Dans le champ [!UICONTROL **Connexion**] , sélectionnez la connexion que vous avez créée précédemment, comme décrit dans la section [Créer une connexion dans Customer Journey Analytics](#create-a-connection-in-customer-journey-analytics).

      La sélection de la connexion que vous avez créée peut prendre jusqu’à 15 minutes.

   1. Sur l’onglet [!UICONTROL **Composants**], dans la section [!UICONTROL **Champs de schéma**], recherchez chaque composant répertorié dans les tableaux ci-dessous et faites-le glisser dans le panneau [!UICONTROL **Mesures**]. S’il existe plusieurs champs portant le même nom, utilisez le chemin XDM pour vous assurer qu’il s’agit bien du champ.

      **Contenu principal - Mesures de contenu**

      | Nom du composant | Chemin XDM |
      |----------|---------|
      | Démarrage du contenu multimédia | mediaReporting.sessionDetails.isViewed |
      | Vues de segments du fichier multimédia | mediaReporting.sessionDetails.hasSegmentView |
      | Démarrages de contenu | mediaReporting.sessionDetails.isPlayed |
      | Le contenu se termine | mediaReporting.sessionDetails.isCompleted |
      | Temps passé sur le contenu | mediaReporting.sessionDetails.timePlayed |
      | Passé sur le média | mediaReporting.sessionDetails.totalTimePlayed |
      | Durée de lecture unique | mediaReporting.sessionDetails.uniqueTimePlayed |
      | Marqueur de progression de 10% | mediaReporting.sessionDetails.hasProgress10 |
      | Audience moyenne par minute | mediaReporting.sessionDetails.averageMinuteAudience |


      **Chapitre et publicités - Mesures de chapitre et publicités**

      | Nom du composant | Chemin XDM |
      |----------|---------|
      | Démarrage du chapitre | mediaReporting.chapterDetails.isStarted |
      | Chapitre terminé | mediaReporting.chapterDetails.isCompleted |
      | Durée de lecture des chapitres | mediaReporting.chapterDetails.timePlayed |
      | Publicité lancée | mediaReporting.advertisingDetails.isStarted |
      | Publicité terminée | mediaReporting.advertisingDetails.isCompleted |
      | Durée de lecture des publicités | mediaReporting.advertisingDetails.timePlayed |


      **QoE - mesures QoE**

      | Nom du composant | Chemin XDM |
      |----------|---------|
      | Temps jusqu’au début | mediaReporting.qoeDataDetails.timeToStart |
      | Pertes avant le début | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | Flux touchés par la mémoire tampon | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | Flux touchés par les changements de débit | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | Changements de débit | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | Débit moyen | mediaReporting.qoeDataDetails.bitrateAverage |
      | Perte d’images | mediaReporting.qoeDataDetails.droppedFrames |
      | Erreurs | mediaReporting.qoeDataDetails.errorCount |
      | Flux touchés par les erreurs | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | Flux touchés par la perte d’images | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |


      **État du lecteur - Mesures d’état du lecteur**

      | Nom du composant | Chemin XDM |
      |----------|---------|
      | Jeu d’états du lecteur | mediaReporting.states.isSet |
      | Nombre d’états du lecteur | mediaReporting.states.count |
      | Heure d’état du lecteur | mediaReporting.states.time |


   1. Mettez à jour les libellés (dans le menu déroulant [!UICONTROL **Étiquettes contextuelles**]) pour les composants du tableau suivant. Recherchez et faites glisser des composants qui ne se trouvent pas déjà dans le panneau des mesures dans le panneau.

      | Nom du composant | Libellé de contexte |
      |---------|----------|
      | Délai d’expiration du serveur de session multimédia | Média : secondes depuis le dernier appel |
      | Passé sur le média | Média : temps passé sur le média |
      | Durée totale de la mémoire tampon | Média : durée totale de la mémoire tampon |
      | Temps jusqu’au début | Média : temps jusqu’au début |
      | Durée totale de pause | Média : durée totale de pause |

   1. Pour ajouter des ventilations à votre projet Customer Journey Analytics, ajoutez les dimensions suivantes au panneau [!UICONTROL **Dimensions**] :

      | Chemin XDM | Nom du composant |
      |---------|----------|
      | mediaReporting.states.name | Nom de l’état du lecteur |
      | mediaReporting.sessionDetails.ID | ID de session multimédia |

      Outre les dimensions de ce tableau, vous pouvez ajouter toute autre dimension que vous souhaitez rendre disponible pour filtrer les données par dans les projets Customer Journey Analytics.

1. Sélectionnez [!UICONTROL **Enregistrer et continuer**] > [!UICONTROL **Enregistrer et terminer**] pour enregistrer vos modifications.

1. Passez à [Créer et configurer un projet en Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Création et configuration d’un projet dans Customer Journey Analytics

1. Vérifiez que vous avez créé une vue de données dans Customer Journey Analytics comme décrit dans [Création d’une vue de données dans Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

1. Dans Customer Journey Analytics, dans l’onglet [!UICONTROL **Workspace**], dans la zone [!UICONTROL **Projets**], sélectionnez [!UICONTROL **Créer un projet**].

1. Sélectionnez [!UICONTROL **Projet vierge**] > [!UICONTROL **Créer**].

1. Dans le nouveau projet, sélectionnez la vue de données que vous avez créée précédemment.

   Lors de la création de panneaux dans votre projet, vous pouvez utiliser tous les composants que vous avez ajoutés à votre vue de données, comme décrit dans la section [Création d’une vue de données dans Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics).

   Les 4 panneaux suivants constituent des exemples de panneaux que vous pouvez créer :

   ![Panneau Contenu principal](assets/main-content-panel.png)

   ![Panneau Chapitre et publicités](assets/chapter-and-ads-panel.png)

   ![Panneau QoE](assets/qoe-panel.png)

   ![Panneau d’état Plater](assets/player-state-panel.png)

1. Sélectionnez l’icône **Panneaux** dans le rail de gauche, puis faites glisser le curseur dans le panneau [!UICONTROL **Visionneuses simultanées de médias**] et le panneau [!UICONTROL **Durée de lecture de médias**].

   Les deux panneaux doivent se présenter comme suit :

   ![Panneau des visionneuses simultanées de médias](assets/media-concurrent-viewers-panels.png)

   ![Durée de lecture du média dans le panneau](assets/media-playback-time-spent-panels.png)

1. Partagez le projet comme décrit dans [Partager les projets](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   Si les utilisateurs avec lesquels vous souhaitez partager du contenu ne sont pas disponibles, assurez-vous qu’ils disposent d’un accès utilisateur et administrateur à Customer Journey Analytics dans Adobe Admin Console.

1. Passez à [Envoyer des données à Edge Experience Platform](#send-data-to-experience-platform-edge).

## Envoi de données à Experience Platform Edge

Selon le type de données à envoyer à Experience Platform Edge, vous pouvez utiliser l’une des méthodes suivantes :

### Web : utilisation du SDK Web de Adobe Experience Platform

* [Prise en main](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Envoi de données Web à Edge avec le SDK Web de Adobe Experience Platform](/help/implementation/edge/edge-web-sdk.md)

* [Migrer vers Adobe Streaming Media pour l’extension Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Mobile : utilisation du SDK Mobile Adobe Experience Platform

Utilisez les ressources de documentation suivantes pour terminer la mise en oeuvre pour iOS et Android :

* [Prise en main](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Référence d’API](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [Migrer vers Adobe Streaming Media pour l’extension Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku : SDK Adobe Experience Platform Roku

* [Prise en main](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [SDK Adobe Experience Platform Roku](https://github.com/adobe/aepsdk-roku/tree/main)

* [Migrer vers Adobe Streaming Media pour l’extension Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API : Web et autres

L’API est actuellement la seule méthode prise en charge pour envoyer des données web à Edge Experience Platform.

L’API est également disponible si vous souhaitez utiliser une implémentation personnalisée des API Edge.

Pour plus d’informations sur l’API Media Edge, voir les ressources suivantes :

* [Présentation de l’API Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Prise en main de l’API Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Guide de dépannage de l’API Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [Utilisation du fichier de spécification d’API Open pour les API Media Edge](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)
