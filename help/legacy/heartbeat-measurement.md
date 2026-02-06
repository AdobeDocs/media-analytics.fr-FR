---
title: À propos de la mesure de pulsation
description: Découvrez comment les pulsations servent à collecter des mesures vidéo.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 75%

---

# À propos de la mesure de pulsation

Les services de streaming multimédia d’Adobe utilisent des « pulsations » pour collecter des mesures vidéo. Pendant la lecture vidéo, les pulsations sont envoyées au serveur de suivi de pulsation pour mesurer la durée de lecture. Les appels de pulsation sont envoyés toutes les dix secondes. Les pulsations génèrent des mesures d’engagement vidéo granulaires et des rapports d’abandons vidéo plus précis. Les services de médias en flux continu mesurent les pulsations à l’aide d’Adobe Launch avec l’extension Media Analytics, Media SDK et l’API Media Collection. Les composants `AppMeasurement` et `VisitorID` sont utilisés pour recevoir des données vidéo.

L’utilisation des pulsations dans les services de streaming multimédia offre les avantages suivants :

| Fonctionnalité | Description |
|---|---|
| Événements de médias | Des événements détaillés et personnalisés sont envoyés toutes les 10 secondes pour le contenu principal et toutes les secondes pour les publicités. |
| Mesures et dimensions | Des mesures, dimensions et benchmarks standardisés et clairs pour tous les fournisseurs. Grâce à une solution standardisée sur toutes les plateformes, vous pouvez utiliser des variables uniformes sur l’ensemble de vos médias et plateformes pour permettre une comparaison plus efficace entre les campagnes, les appareils et les fournisseurs. |
| Intégrations | L’ID Experience Cloud est lié à Adobe Experience Cloud pour une analyse croisée plus facile. Grâce à l’intégration automatique d’Adobe Experience Cloud, vous pouvez segmenter les audiences de vos médias, les cibler et faire des recommandations de médias en fonction de leurs préférences. |
| Tarifs | Suivi transparent par diffusion média (unique) |
| Mise en œuvre et support | Configuration rationalisée avec mises à jour et améliorations constants. Grâce à un processus d’implémentation rationalisé, vous pouvez rapidement mapper des variables à l’aide de l’API du lecteur et valider les implémentations à l’aide de l’outil de débogage Adobe pour vous assurer que toutes les variables nécessaires sont suivies avec précision. |
| Partage de partenaires | Federated Media et Certified Metrics. Grâce aux données partagées via Federated Media, vous pouvez tirer parti de nos fonctionnalités de partage de médias leaders du secteur afin d’évaluer de manière holistique les données de tous vos partenaires de distribution de médias (opérateurs, programmeurs et distributeurs). |
| Suivi avancé | Suivi du contenu téléchargé, suivi de la récupération des erreurs et observateurs simultanés. Vous pouvez effectuer le suivi du contenu multimédia en streaming téléchargé et lu sur un appareil, quelle que soit sa connectivité. |
