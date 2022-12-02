---
title: Présentation d’Adobe Analytics for Streaming Media
description: Utilisez Streaming Media Analytics pour obtenir de puissants insights sur le contenu, l’audio et les publicités.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '529'
ht-degree: 100%

---

# Présentation d’Adobe Analytics for Streaming Media

![Bannière](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media est un module complémentaire d’Adobe Analytics qui fournit de puissants outils de mesure pour l’audio, la vidéo et les publicités. Grâce à Analytics for Streaming Media, vous pouvez obtenir des détails granulaires en temps quasi réel sur la durée, les arrêts et les démarrages. Vous pourrez ainsi mieux évaluer et combiner des mesures vidéo et audio. Ces insights vous permettent de comprendre les habitudes de visionnage et d’écoute de vos clients et d’augmenter l’engagement grâce à des recommandations hautement personnalisées.

Adobe Analytics for Streaming Media vous permet de suivre l’ensemble du parcours client sur votre site et vos applications en flux continu. Vous pouvez combiner les mesures Streaming Media avec d’autres fonctionnalités Adobe Analytics, telles qu’Audience Analytics, Mobile ou Analytics sur l’ensemble des appareils. Ces mesures s’intègrent facilement aux rapports Adobe Analytics et aux autres produits Adobe Experience Platform. La mesure des médias vous permet de catégoriser vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées nécessaires à une analyse complète et détaillée. Vous pouvez ensuite analyser les données et attribuer des critères de succès au média entièrement consommé, au temps passé moyen et aux publicités terminées.

Vous pouvez déterminer les mesures de diffusion vidéo essentielles liées à la qualité d’expérience (QoE), telles que les images manquantes, le temps consacré à la mise en mémoire tampon et le débit moyen. De plus, ces mesures peuvent être combinées avec les données de votre site Web ou de votre application pour visualiser le chemin et les intérêts des clients, afin de fournir des recommandations optimisées et de personnaliser les expériences client à l’aide d’Adobe Experience Platform.

## Fonctionnement

Les données de Streaming Media sont collectées à partir d’un lecteur à l’aide des SDK Media, des API Media Collection ou des extensions Media (avec balises). Toutes les données granulaires (jusqu’à 10 secondes) sont envoyées au service Media Analytics qui collecte et traite les données pour chaque session de lecture individuelle. Une fois la session de lecture terminée, les données de suivi calculées sont envoyées à Adobe Analytics pour stockage et création de rapports. Grâce aux implémentations d’Adobe Customer Journey Analytics (CJA), les données peuvent être envoyées à CJA à l’aide d’Analytics Data Connector (ADC) afin que les clients puissent utiliser CJA comme outil de création de rapports.

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="Processus Streaming Media" width="75%">
</div>

## Fonctionnalités

Les avantages d’Adobe Analytics for Streaming Media incluent la surveillance en temps réel, les analyses détaillées, des informations exploitables et des opportunités de monétisation.

* **Analyse en temps réel** : prenez des décisions applicables en temps réel à l’aide des mesures de performances clés, telles que les démarrages de média, sur plusieurs canaux.

* **Stimuler l’engagement** : stimulez l’engagement des utilisateurs en réduisant le nombre d’événements de mise en mémoire tampon et en sachant où et quand les publicités doivent s’afficher dans le contenu vidéo pour offrir une expérience de visionnage fluide et moins intrusive qui apporte des visites renouvelées.

* **Image holistique** : combinez plusieurs points de données sur tous vos distributeurs de contenu pour obtenir une vue complète de l’ensemble de vos activités multimédia. Mesurez l’engagement et les vues/écoutes sur tous les canaux possibles via la fonctionnalité Federated Analytics.

* **Meilleure granularité** : évaluez le comportement de visionnage au niveau le plus granulaire, y compris l’heure des visiteurs individuels dans la journée, les observateurs simultanés par minute et la durée moyenne d’affichage du contenu.

* **Mesure précise** : effectuez une mesure pour les différents appareils utilisés pour la consommation de vidéos, notamment les appareils OTT, les smartphones, les tablettes, les postes de travail et autres, pour surveiller les schémas et les habitudes d’engagement des utilisateurs.

* **Segmentation** : appliquez des classifications à vos lecteurs, appareils, genres, chapitres et programmes pour voir comment chacun a un impact sur vos vues générales et l’engagement du client dans le contenu, le son, les annonces et ces éléments combinés.
