---
title: Présentation d’Adobe Analytics for Streaming Media
description: Utilisez Streaming Media Analytics pour obtenir de puissantes informations sur le contenu, le son et les publicités.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 16%

---

# Présentation d’Adobe Analytics for Streaming Media

![Bannière](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media est un module complémentaire d’Adobe Analytics qui fournit de puissants outils de mesure pour l’audio, la vidéo et les publicités. Avec Analytics for Streaming Media, vous obtenez des détails granulaires en temps quasi réel sur la durée, les arrêts et les démarrages qui vous permettent d’évaluer et de combiner des mesures vidéo et audio. Ces informations vous permettent de comprendre les habitudes de visionnage et d’écoute de vos clients et d’augmenter l’engagement avec des recommandations hautement personnalisées.

Adobe Analytics for Streaming Media vous permet de suivre l’ensemble du parcours client sur votre site et les applications de diffusion en continu. Vous pouvez combiner les mesures de médias en flux continu avec d’autres fonctionnalités Adobe Analytics, telles que les analyses d’Audience Analytics, de périphériques mobiles ou entre appareils. Les mesures s’intègrent facilement dans les rapports Adobe Analytics et d’autres produits Adobe Experience Platform. La mesure des médias vous permet de catégoriser vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées nécessaires à une analyse complète et détaillée. Vous pouvez ensuite analyser les données et attribuer des critères de succès au média entièrement consommé, au temps passé moyen et aux publicités terminées.

Vous pouvez mesurer des mesures de diffusion essentielles liées à la qualité de l’expérience (QoE), telles que les images perdues, le temps passé à la mise en mémoire tampon et le débit moyen. De plus, les mesures peuvent être combinées avec les données de votre site web ou de votre application afin de visualiser le chemin et les intérêts du client, afin de fournir des recommandations optimisées et de personnaliser les expériences client à l’aide de Adobe Experience Platform.

## Fonctionnement

Les données de suivi des médias en flux continu sont collectées à partir d’un lecteur à l’aide des SDK Media, des API Media Collection ou des extensions Media (avec balises). Toutes les données granulaires (jusqu’à 10 secondes) sont envoyées au service Media Analytics qui collecte et traite les données pour chaque session de lecture individuelle. Une fois la session de lecture terminée, les données de suivi calculées sont envoyées à Adobe Analytics pour stockage et création de rapports. Avec les mises en oeuvre d’Adobe Customer Journey Analytics (CJA), les données peuvent être envoyées à CJA à l’aide d’Analytics Data Connector (ADC) afin que les clients puissent utiliser CJA comme outil de création de rapports.

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="Processus de diffusion en continu de médias" width="75%">
</div>

## Fonctionnalités

Les avantages d’Adobe Analytics for Streaming Media incluent la surveillance en temps réel, les analyses détaillées, des informations exploitables et des opportunités de monétisation.

* **Analyse en temps réel**: Prenez des décisions en temps réel exploitables à l’aide de mesures de performances clés telles que les démarrages de média, sur plusieurs canaux.

* **Stimuler l’engagement**: Contactez les utilisateurs en réduisant le nombre d’événements de mise en mémoire tampon et en sachant où et quand les publicités doivent être lues dans le contenu afin de fournir une expérience fluide et moins intrusive qui offre des visites renouvelées.

* **Image holistique**: Combinez plusieurs points de données sur tous vos distributeurs de contenu pour obtenir une vue complète de toute votre activité multimédia. Mesurez l’engagement et les vues/écoutes sur tous les canaux possibles via la fonctionnalité Federated Analytics.

* **Granularité accrue**: Évaluer le comportement de visionnage au niveau le plus granulaire, y compris l’heure des visiteurs individuels de la journée, les observateurs simultanés ou les auditeurs par minute, et la durée moyenne de visionnage du contenu.

* **Mesure précise**: Mesurez les différents appareils utilisés pour la consommation de médias (OTT, smartphone, tablette, bureau, etc.) afin de surveiller les schémas et les habitudes d’engagement des utilisateurs.

* **Segmentation**: Appliquez des classifications à vos lecteurs, appareils, genres, chapitres et programmes pour voir comment chacun a un impact sur vos vues/écoutes générales et l’engagement du client avec du contenu, du son, des publicités et des éléments combinés.
