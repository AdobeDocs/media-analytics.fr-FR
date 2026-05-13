---
title: Présentation des médias en flux continu Adobe
description: Utilisez les solutions de streaming multimédia d’Adobe pour bénéficier d’insight puissante pour le contenu, l’audio et les publicités.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6osO9PkXBubSF7a7HebRJhpSTamNnghofASOs7E-E
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: df312454-73c4-43f6-a90e-18f5043f074cid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5520579-b31f-4df7-9281-f0d9f91e2edcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 606
ht-degree: 53%

---

# Présentation des services de streaming multimédia Adobe

![Bannière](./assets/media_analytics_banner.png)

Les services de médias en flux continu Adobe fournissent de puissants outils de collecte, de mesure et de personnalisation pour le contenu multimédia en flux continu, tel que l’audio, la vidéo et la publicité pour les fournisseurs de médias en flux continu. Vous pouvez combiner des mesures de médias en flux continu avec des fonctionnalités telles qu’Audience Analytics, Mobile ou Analytics sur l’ensemble des appareils.

Les données de streaming multimédia s’intègrent facilement aux produits Adobe Experience Platform suivants :

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Pour mettre en œuvre les services de médias en flux continu, contactez votre représentant commercial Adobe ou l’équipe du compte Adobe pour vous assurer que le module complémentaire de collecte de médias en flux continu Customer Journey Analytics ou le module complémentaire Adobe Analytics for Streaming Media fait partie de votre portefeuille de produits.

## Principales fonctionnalités

Les avantages des services de médias en flux continu comprennent la surveillance en temps réel, l’analyse détaillée, des informations exploitables, des opportunités de monétisation, etc.

* **Analyse en temps réel** : prenez des décisions applicables en temps réel à l’aide des mesures de performances clés, telles que les démarrages de média, sur plusieurs canaux.

  Grâce aux services de médias en flux continu, vous obtenez des détails granulaires en temps quasi réel sur la durée, les arrêts et les démarrages qui vous permettent d’évaluer et de combiner des mesures vidéo et audio. Ces informations vous permettent de comprendre les habitudes de visionnage et d’écoute de vos clients et clientes et d’augmenter l’engagement grâce à des recommandations hautement personnalisées.

* **Stimuler l’engagement** : stimulez l’engagement des utilisateurs et utilisatrices en réduisant le nombre d’événements de mise en mémoire tampon et en sachant où et quand les publicités doivent s’afficher dans le contenu vidéo pour offrir une expérience de visionnage fluide et moins intrusive qui apporte des visites renouvelées.

* **Image holistique** : combinez plusieurs points de données sur tous vos distributeurs de contenu pour obtenir une vue complète de l’ensemble de vos activités multimédia. Mesurez l’engagement et les vues/écoutes sur tous les canaux possibles.

  Les services de streaming multimédia vous permettent de suivre l’ensemble du parcours client sur votre site et vos applications de streaming afin de visualiser le chemin et les intérêts des clients et de fournir des recommandations améliorées et de personnaliser les expériences client.  La mesure des médias vous permet de catégoriser vos données en plusieurs dimensions et segments, en capturant toutes les métadonnées nécessaires à une analyse complète et détaillée. Vous pouvez ensuite analyser les données et attribuer des critères de succès au média entièrement consommé, au temps passé moyen et aux publicités terminées.

* **Mesures essentielles** : détermine les mesures de diffusion essentielles liées à la qualité d’expérience (QoE), telles que les images manquantes, le temps consacré à la mise en mémoire tampon et le débit moyen.

* **Meilleure granularité** : évaluez le comportement de visionnage au niveau le plus granulaire, y compris l’heure des visiteurs individuels dans la journée, les observateurs simultanés par minute et la durée moyenne d’affichage du contenu.

* **Mesure précise** : effectuez une mesure pour les différents appareils utilisés pour la consommation de vidéos, notamment les appareils OTT, les smartphones, les tablettes, les postes de travail et autres, pour surveiller les schémas et les habitudes d’engagement des utilisateurs.

* **Segmentation** : appliquez des classifications à vos lecteurs, appareils, genres, chapitres et programmes pour voir comment chacun a un impact sur vos vues générales et l’engagement du client dans le contenu, le son, les annonces et ces éléments combinés.


## Fonctionnement

Les données de suivi des services de médias en flux continu sont collectées à partir d’un lecteur à l’aide de l’extension Media for Edge Network SDK, de l’extension Media avec balises, des SDK Media, de l’API Media Edge ou de l’API Media Collection.

Toutes les données granulaires (jusqu’à 10 secondes) sont envoyées au service Media Analytics ou à Experience Edge (en fonction de la [méthode d’implémentation](/help/implementation/overview.md) que vous choisissez), qui collecte et traite les données pour chaque session de lecture individuelle.

Une fois la session de lecture terminée, les données de suivi calculées sont envoyées à Adobe Analytics ou à Customer Journey Analytics pour stockage et création de rapports.

>[!NOTE]
>
>Avec les implémentations de Customer Journey Analytics, les données peuvent être envoyées à Customer Journey Analytics à l’aide d’Experience Edge ou d’Analytics Data Connector (ADC).


Pour plus d’informations sur les différentes méthodes d’implémentation, voir [ Implémentation des services de streaming multimédia pour Adobe Analytics ou Customer Journey Analytics](/help/implementation/overview.md).
