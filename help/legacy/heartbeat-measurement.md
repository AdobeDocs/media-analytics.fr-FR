---
title: À propos de la mesure des pulsations
description: Découvrez comment les pulsations sont utilisées pour collecter des mesures vidéo.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 30%

---

# À propos de Heartbeat Measurement

Adobe Analytics utilise des &quot;pulsations&quot; pour collecter des mesures vidéo. Pendant la lecture vidéo, les pulsations sont envoyées au serveur de suivi de pulsation pour mesurer la durée de lecture. Les appels de pulsation sont envoyés toutes les dix secondes. Les pulsations génèrent des mesures d’engagement vidéo granulaires et des rapports d’abandons vidéo plus précis. Adobe Analytics for Streaming Media mesure les pulsations à l’aide d’Adobe Launch avec l’extension Media Analytics, le SDK Media et l’API Media Collection. Les composants `AppMeasurement` et `VisitorID` sont utilisés pour recevoir des données vidéo.

L’utilisation de pulsations Adobe Analytics pour les médias en flux continu présente les avantages suivants :

| Fonctionnalité | Description |
|---|---|
| Événements de médias | Des événements détaillés et personnalisés sont envoyés toutes les 10 secondes pour le contenu principal et toutes les secondes pour les publicités. |
| Mesures et dimensions | Classez des mesures, dimensions et références normalisées entre les fournisseurs. Grâce à une solution normalisée sur toutes les plateformes, vous pouvez utiliser des variables uniformes et normalisées sur l’ensemble de vos médias et plateformes afin de permettre une comparaison plus efficace entre les campagnes, les périphériques et les fournisseurs. |
| Intégrations | L’ID d’Experience Cloud est lié à Adobe Experience Cloud pour une analyse croisée plus facile. Grâce à l’intégration automatique de Adobe Experience Cloud, vous pouvez segmenter vos audiences multimédia, les cibler et formuler des recommandations multimédia en fonction des préférences de l’utilisateur. |
| Tarifs | Suivi transparent par diffusion média (unique) |
| Mise en œuvre et support | Configuration rationalisée avec mises à jour et améliorations continues. Grâce à un processus de mise en oeuvre simplifié, vous pouvez rapidement mapper des variables à l’aide de l’API de votre lecteur et valider les mises en oeuvre à l’aide de l’outil de débogage Adobe afin de vous assurer que toutes les variables nécessaires sont suivies avec précision. |
| Partage de partenaires | Mesures Federated Analytics et certifiées. Grâce aux données partagées par le biais de Federated Analytics, vous pouvez tirer parti de nos fonctionnalités de partage multimédia leaders du secteur pour évaluer les données de manière holistique pour l’ensemble de vos partenaires de distribution multimédia (opérateurs, programmeurs et distributeurs). |
| Suivi avancé | Suivi du contenu téléchargé, suivi de la récupération des erreurs et observateurs simultanés. Vous pouvez effectuer le suivi du contenu multimédia en flux continu téléchargé et lu sur un appareil, quelle que soit sa connectivité. |
