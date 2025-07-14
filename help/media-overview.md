---
title: Présentation de la collection de médias en flux continu Adobe
description: Utilisez la collection de médias en flux continu pour obtenir un insight puissant pour le contenu, l’audio et les publicités.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 65%

---

# Présentation de la collection de médias en flux continu Adobe

![Bannière](./assets/media_analytics_banner.png)

La collection de médias en flux continu Adobe fournit de puissants outils de collecte, de mesure et de personnalisation pour le contenu multimédia en flux continu, tel que l’audio, la vidéo et la publicité pour les fournisseurs de médias en flux continu. Vous pouvez combiner des mesures de médias en flux continu avec des fonctionnalités telles qu’Audience Analytics, Mobile ou Analytics sur l’ensemble des appareils.

Les données de streaming multimédia s’intègrent facilement aux produits Adobe Experience Platform suivants :

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Pour implémenter Streaming Media Collection, contactez votre représentant commercial Adobe ou l’équipe du compte Adobe pour vous assurer que le module complémentaire Streaming Media Collection fait partie de votre portefeuille de produits.

## Principales fonctionnalités

Les avantages de la collection de médias en flux continu incluent la surveillance en temps réel, l’analyse détaillée, des informations exploitables, des opportunités de monétisation, etc.

* **Analyse en temps réel** : prenez des décisions applicables en temps réel à l’aide des mesures de performances clés, telles que les démarrages de média, sur plusieurs canaux.

  Avec la collection de médias en flux continu, vous obtenez des détails granulaires en temps quasi réel sur la durée, les arrêts et les démarrages qui vous permettent d’évaluer et de combiner des mesures vidéo et audio. Ces informations vous permettent de comprendre les habitudes de visionnage et d’écoute de vos clients et clientes et d’augmenter l’engagement grâce à des recommandations hautement personnalisées.

* **Stimuler l’engagement** : stimulez l’engagement des utilisateurs et utilisatrices en réduisant le nombre d’événements de mise en mémoire tampon et en sachant où et quand les publicités doivent s’afficher dans le contenu vidéo pour offrir une expérience de visionnage fluide et moins intrusive qui apporte des visites renouvelées.

* **Image holistique** : combinez plusieurs points de données sur tous vos distributeurs de contenu pour obtenir une vue complète de l’ensemble de vos activités multimédia. Mesurez l’engagement et les vues/écoutes sur tous les canaux possibles.

  La collection de médias en flux continu vous permet de suivre l’ensemble du parcours client sur votre site et vos applications en flux continu pour visualiser le chemin et les intérêts des clients, et fournir des recommandations améliorées et personnaliser les expériences client.  La mesure des médias vous permet de catégoriser vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées nécessaires à une analyse complète et détaillée. Vous pouvez ensuite analyser les données et attribuer des critères de succès au média entièrement consommé, au temps passé moyen et aux publicités terminées.

* **Mesures essentielles** : détermine les mesures de diffusion essentielles liées à la qualité d’expérience (QoE), telles que les images manquantes, le temps consacré à la mise en mémoire tampon et le débit moyen.

* **Meilleure granularité** : évaluez le comportement de visionnage au niveau le plus granulaire, y compris l’heure des visiteurs individuels dans la journée, les observateurs simultanés par minute et la durée moyenne d’affichage du contenu.

* **Mesure précise** : effectuez une mesure pour les différents appareils utilisés pour la consommation de vidéos, notamment les appareils OTT, les smartphones, les tablettes, les postes de travail et autres, pour surveiller les schémas et les habitudes d’engagement des utilisateurs.

* **Segmentation** : appliquez des classifications à vos lecteurs, appareils, genres, chapitres et programmes pour voir comment chacun a un impact sur vos vues générales et l’engagement du client dans le contenu, le son, les annonces et ces éléments combinés.


## Fonctionnement

Les données de suivi des médias en flux continu sont collectées à partir d’un lecteur à l’aide du SDK/de l’extension pour réseau Edge pour Media, de l’extension Media avec des balises, des SDK Media, de l’API Media Edge ou de l’API Media Collection.

Toutes les données granulaires (jusqu’à 10 secondes) sont envoyées au service Media Analytics ou à Experience Edge (en fonction de la [méthode d’implémentation](/help/implementation/overview.md) que vous choisissez), qui collecte et traite les données pour chaque session de lecture individuelle.

Une fois la session de lecture terminée, les données de suivi calculées sont envoyées à Adobe Analytics ou à Customer Journey Analytics pour stockage et création de rapports.

>[!NOTE]
>
>Avec les implémentations de Customer Journey Analytics, les données peuvent être envoyées à Customer Journey Analytics à l’aide d’Experience Edge ou d’Analytics Data Connector (ADC).


Pour plus d’informations sur les différentes méthodes d’implémentation, voir [ Implémentation de la collection Streaming Media pour Adobe Analytics ou Customer Journey Analytics](/help/implementation/overview.md).
