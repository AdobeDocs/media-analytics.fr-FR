---
title: Federated Analytics
description: 'Le service Federated Analytics fournit un système pour le partage de données Adobe Media Analytics (audio et vidéo) entre deux partenaires. '
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Federated Analytics {#federated-analytics}

Le service Federated Analytics fournit un système pour le partage de données Adobe Media Analytics (audio et vidéo) entre deux partenaires. Les données de mesure normalisées créées par Media Analytics sont la marque distinctive de Federated Analytics, ce qui permet aux mêmes données d’intégrer un rapport unique à partir de sources multiples.
Via les règles et la logique régissant Federated Analytics, les données sont facilement contrôlées et individualisées pour répondre aux besoins de chaque partenariat.
Avec Federated Analytics, les mesures audio et vidéo sont plus efficaces, plus simples et plus exploitables.

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
* **Mise en œuvre de Media Analytics :** l’expéditeur doit avoir mis en œuvre Media Analytics sur tous les lecteurs qui feront partie du jeu de données fédérées. Seules les données Media Analytics sont disponibles pour la fédération. Voir documentation : [Mesures audio et vidéo dans Adobe Analytics](/help/media-overview.md)

* **Contrat de conseil Adobe :** Pour la configuration initiale des règles fédérées entre le récepteur et l’expéditeur, il est recommandé de travailler avec des services de conseil pour examiner les données et créer l’accord de partage de données.

## Télécharger le formulaire Federated Analytics

Téléchargez la version actuelle de ce formulaire ici : [Accord sur les règles de fédération](https://github.com/AdobeDocs/media-analytics.en/blob/master/help/federated-analytics-form.pdf)

## Processus {#process}

1. L’expéditeur et le récepteur collaborent ensemble pour remplir le formulaire d’accord des règles de fédération. Ce formulaire contient des champs spéciaux pour notre équipe d’ingénieurs et doit UNIQUEMENT être modifié avec Adobe Acrobat. [Téléchargez gratuitement Acrobat.](https://get.adobe.com/fr/reader/)
1. Les services de conseil fournissent au destinataire un fichier de données échantillon comportant les données des lecteurs de l’expéditeur afin de confirmer que des règles de partage de données correctes sont définies, à condition que des fichiers de données soient disponibles.
1. L’expéditeur et le destinataire s’assurent que l’accord de partage des données répondra à toutes les exigences contractuelles entre les deux parties.
1. Les services de conseil envoient le formulaire complété au service Adobe Engineering pour configurer les règles de partage de données.
1. Les données sont partagées dans la suite de rapports de développement, où le destinataire examine et valide les données.
1. Une fois que le destinataire a confirmé que les données sont correctes, Adobe Engineering met à jour les règles afin qu’elles pointent vers une suite de rapports de production.
1. Le destinataire examine et valide les données de la suite de rapports de production.
1. Si des modifications sont par la suite apportées à l’ensemble de données, l’expéditeur ou le destinataire peut envoyer un ticket à l’assistance clientèle pour obtenir de l’aide.

