---
title: Configurer des rapports pour les implémentations d’Edge
description: Configurez Customer Journey Analytics pour créer des rapports sur les données de médias en flux continu collectées via Edge Network.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 8%

---

# Configurer des rapports pour les implémentations d’Edge

Après avoir implémenté la collecte de médias en flux continu via Edge Network, configurez Customer Journey Analytics pour créer des rapports sur les données collectées.

>[!NOTE]
>
>Cette page traite des rapports dans Customer Journey Analytics, la destination recommandée pour les implémentations d’Edge. Si votre flux de données envoie plutôt des données de médias en flux continu à Adobe Analytics, voir [Configurer des rapports pour les implémentations Analytics uniquement](analytics-reporting.md).

* **Conditions préalables** : terminez une implémentation d’Edge et collectez des données. Voir la présentation de l’implémentation d’Edge [&#128279;](/help/implementation/edge/overview.md) et la méthode d’implémentation choisie.

## Créer une connexion dans Customer Journey Analytics

1. Dans Customer Journey Analytics, créez une connexion comme décrit dans la section [Créer une connexion](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-connections/create-connection). Lors de la création de la connexion, assurez-vous que la case **[!UICONTROL Importer toutes les nouvelles données]** est activée.

## Créer une vue de données dans Customer Journey Analytics

1. Dans Customer Journey Analytics, créez une vue de données comme décrit dans la section [Créer ou modifier une vue de données](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-dataviews/create-dataview).

   1. Dans le champ **[!UICONTROL Connexion]**, sélectionnez la connexion que vous avez précédemment créée. Les nouvelles connexions peuvent prendre jusqu’à 15 minutes pour apparaître.

   1. Dans l’onglet **[!UICONTROL Composants]** de la section **[!UICONTROL Champs de schéma]**, recherchez chaque composant du tableau ci-dessous et faites-le glisser dans le panneau **[!UICONTROL Dimensions]** ou **[!UICONTROL Mesures]** approprié. S’il existe plusieurs champs du même nom, utilisez le chemin XDM pour confirmer le champ correct. Appliquez le libellé de contexte affiché dans la liste déroulante **[!UICONTROL Libellés de contexte]** dans les paramètres du composant.

      | Composant | Type | Chemin XDM | Étiquette de contexte |
      |---|---|---|---|
      | [Contenu](/help/reporting/dimensions/content.md) | Dimension | `mediaReporting.sessionDetails.name` | Média : ID de contenu |
      | [&#x200B; Nom du contenu &#x200B;](/help/reporting/dimensions/content-name.md) | Dimension | `mediaReporting.sessionDetails.friendlyName` | Média : nom de la vidéo |
      | [&#x200B; Longueur du contenu &#x200B;](/help/reporting/dimensions/content-length.md) | Dimension | `mediaReporting.sessionDetails.length` | Média : durée de la vidéo |
      | [Afficher](/help/reporting/dimensions/show.md) | Dimension | `mediaReporting.sessionDetails.show` | Média : afficher |
      | [&#x200B; Saison &#x200B;](/help/reporting/dimensions/season.md) | Dimension | `mediaReporting.sessionDetails.season` | Média : Saison |
      | [Épisode](/help/reporting/dimensions/episode.md) | Dimension | `mediaReporting.sessionDetails.episode` | Média : épisode |
      | Type d’événement | Dimension | `eventType` | Média : type d’événement |
      | [&#x200B; Temps passé sur le contenu &#x200B;](/help/reporting/metrics/content-time-spent.md) | Mesure | `mediaReporting.sessionDetails.timePlayed` | Média : temps passé sur le contenu |
      | [Temps passé sur le média](/help/reporting/metrics/media-time-spent.md) | Mesure | `mediaReporting.sessionDetails.totalTimePlayed` | Média : temps passé sur le média |
      | [Durée totale de la pause](/help/reporting/metrics/total-pause-duration.md) | Mesure | `mediaReporting.sessionDetails.pauseTime` | Média : durée totale de pause |
      | [Heure de commencer](/help/reporting/metrics/time-to-start.md) | Mesure | `mediaReporting.qoeDataDetails.timeToStart` | Média : heure de début |
      | [Durée totale du tampon](/help/reporting/metrics/total-buffer-duration.md) | Mesure | `mediaReporting.qoeDataDetails.bufferTime` | Média : durée totale de la mémoire tampon |
      | Timeout serveur de la session multimédia | Mesure | `mediaReporting.sessionDetails.secondsSinceLastCall` | Média : secondes depuis le dernier appel |

      >[!IMPORTANT]
      >
      >Les libellés de contexte de ce tableau sont nécessaires au fonctionnement des panneaux de médias en flux continu. Customer Journey Analytics les utilise pour calculer automatiquement les mesures dérivées **Observateurs simultanés** et **Temps de lecture** (utilisées par les panneaux [Observateurs simultanés de médias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) et [Temps de lecture de médias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)), et pour renseigner les options de création de rapports dans le panneau [Audience moyenne par minute de média](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel).

      À ce stade, vous pouvez ajouter d’autres [dimensions](/help/reporting/dimensions/overview.md) ou [mesures](/help/reporting/metrics/overview.md) à votre vue de données. Chaque page répertorie le chemin XDM de ce composant.

1. Sélectionnez **[!UICONTROL Enregistrer et continuer]** → **[!UICONTROL Enregistrer et terminer]** pour enregistrer vos modifications.

## Création et configuration d’un projet dans Customer Journey Analytics

1. Dans Customer Journey Analytics, dans l’onglet **[!UICONTROL Workspace]**, dans la zone **[!UICONTROL Projets]**, sélectionnez **[!UICONTROL Créer un projet]**.

1. Sélectionnez **[!UICONTROL Projet vierge]** → **[!UICONTROL Créer]**.

1. Dans le nouveau projet, sélectionnez la vue de données que vous avez précédemment créée.

   Lors de la création de panneaux dans votre projet, vous pouvez utiliser tous les composants que vous avez ajoutés à votre vue de données.

1. Sélectionnez l’icône **Panneaux** dans le rail de gauche, puis faites glisser les panneaux **[!UICONTROL Audience moyenne par minute de média]**, **[!UICONTROL Observateurs simultanés de médias]** et **[!UICONTROL Temps de lecture de média]**.

1. (Conditionnel) Si vous avez ajouté des métadonnées personnalisées à votre schéma, définissez la persistance des champs personnalisés, comme décrit dans la section [Paramètres du composant de persistance](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/cja-dataviews/component-settings/persistence) du guide de Customer Journey Analytics.

1. Partagez le projet comme décrit dans la section [Partager des projets](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >Si les utilisateurs avec lesquels vous souhaitez partager ne sont pas disponibles, assurez-vous qu’ils disposent d’un accès utilisateur et administrateur à Customer Journey Analytics dans Adobe Admin Console.

## Panneaux multimédias disponibles dans Customer Journey Analytics

Analysis Workspace dans Customer Journey Analytics comprend trois panneaux de médias dédiés pour les clients avec le module complémentaire Streaming Media Collection. Ces panneaux fournissent des visualisations préconfigurées pour les besoins de création de rapports sur les médias en flux continu les plus courants.

* **[Audience moyenne par minute pour les médias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)** : compare la consommation moyenne de contenu sur plusieurs programmes, quels qu’en soient la durée ou le genre. Prend en charge le contenu spécifique (basé sur la durée) et les modes de période personnalisés, et permet de mettre à jour les classifications de durée après coup.
* **[Observateurs simultanés de médias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)** : analyse les observateurs simultanés au fil du temps pour identifier le pic d’accès simultanés et les points de chute. Prend en charge la granularité configurable et la répartition des séries par segments, dimensions ou périodes.
* **[Temps de lecture de média](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)** : analyse la durée de lecture au fil du temps avec des détails sur les périodes de pic et de creux. Prend en charge la granularité et le format de sortie configurables (heures ou minutes).

>[!MORELIKETHIS]
>
>* [Présentation des dimensions](/help/reporting/dimensions/overview.md)
>* [Présentation des mesures](/help/reporting/metrics/overview.md)
