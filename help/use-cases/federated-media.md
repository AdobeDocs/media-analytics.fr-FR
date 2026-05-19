---
title: Federated Media
description: Le service Federated Media fournit un système de partage de données multimédia en flux continu entre deux partenaires.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/3h9hYx2YAws6b9RGCcZMydQ0jm-YxpxcVg40Tg-N4S4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 599
ht-degree: 59%

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

* **Implémentation de la collecte de médias en flux continu :** l’expéditeur doit disposer de services de médias en flux continu implémentés sur tous les lecteurs qui feront partie du jeu de données fédéré. Seules les données de médias en flux continu sont disponibles pour la fédération. Pour plus d’informations, voir [Présentation des services de streaming multimédia &#x200B;](/help/media-overview.md).

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
