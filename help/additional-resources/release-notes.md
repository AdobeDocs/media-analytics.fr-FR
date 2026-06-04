---
title: Notes de mise à jour des services de streaming multimédia
description: Affichez les notes de mise à jour des notes de mise à jour des services de streaming multimédia.
feature: Release Notes
role: User, Admin, Developer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
TQID: https://experienceleague.adobe.com/yNfosiewndKE7c-VjoVM6D3ifYlgX3eJGgYQWcBC9no
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: f73667dc-d296-4875-8975-ac3fdc3adc42
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: ac8a38fa-dec3-4581-8f64-178fde9f64e8
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 1516
ht-degree: 79%

---

# Notes de mise à jour des services de streaming multimédia (octobre 2025)

**Dernière mise à jour** : mercredi 7 octobre 2025

## Ressources connexes

Pour plus d’informations sur les nouvelles fonctionnalités, les correctifs et des informations importantes pour les administrateurs, consultez les ressources suivantes.

* [Notes de mise à jour d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=fr)
* [Notes de mise à jour de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=fr)
* Dernières mises à jour des versions d’[Adobe CX Enterprise](https://business.adobe.com/fr/products/adobe-experience-cloud-products.html)

* [Tutoriels Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=fr)

## *Notes de mise à jour de la version actuelle*

## Fonctionnalités nouvelles et mises à jour pour les services de streaming multimédia d’Adobe {#cja-features}

| Fonctionnalité | Description | Date ciblée |
| ----------- | ---------- | ------- |
| **Services de médias en streaming : prise en charge des données de planning** | Vous pouvez désormais charger des données planifiées antérieures de contenu de médias en streaming et en direct afin de suivre l’audience plus facilement et avec plus de précision.<p>Les éléments suivants sont des exemples de contenu en direct qui sont pris en charge avec le chargement de données de planning :</p><ul><li>Plateformes FAST (Free Ad Supported TV)</li><li>Flux locaux</li><li>Sports en direct</li></ul><p>Le chargement des données de planning vous permet de suivre les audiences des programmes individuels qui ont été diffusés pendant la période que vous avez indiquée dans le fichier de chargement. Vous pouvez même recueillir des données d’audience pour des sujets ou des segments de programme spécifiques.</p><p>Ces fonctionnalités sont disponibles quelle que soit la manière dont vous avez mis en œuvre Streaming Media Collection.</p><p>Auparavant, il était difficile de relier avec précision une session donnée à des programmes spécifiques lors de l’analyse du contenu en direct, et il n’était pas possible de relier une session donnée à des sujets individuels ou à des segments de programmes.</p><p>Pour plus d’informations, voir [Charger des données de planning pour suivre le contenu en direct](/help/use-cases/track-schedule-data.md)</p> | Début du déploiement : 29 octobre 2025<p>Disponibilité générale : Premier semestre 2026</p><p>(Initialement prévu pour une disponibilité générale le 29 octobre 2025)</p> |
| Mise à jour des champs XDM pour la collecte de données de médias en flux continu dans Adobe Experience Platform | Lors de la collecte de données des médias en streaming dans Adobe Experience Platform, les chemins d’accès aux champs XDM affichés dans la section « Chemin d’accès au champ XDM » de la documentation des paramètres des médias de streaming ne doivent plus être utilisés. Au lieu de cela, la clientèle qui a implémenté le connecteur source Analytics pour collecter des données de médias en streaming dans Platform avant le 9 mai 2025 doit migrer ses configurations existantes vers les chemins d’accès aux champs mediaReporting, comme indiqué sous l’en-tête « Chemin d’accès aux champs XDM de création de rapports » de la documentation des paramètres de médias en streaming.<p> Ces chemins d’accès aux champs sont documentés dans les pages de variables de médias en flux continu liées à la [présentation des services de médias en flux continu](../media-overview.md) et sont marqués comme « Obsolètes ». (Aucune action n’est requise de la part des clientes et des clients qui implémentent le connecteur source Analytics après le 9 mai 2025 et qui utilisent déjà uniquement les chemins XDM mediaReporting.)</p><p>L’ingestion des données sur les chemins d’accès aux champs XDM obsolètes se poursuivra jusqu’à la fin octobre 2025. Après cela, les chemins d’accès aux champs obsolètes seront intégralement supprimés et ne seront plus visibles dans l’interface d’utilisation de schéma Adobe Experience Platform, et les données seront envoyées uniquement à l’aide des chemins d’accès aux champs mediaReporting.</p><p>Pour plus d’informations, voir [Mappage des paramètres Media Analytics pour Adobe Experience Platform et Customer Journey Analytics](/help/implementation/edge/migrate/parameters-mapping.md).</p><p>Pour obtenir de l’aide concernant la migration, contactez les services Adobe Consulting ou l’équipe en charge des comptes. </p> | Octobre 2025 |
| Envoyer des données web à Adobe Experience Platform Edge Network avec le SDK Web | Vous pouvez désormais [utiliser Adobe Experience Platform Web SDK pour envoyer des données web de médias en flux continu à Adobe Experience Platform Edge Network](/help/implementation/edge/web-sdk.md), ce qui vous permet de créer des campagnes plus personnalisées et de fournir du contenu plus personnalisé, ce qui entraîne davantage de données de tracking pour les rapports.<p>Avec cette amélioration, vous disposez d’une méthode de collecte unifiée pour les implémentations web couvrant toutes les solutions de la plateforme, notamment Customer Journey Analytics, RT-CDP, AJO et le transfert d’événements. Jusqu’à présent, la seule méthode pour transmettre des données web de médias de streaming vers Edge Network était d’utiliser l’API Media Edge. | 29 mai 2024 |
| Envoi de données Roku à Adobe Experience Platform Edge | Désormais, lorsque vous [installez la collecte de médias en flux continu Customer Journey Analytics avec Experience Platform Edge](/help/implementation/edge/overview.md), vous pouvez utiliser le SDK Roku de Adobe Experience Platform pour envoyer des données de médias en flux continu à Adobe Experience Platform. | 12 avril 2024 |
| Media Collection : Intégration à Experience Edge (API et Mobile SDK) | Vous pouvez désormais utiliser l’API Experience Edge et Mobile SDK pour implémenter la collecte de médias en flux continu Customer Journey Analytics, ce qui vous permet de créer des campagnes plus personnalisées et de fournir du contenu plus personnalisé, ce qui entraîne davantage de données de suivi pour les rapports.<p>Cette amélioration fournit une méthode de collecte unifiée pour toutes les solutions, telles que la création de rapports Customer Journey Analytics, RT-CDP, AJO et le transfert d’événement.  [En savoir plus](/help/implementation/edge/overview.md) | samedi 12 mai 2023 |
| Panneau Observateurs simultanés de médias | Déterminez où s’est produit le pic d’accès simultanés et où des abandons ont eu lieu. Obtenez des informations importantes sur la qualité du contenu et l’engagement des observateurs, ainsi que de l’aide concernant la résolution de problèmes ou la planification du volume et de l’échelle. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=fr) | 9 août 2022 |
| Panneau Temps de lecture de média | Le panneau Temps de lecture de média fournit des informations importantes sur lʼengagement des observateurs. Il permet également aux organisations de médias dʼobtenir des informations plus approfondies et plus granulaires sur lʼinteraction client, minute par minute, grâce à une analyse avancée de la durée de la lecture et des fonctionnalités dʼanalyse par tranches horaires. Vous pouvez observer la durée de visionnage de vos flux multimédia à un moment précis. Vous pouvez diviser la durée de lecture selon différentes granularités, notamment les nouvelles granularités de 5 minutes, 15 minutes et 30 minutes. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=fr) | 9 août 2022 |
| Partage des annotations dans les cartes de performance mobiles | Vous pouvez afficher les annotations créées dans l’espace de travail sur les cartes de performance mobiles. Cela vous permet de partager des nuances et informations de données contextuelles sur votre organisation et vos campagnes directement au sein des projets de cartes de performance mobiles, visibles dans l’application mobile des tableaux de bord Analytics. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=fr) | 15 juin 2022 |
| Mises à jour de Report Builder pour Customer Journey Analytics | Inclut des fonctionnalités telles que la planification et le gestionnaire de blocs de données. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=fr) | 18 mai 2022 |
| Annotations dans Analysis Workspace | Les annotations dans l’espace de travail vous permettent de communiquer efficacement les nuances et informations sur les données contextuelles à votre organisation. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=fr) | Le déploiement progressif commence le 23 mars 2022 |
| Mode de prévisualisation du projet de cartes de performance mobile | Lancez une prévisualisation de l’apparence de votre carte de performance mobile dans l’application de tableaux de bord Analytics, directement à partir du créateur de cartes de performance. Le mode de prévisualisation permet aux utilisateurs d’interagir avec les filtres et les graphiques de la même manière que dans l’application, ce qui leur permet de prévisualiser l’expérience avant d’enregistrer et de partager la carte de performance. Les utilisateurs peuvent également utiliser le sélecteur d’appareil en mode de prévisualisation pour voir à quoi ressemblera leur carte de performance sur différents appareils. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=fr#preview) | 16 février 2022 |


## Fonctionnalités nouvelles et mises à jour pour les services de streaming multimédia d’Adobe {#sm-features}

| Fonctionnalité | Description | Date ciblée |
| ----------- | ---------- | ------- |
| À propos du suivi des multiple états du lecteur | Utilisez l’API Media Collection pour implémenter le suivi des multiples états du lecteur. [En savoir plus](/help/implementation/events/player-state/overview.md) | Septembre 2022 |
| Champs XDM renommés | Noms de champ XDM renommés par souci de cohérence :<br>* Paramètres audio et vidéo<br>* Paramètres de publicité<br>* Paramètres de chapitre<br>* Paramètres d’état du lecteur<br>* Paramètres de qualité | Septembre 2022 |
| Référence de Device Co-op | Suppression de la référence à Device Co-op et à l’exigence du service d’ID. | Août 2022 |
| Noms de champ et chemins d’accès XDM mis à jour pour la collecte et la création de rapports. | Mise à jour des éléments suivants :<br>* Paramètres audio et vidéo<br>* Paramètres de publicité<br>* Paramètres de chapitre<br>* Paramètres d’état du lecteur<br>* Paramètres de qualité | Août 2022 |
| Audience moyenne par minute | Le panneau Audience moyenne par minute permet aux clients de Media Analytics de mieux comprendre la consommation moyenne de contenu. <br>Lʼaudience moyenne par minute permet de comparer des programmes de toute longueur ou de tout genre. En outre, vous pouvez comparer ou ajouter l’audience numérique moyenne par minute aux mesures moyennes par minute de la télévision linéaire. Ce panneau offre plus de flexibilité pour mesurer l’audience moyenne pour des périodes personnalisées, ainsi que lorsque la classification de la durée a été mise à jour.  [En savoir plus](/help/reporting/workspace/average-minute-audience.md) | 16 mars 2022 |
| Panneau Temps de lecture de média | Découvrez comment le panneau Temps de lecture de média permet aux utilisateurs de médias de comprendre leur audience en fonction du temps de visionnage au cours de la journée selon une granularité choisie. <br>[Panneau Temps de lecture de média (tutoriel)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=fr) | Janvier 2022 |


## *Notes de mise à jour précédentes*

| Fonctionnalité | Description | Date ciblée ou mise à jour |
| ----------- | ---------- | -------------- |
| Temps de lecture de média | La fonctionnalité Temps de lecture de média en flux continu dʼAdobe fournit des informations précieuses sur lʼengagement des observateurs. Elle permet aux organisations de médias dʼobtenir des informations plus approfondies et granulaires sur lʼinteraction client, minute par minute, grâce à une analyse avancée de la durée de la lecture et de fonctionnalités dʼanalyse par tranches horaires. Vous pouvez observer la durée de visionnage de vos flux multimédias à un moment précis. Vous pouvez diviser la durée de lecture selon différentes granularités, notamment les nouvelles granularités de 5 minutes, 15 minutes et 30 minutes. [En savoir plus...](/help/reporting/workspace/media-playback-time-spent.md) | Septembre 2021 |
| Panneau Observateur simultané de médias dans Analytics Workspace | Déterminez où s’est produit le pic d’accès simultanés et où des abandons ont eu lieu. Obtenez des informations importantes sur la qualité du contenu et l’engagement des observateurs, ainsi que de l’aide concernant la résolution de problèmes ou la planification du volume et de l’échelle. [En savoir plus...](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Panneau Observateurs simultanés de médias dans Analytics Workspace (tutoriel)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=fr#analysis-workspace) | Septembre 2020 <br><br><br>Janvier 2021 |
| Appareils et plateformes pris en charge | L’extension Media Launch avec SDK AEP prend désormais en charge les appareils OTT suivants : <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Système d’exploitation Fire)</li><li>Android TV</li></ul></div> | Juin 2020 |


<!--
## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | 
-->
