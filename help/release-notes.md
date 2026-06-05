---
title: Notes de mise à jour des services de streaming multimédia
description: Affichez les notes de mise à jour des services de médias en flux continu.
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
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: 720
ht-degree: 36%

---

# Notes de mise à jour des services de streaming multimédia

**Dernière mise à jour** : 4 juin 2026

## 2026

| Fonctionnalité | Description | Date |
| --- | --- | --- |
| **Prise en charge des données de planning** | Chargez les données planifiées pour le contenu en direct précédent afin de suivre l’audience par programme ou segment. Les types de contenu pris en charge comprennent :<ul><li>Plateformes FAST (Free Ad Supported TV)</li><li>Flux locaux</li><li>Sports en direct</li></ul>Pour plus d’informations[&#128279;](/help/use-cases/track-schedule-data.md) consultez le cas d’utilisation  Charger des données de planning pour effectuer le suivi du contenu en direct . | Début du déploiement : 29 octobre 2025<p>Disponibilité générale : octobre 2026</p> |

## 2025

| Fonctionnalité | Description | Date |
| --- | --- | --- |
| **`mediaTimed`l’obsolescence des champs XDM** | L’objet XDM `mediaTimed` est obsolète au profit des chemins d’accès aux champs `mediaReporting`. Les clients qui ont implémenté le connecteur source Analytics avant le 9 mai 2025 doivent migrer leurs configurations. Pour plus d’informations, consultez les guides de migration suivants :<ul><li>[Migration des audiences vers les nouveaux champs de médias en flux continu](/help/implementation/edge/migrate/migrate-audiences.md)</li><li>[Migrez Customer Journey Analytics pour utiliser les nouveaux champs de médias en flux continu](/help/implementation/edge/migrate/migrate-cja-setup.md)</li><li>[Migrer la préparation des données pour les champs personnalisés vers les nouveaux champs de médias en flux continu](/help/implementation/edge/migrate/migrate-dataprep.md)</li><li>[Migration des profils vers les nouveaux champs de médias en flux continu](/help/implementation/edge/migrate/migrate-profiles.md)</li></ul> | Octobre 2025 |

## 2024

| Fonctionnalité | Description | Date |
| --- | --- | --- |
| **Prise en charge de Web SDK** | Envoyez des données web de médias en flux continu à Adobe Experience Platform Edge Network à l’aide de l’extension de balise Web SDK ou Web SDK, ce qui permet d’appliquer une méthode de collecte unifiée à l’ensemble des solutions Platform telles que Customer Journey Analytics, Real-time CDP, Journey Optimizer et le transfert d’événement. Voir [Configuration de Web SDK pour les médias en flux continu](/help/implementation/edge/web-sdk.md) ou [Configuration de l’extension de balise Web SDK pour les médias en flux continu](/help/implementation/edge/web-sdk-tags.md) pour plus d’informations. | 29 mai 2024 |
| **Prise en charge de Roku** | Envoyez des données de médias en flux continu à Adobe Experience Platform à l’aide de Roku SDK. Voir [Configuration de Roku pour les médias en flux continu](/help/implementation/edge/roku.md) pour plus d’informations. | 12 avril 2024 |

## 2023

| Fonctionnalité | Description | Date |
| --- | --- | --- |
| **Assistance pour Experience Edge** | Implémentez la collecte de médias en flux continu à l’aide de l’API Media Edge ou des SDK mobiles pour iOS et Android.<ul><li>[Configurer l’API Media Edge pour les médias en flux continu](/help/implementation/edge/media-edge-api.md)</li><li>[Configurer iOS pour les médias en flux continu](/help/implementation/edge/ios.md) ou [Configurer iOS pour les médias en flux continu avec des balises](/help/implementation/edge/ios-tags.md)</li><li>[Configurer Android pour les médias en flux continu](/help/implementation/edge/android.md) ou [Configurer Android pour les médias en flux continu avec des balises](/help/implementation/edge/android-tags.md)</li></ul> | samedi 12 mai 2023 |

## 2022

| Fonctionnalité | Description | Date |
| --- | --- | --- |
| **Suivi de plusieurs états du lecteur** | Utilisez l’API Media Collection pour implémenter plusieurs [suivi de l’état du lecteur](/help/implementation/events/player-state/overview.md). | Septembre 2022 |
| Champs XDM renommés | Noms de champs XDM renommés par souci de cohérence :<ul><li>Paramètres audio et vidéo</li><li>Paramètres de publicité</li><li>Paramètres de chapitre</li><li>Paramètres d’état du lecteur</li><li>Paramètres de qualité</li></ul> | Septembre 2022 |
| **Panneaux ajoutés à Customer Journey Analytics** | Ajout des panneaux [Observateurs simultanés de médias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers) et [Temps de lecture de médias](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent) à Customer Journey Analytics. | 9 août 2022 |
| **Audience moyenne par minute** | Vous pouvez utiliser le panneau [Audience moyenne par minute](https://experienceleague.adobe.com/fr/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel) pour mieux comprendre la consommation moyenne de contenu. <br>Lʼaudience moyenne par minute permet de comparer des programmes de toute longueur ou de tout genre. En outre, vous pouvez comparer ou ajouter l’audience numérique moyenne par minute aux mesures moyennes par minute de la télévision linéaire. Ce panneau offre plus de flexibilité pour mesurer l’audience moyenne pour des périodes personnalisées, ainsi que lorsque la classification de la durée a été mise à jour. | 16 mars 2022 |

## 2021

| Fonctionnalité | Description | Date |
| --- | --- | --- |
| **Temps de lecture de média** | Le panneau [Temps de lecture](https://experienceleague.adobe.com/fr/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent) fournit un précieux insight sur l’engagement des observateurs et permet aux médias d’obtenir des informations plus précises et plus précises grâce à l’engagement minute par minute des utilisateurs, grâce à une analyse avancée du temps passé et à des fonctionnalités de répartition par jour. Vous pouvez observer la durée de visionnage de vos flux multimédia à un moment précis. Vous pouvez diviser la durée de lecture selon différentes granularités, notamment les nouvelles granularités de 5 minutes, 15 minutes et 30 minutes. | Septembre 2021 |

## 2020

| Fonctionnalité | Description | Date |
| --- | --- | --- |
| **Panneau d’observateurs simultanés de médias** | Le panneau [Observateurs simultanés](https://experienceleague.adobe.com/fr/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers) vous aide à déterminer où s’est produit le pic d’accès simultanés ou où des abandons ont eu lieu. Obtenez des informations importantes sur la qualité du contenu et l’engagement des observateurs, ainsi que de l’aide concernant la résolution de problèmes ou la planification du volume et de l’échelle.<br><br>[Panneau Observateurs simultanés de médias (tutoriel) &#x200B;](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace) | Septembre 2020 ; Janvier 2021 |
| **Appareils et plateformes pris en charge** | L’extension Media Launch avec SDK AEP prend désormais en charge les appareils OTT suivants : <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Système d’exploitation Fire)</li><li>Android TV</li></ul></div> | Juin 2020 |
