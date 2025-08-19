---
title: Federated Media
description: Le service Federated Media fournit un système de partage de données multimédia en flux continu entre deux partenaires.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 58%

---

# Federated Media{#federated-media}

>[!AVAILABILITY]
>
>Le service Federated Analytics est disponible uniquement lors de l’utilisation de fonctionnalités de streaming multimédia avec Adobe Analytics. Federated Analytics n’est pas disponible dans Customer Journey Analytics.


Le service Federated Analytics fournit un système de partage de données multimédia en flux continu (audio et vidéo) entre deux partenaires.

Les données de mesure normalisées créées par les services de médias en flux continu sont la caractéristique de Federated Media, car elles permettent aux mêmes données de circuler dans un seul rapport à partir de plusieurs sources.

Grâce aux règles et à la logique qui régissent Federated Media, les données sont facilement contrôlées et individualisées pour répondre aux besoins de chaque partenariat.

Federated Media rend les mesures audio et vidéo plus efficaces, rationalisées et exploitables.


![](assets/media-federated.png)

## Avantages {#benefits}

* **Transparent :** éliminer la boîte noire de la création de données en utilisant la même logique dans toutes les entreprises
* **Large :** comprendre la portée et l’impact complets de la consommation audio et vidéo sur l’ensemble des partenariats, plateformes et appareils
* **Sécurisé :** contrôler le partage des données côté serveur par le biais de règles et d’une logique
* **Normalisé :** parler le même langage de données que vos partenaires
* **Exploitable :** quantifier les données audio et vidéo pour évaluer les lecteurs, surveiller les tendances et détecter les anomalies dans Adobe Analytics
* **Centralisé :** collecter des données de mesure audio et vidéo dans un emplacement Adobe
* **Contractuel :** être conforme aux exigences liées au partage des données légales
* **Rapide :** envoyer et recevoir des données quasiment en temps réel
* **Facile :** baliser les lecteurs une seule fois avec les SDK Adobe et partager les données avec de nombreux partenaires

## Définitions {#definitions}

* **Expéditeur :** client générant des données d’analyse audio et vidéo sur les lecteurs détenus
* **Destinataire :** client recevant des données d’analyse audio et vidéo de la part de l’expéditeur

## Conditions {#requirements}

* **Contrat de diffusion média :** le destinataire et l’expéditeur doivent disposer d’un contrat Adobe Analytics pour les diffusions multimédia avant d’accéder aux données audio et vidéo dans Adobe Analytics. Pour plus d’informations, contactez l’équipe chargée de votre compte.
* **Federated Addendum :** chaque expéditeur et chaque destinataire doit avoir signé un addendum avec Adobe avant d’envoyer ou de recevoir des données. Un addendum par client est requis, et non un addendum par partenariat. Pour plus d’informations, contactez l’équipe chargée de votre compte.

* **Implémentation de la collecte de médias en flux continu :** l’expéditeur doit disposer de services de médias en flux continu implémentés sur tous les lecteurs qui feront partie du jeu de données fédéré. Seules les données de médias en flux continu sont disponibles pour la fédération. Pour plus d’informations, voir [Présentation des services de streaming multimédia Adobe](/help/media-overview.md).

* **Contrat de conseil Adobe :** Pour la configuration initiale des règles fédérées entre le récepteur et l’expéditeur, il est recommandé de travailler avec des services de conseil pour examiner les données et créer l’accord de partage de données.

## Téléchargement du formulaire Federated Media

Pour participer à Federated Media, téléchargez et remplissez le formulaire [Accord sur les règles de fédération](assets/federated_analytics_form.pdf).

## Processus {#process}

1. L’expéditeur et le récepteur collaborent ensemble pour remplir le formulaire d’accord des règles de fédération. Ce formulaire contient des champs spéciaux pour notre équipe d’ingénieurs et doit UNIQUEMENT être modifié avec Adobe Acrobat. [Téléchargez gratuitement Acrobat.](https://get.adobe.com/fr/reader/)
1. Les services de conseil fournissent au destinataire un exemple de fichier de données comportant les données des lecteurs de l’expéditeur afin de confirmer que des règles de partage de données correctes sont définies, à condition que des fichiers de données soient disponibles.
1. L’expéditeur et le destinataire s’assurent que l’accord de partage des données répondra à toutes les exigences contractuelles entre les deux parties.
1. Les services de conseil envoient le formulaire complété au service Adobe Engineering pour configurer les règles de partage de données.
1. Les données sont partagées avec la suite de rapports de développement Adobe Analytics ou le flux de données Adobe Experience Platform, où le récepteur examine et valide les données.
1. Une fois que le récepteur confirme que les données sont correctes, l’ingénierie Adobe met à jour les règles pour pointer vers une suite de rapports Analytics de production ou un flux de données Adobe Experience Platform.
1. Le destinataire examine et valide les données de la suite de rapports Analytics de production ou du flux de données Adobe Experience Platform.
1. Si des modifications sont par la suite apportées à l’ensemble de données, l’expéditeur ou le destinataire peut envoyer un ticket à l’assistance clientèle pour obtenir de l’aide.
