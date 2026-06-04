---
title: Configurer des rapports pour les implémentations d’Edge
description: Configurez Customer Journey Analytics pour créer des rapports sur les données de médias en flux continu collectées via Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 18%

---

# Configurer des rapports pour les implémentations d’Edge

Après avoir implémenté la collecte de médias en flux continu via Edge Network, configurez Customer Journey Analytics pour créer des rapports sur les données collectées. Cette page décrit comment créer une connexion, une vue de données et un projet pour les médias en flux continu.

>[!NOTE]
>
>Cette page traite des rapports dans Customer Journey Analytics, la destination recommandée pour les implémentations d’Edge. Si votre flux de données envoie plutôt des données de médias en flux continu à Adobe Analytics, voir [Configurer des rapports pour les implémentations Analytics uniquement](analytics-reporting.md).

* **Conditions préalables** : terminez une implémentation d’Edge et collectez des données. Voir la présentation de l’implémentation d’Edge [&#128279;](/help/implementation/edge/overview.md) et la méthode d’implémentation choisie.

## Créer une connexion dans Customer Journey Analytics

1. Dans Customer Journey Analytics, créez une connexion comme décrit dans la section [Créer une connexion](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=fr).

   Lors de la création de la connexion, les sélections suivantes sont requises pour les médias en flux continu :

   1. Sélectionnez le jeu de données créé lors de l’implémentation.

   1. Assurez-vous que le paramètre **[!UICONTROL Importer toutes les nouvelles données]** est activé.

1. Continuez avec [Création d’une vue de données dans Customer Journey Analytics](#create-a-data-view-in-customer-journey-analytics).

## Créer une vue de données dans Customer Journey Analytics

1. Dans Customer Journey Analytics, créez une vue de données comme décrit dans la section [Créer ou modifier une vue de données](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=fr).

   1. Dans le champ **[!UICONTROL Connexion]**, sélectionnez la connexion que vous avez précédemment créée.

      Il peut s’écouler jusqu’à 15 minutes avant qu’une nouvelle connexion ne soit disponible.

   1. Dans l’onglet **[!UICONTROL Composants]** de la section **[!UICONTROL Champs de schéma]**, recherchez chaque composant dans les tableaux ci-dessous et faites-le glisser dans le panneau **[!UICONTROL Mesures]**. S’il existe plusieurs champs du même nom, utilisez le chemin XDM pour confirmer le champ correct.

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

      **Mesures de chapitre et de publicité - Chapitre et publicités**

      | Nom du composant | Chemin XDM |
      |----------|---------|
      | Chapitre démarré | mediaReporting.chapterDetails.isStarted |
      | Chapitre terminé | mediaReporting.chapterDetails.isCompleted |
      | Temps de lecture du chapitre | mediaReporting.chapterDetails.timePlayed |
      | Annonce démarrée | mediaReporting.advertisingDetails.isStarted |
      | Annonce publicitaire terminée | mediaReporting.advertisingDetails.isCompleted |
      | Durée de lecture de la publicité | mediaReporting.advertisingDetails.timePlayed |

      **QoE - Mesures de QoE**

      | Nom du composant | Chemin XDM |
      |----------|---------|
      | Temps jusqu’au début | mediaReporting.qoeDataDetails.timeToStart |
      | Pertes avant démarrages | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
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
      | État du lecteur défini | mediaReporting.states.isSet |
      | Nombre d’états du lecteur | mediaReporting.states.count |
      | État du lecteur - Heure | mediaReporting.states.time |

   1. Mettez à jour les libellés (dans le menu déroulant **[!UICONTROL Libellés de contexte]**) des composants dans le tableau suivant. Recherchez et faites glisser dans le panneau tous les composants qui ne figurent pas encore dans le panneau mesures .

      | Nom du composant | Étiquette de contexte |
      |---------|----------|
      | Délai d’expiration du serveur de session multimédia | Média : secondes depuis le dernier appel |
      | Passé sur le média | Média : temps passé sur le média |
      | Durée totale de la mémoire tampon | Média : durée totale de la mémoire tampon |
      | Temps jusqu’au début | Média : Heure De Début |
      | Durée totale de pause | Média : durée totale de pause |

   1. Pour ajouter des répartitions à votre projet, ajoutez les dimensions suivantes au panneau **[!UICONTROL Dimensions]** :

      | Chemin XDM | Nom du composant |
      |---------|----------|
      | mediaReporting.states.name | Nom de l’état du lecteur |
      | mediaReporting.sessionDetails.ID | ID de session multimédia |

      Outre les dimensions de ce tableau, vous pouvez ajouter toutes les autres dimensions en fonction desquelles vous souhaitez filtrer les données dans vos projets.

1. Sélectionnez **[!UICONTROL Enregistrer et continuer]** > **[!UICONTROL Enregistrer et terminer]** pour enregistrer vos modifications.

1. Continuez avec [Créer et configurer un projet dans Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics).

## Création et configuration d’un projet dans Customer Journey Analytics

1. Dans Customer Journey Analytics, dans l’onglet **[!UICONTROL Workspace]**, dans la zone **[!UICONTROL Projets]**, sélectionnez **[!UICONTROL Créer un projet]**.

1. Sélectionnez **[!UICONTROL Projet vierge]** > **[!UICONTROL Créer]**.

1. Dans le nouveau projet, sélectionnez la vue de données que vous avez précédemment créée.

   Lors de la création de panneaux dans votre projet, vous pouvez utiliser tous les composants que vous avez ajoutés à votre vue de données.

1. Sélectionnez l’icône **Panneaux** dans le rail de gauche, puis faites glisser le panneau **[!UICONTROL Visionneuses simultanées de médias]** et le panneau **[!UICONTROL Temps de lecture de médias]**.

1. (Conditionnel) Si vous avez ajouté des métadonnées personnalisées à votre schéma, définissez la persistance des champs personnalisés, comme décrit dans la section [Paramètres du composant de persistance](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) du guide de Customer Journey Analytics.

1. Partagez le projet comme décrit dans la section [Partager des projets](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=fr).

   >[!NOTE]
   >
   >Si les utilisateurs avec lesquels vous souhaitez partager ne sont pas disponibles, assurez-vous qu’ils disposent d’un accès utilisateur et administrateur à Customer Journey Analytics dans Adobe Admin Console.

>[!MORELIKETHIS]
>
>* [Panneaux multimédias dans Workspace](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [Présentation des dimensions](/help/reporting/dimensions/overview.md)
>* [Présentation des mesures](/help/reporting/metrics/overview.md)
