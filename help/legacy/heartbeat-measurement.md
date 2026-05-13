---
title: À propos de la mesure de pulsation
description: Découvrez comment les pulsations servent à collecter des mesures vidéo.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: eb9732ab-8232-4b21-bc4c-89de86dbe4d7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e6c28e30-8689-4bf4-8fa8-561343d308a9id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# À propos de la mesure de pulsation

Les services de streaming multimédia d’Adobe utilisent des « pulsations » pour collecter des mesures vidéo. Pendant la lecture vidéo, les pulsations sont envoyées au serveur de suivi de pulsation pour mesurer la durée de lecture. Les appels de pulsation sont envoyés toutes les dix secondes. Les pulsations génèrent des mesures d’engagement vidéo granulaires et des rapports d’abandons vidéo plus précis. Les services de médias en flux continu mesurent les pulsations à l’aide d’Adobe Launch avec l’extension Media Analytics, Media SDK et l’API Media Collection. Les composants `AppMeasurement` et `VisitorID` sont utilisés pour recevoir des données vidéo.

L’utilisation des pulsations dans les services de streaming multimédia offre les avantages suivants :

| Fonctionnalité | Description |
|---|---|
| Événements de médias | Des événements détaillés et personnalisés sont envoyés toutes les 10 secondes pour le contenu principal et toutes les secondes pour les publicités. |
| Mesures et dimensions | Des mesures, dimensions et benchmarks normalisés et clairs pour tous les fournisseurs. Grâce à une solution normalisée sur toutes les plateformes, vous pouvez utiliser des variables uniformes sur l’ensemble de vos médias et plateformes afin de permettre une comparaison plus efficace entre les campagnes, les appareils et les fournisseurs. |
| Intégrations | L’Experience Cloud ID est lié à Adobe Experience Cloud pour une analyse croisée plus facile. Grâce à l’intégration automatique de Adobe Experience Cloud, vous pouvez segmenter les audiences de vos médias, les cibler et faire des recommandations de médias en fonction de leurs préférences. |
| Tarifs | Suivi transparent par diffusion média (unique) |
| Mise en œuvre et support | Configuration rationalisée avec mises à jour et améliorations continues. Grâce à un processus d’implémentation rationalisé, vous pouvez rapidement mapper des variables via l’API de votre lecteur et valider les implémentations à l’aide de l’outil de débogage Adobe pour vous assurer que toutes les variables nécessaires sont suivies avec précision. |
| Partage de partenaires | Federated Media et Certified Metrics. Grâce aux données partagées via Federated Media, vous pouvez tirer parti de nos fonctionnalités de partage de médias leaders du secteur afin d’évaluer de manière holistique les données de tous vos partenaires de distribution de médias (opérateurs, programmeurs et distributeurs). |
| Suivi avancé | Suivi du contenu téléchargé, suivi de la récupération des erreurs et observateurs simultanés. Vous pouvez effectuer le suivi du contenu multimédia en flux continu téléchargé et lu sur un appareil, quelle que soit sa connectivité. |
