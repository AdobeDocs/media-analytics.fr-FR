---
title: Notes de mise à jour de Streaming Media Collection
description: Affichez les notes de mise à jour des notes de mise à jour de la collection Streaming Media.
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 78%

---

# Notes de mise à jour de Streaming Media Collection (mai 2023)

**Dernière mise à jour** : jeudi 29 mai 2024

## Ressources connexes

Pour plus d’informations sur les nouvelles fonctionnalités, les correctifs et des informations importantes pour les administrateurs, consultez les ressources suivantes.

* [Notes de mise à jour d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=fr)
* [Notes de mise à jour de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=fr)
* Dernières mises à jour des [produits Adobe Experience Cloud](https://business.adobe.com/fr/products/adobe-experience-cloud-products.html)

* [Tutoriels Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=fr)

## *Notes de mise à jour de la version actuelle*

## Fonctionnalités nouvelles et mises à jour de la collection Streaming Media d’Adobe {#cja-features}

| Fonctionnalité | Description | Date ciblée |
| ----------- | ---------- | ------- |
| Envoyer des données web à Adobe Experience Platform Edge Network avec le SDK Web | Vous pouvez désormais [utiliser Adobe Experience Platform Web SDK pour envoyer des données web de médias en flux continu à Adobe Experience Platform Edge Network](/help/implementation/edge/edge-web-sdk.md), ce qui vous permet de créer des campagnes plus personnalisées et de fournir du contenu plus personnalisé, ce qui entraîne davantage de données de tracking pour les rapports.<p>Avec cette amélioration, vous disposez d’une méthode de collecte unifiée pour les implémentations web couvrant toutes les solutions de la plateforme, notamment Customer Journey Analytics, RT-CDP, AJO et le transfert d’événements. Jusqu’à présent, la seule méthode pour transmettre des données web de médias de streaming vers Edge Network était d’utiliser l’API Media Edge. | 29 mai 2024 |
| Envoi de données Roku à Adobe Experience Platform Edge | Désormais, lorsque vous [installez la collecte de médias en flux continu avec Edge Experience Platform ](/help/implementation/edge/implementation-edge.md), vous pouvez utiliser le SDK Roku de Adobe Experience Platform pour envoyer des données de médias en flux continu à Adobe Experience Platform. | 12 avril 2024 |
| Media Collection : Intégration à Experience Edge (API et Mobile SDK) | Vous pouvez désormais utiliser l’API Experience Edge et Mobile SDK pour implémenter la collection de médias en flux continu Adobe, ce qui vous permet de créer des campagnes plus personnalisées et de fournir du contenu plus personnalisé, ce qui entraîne davantage de données de suivi pour les rapports.<p>Cette amélioration fournit une méthode de collecte unifiée pour toutes les solutions, telles que la création de rapports de Customer Journey Analytics, RT-CDP, AJO et le transfert d’événement.  [En savoir plus](/help/implementation/edge/implementation-edge.md) | samedi 12 mai 2023 |
| Panneau Observateurs simultanés de médias | Déterminez où s’est produit le pic d’accès simultanés et où des abandons ont eu lieu. Obtenez des informations importantes sur la qualité du contenu et l’engagement des observateurs, ainsi que de l’aide concernant la résolution de problèmes ou la planification du volume et de l’échelle. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=fr) | 9 août 2022 |
| Panneau Temps de lecture de média | Le panneau Temps de lecture de média fournit des informations importantes sur lʼengagement des observateurs. Il permet également aux organisations de médias dʼobtenir des informations plus approfondies et plus granulaires sur lʼinteraction client, minute par minute, grâce à une analyse avancée de la durée de la lecture et des fonctionnalités dʼanalyse par tranches horaires. Vous pouvez observer la durée de visionnage de vos flux multimédia à un moment précis. Vous pouvez diviser la durée de lecture selon différentes granularités, notamment les nouvelles granularités de 5 minutes, 15 minutes et 30 minutes. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=fr) | 9 août 2022 |
| Partage des annotations dans les cartes de performance mobiles | Vous pouvez afficher les annotations créées dans l’espace de travail sur les cartes de performance mobiles. Cela vous permet de partager des nuances et informations de données contextuelles sur votre organisation et vos campagnes directement au sein des projets de cartes de performance mobiles, visibles dans l’application mobile des tableaux de bord Analytics. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=fr) | 15 juin 2022 |
| Report Builder des mises à jour du Customer Journey Analytics | Inclut des fonctionnalités telles que la planification et le gestionnaire de blocs de données. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=fr) | 18 mai 2022 |
| Annotations dans Analysis Workspace | Les annotations dans l’espace de travail vous permettent de communiquer efficacement les nuances et informations sur les données contextuelles à votre organisation. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=fr) | Le déploiement progressif commence le 23 mars 2022 |
| Mode de prévisualisation du projet de cartes de performance mobile | Lancez une prévisualisation de l’apparence de votre carte de performance mobile dans l’application de tableaux de bord Analytics, directement à partir du créateur de cartes de performance. Le mode de prévisualisation permet aux utilisateurs d’interagir avec les filtres et les graphiques de la même manière que dans l’application, ce qui leur permet de prévisualiser l’expérience avant d’enregistrer et de partager la carte de performance. Les utilisateurs peuvent également utiliser le sélecteur d’appareil en mode de prévisualisation pour voir à quoi ressemblera leur carte de performance sur différents appareils. [En savoir plus](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=fr#preview) | 16 février 2022 |


## Fonctionnalités nouvelles et mises à jour de la collection Streaming Media d’Adobe {#sm-features}

| Fonctionnalité | Description | Date ciblée |
| ----------- | ---------- | ------- |
| À propos du suivi des multiple états du lecteur | Utilisez l’API Media Collection pour implémenter le suivi des multiples états du lecteur. [En savoir plus](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=fr) | Septembre 2022 |
| Champs XDM renommés | Noms de champs XDM renommés par souci de cohérence :<br>* Paramètres audio et vidéo<br>* Paramètres de publicité<br>* Paramètres de chapitre<br>* Paramètres d’état du lecteur<br>* Paramètres de qualité | Septembre 2022 |
| Référence de Device Co-op | Suppression de la référence à Adobe Experience Cloud Device Co-op et à l’exigence du service d’Experience Cloud ID. | Août 2022 |
| Noms de champ et chemins d’accès XDM mis à jour pour la collecte et la création de rapports. | Mise à jour des éléments suivants :<br>* Paramètres audio et vidéo<br>* Paramètres de publicité<br>* Paramètres de chapitre<br>* Paramètres d’état du lecteur<br>* Paramètres de qualité | Août 2022 |
| Audience moyenne par minute | Le panneau Audience moyenne par minute permet aux clients de Media Analytics de mieux comprendre la consommation moyenne de contenu. <br>Lʼaudience moyenne par minute permet de comparer des programmes de toute longueur ou de tout genre. En outre, vous pouvez comparer ou ajouter l’audience numérique moyenne par minute aux mesures moyennes par minute de la télévision linéaire. Ce panneau offre plus de flexibilité pour mesurer l’audience moyenne pour des périodes personnalisées, ainsi que lorsque la classification de la durée a été mise à jour. [En savoir plus](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=fr) | 16 mars 2022 |
| Panneau Temps de lecture de média | Découvrez comment le panneau Temps de lecture de média permet aux utilisateurs de médias de comprendre leur audience en fonction du temps de visionnage au cours de la journée selon une granularité choisie. <br>[Panneau Temps de lecture de média (tutoriel)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=fr) | Janvier 2022 |


## *Notes de mise à jour précédentes*

| Fonctionnalité | Description | Date ciblée ou mise à jour |
| ----------- | ---------- | -------------- |
| Temps de lecture de média | La fonctionnalité Temps de lecture de média en flux continu dʼAdobe fournit des informations précieuses sur lʼengagement des observateurs. Elle permet aux organisations de médias dʼobtenir des informations plus approfondies et granulaires sur lʼinteraction client, minute par minute, grâce à une analyse avancée de la durée de la lecture et de fonctionnalités dʼanalyse par tranches horaires. Vous pouvez observer la durée de visionnage de vos flux multimédias à un moment précis. Vous pouvez diviser la durée de lecture selon différentes granularités, notamment les nouvelles granularités de 5 minutes, 15 minutes et 30 minutes. [En savoir plus...](/help/reporting/workspace/media-playback-time-spent.md) | Septembre 2021 |
| Panneau Observateur simultané de médias dans Analytics Workspace | Déterminez où s’est produit le pic d’accès simultanés et où des abandons ont eu lieu. Obtenez des informations importantes sur la qualité du contenu et l’engagement des observateurs, ainsi que de l’aide concernant la résolution de problèmes ou la planification du volume et de l’échelle. [En savoir plus...](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Panneau Observateurs simultanés de médias dans Analytics Workspace (tutoriel)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=fr#analysis-workspace) | Septembre 2020 <br><br><br>Janvier 2021 |
| Appareils et plateformes pris en charge | L’extension Media Launch avec SDK AEP prend désormais en charge les appareils OTT suivants : <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Système d’exploitation Fire)</li><li>Android TV</li></ul></div> | Juin 2020 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
