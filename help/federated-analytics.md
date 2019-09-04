---
seo-title: Federated Analytics
title: Federated Analytics
uuid: a 82 ace 81-c 2 f 6-4799-9 a 62-4 c 6 a 737 a 7 dab
translation-type: tm+mt
source-git-commit: 9d456d26caf4adf0a4688425251c798b15d1e7ef

---


# Analyses fédérées{#federated-analytics}

Le service Federated Analytics fournit un système pour le partage de données Adobe Media Analytics (audio et vidéo) entre deux partenaires. Les données de mesure normalisées créées par Media Analytics sont la marque distinctive de Federated Analytics, ce qui permet aux mêmes données d’intégrer un rapport unique à partir de sources multiples. Via les règles et la logique régissant Federated Analytics, les données sont facilement contrôlées et individualisées pour répondre aux besoins de chaque partenariat. Avec Federated Analytics, les mesures audio et vidéo sont plus efficaces, plus simples et plus exploitables.

## Avantages {#section_804FFE8671594A6FB769CBE79EF9D627}

* **Transparent :**&#x200B;Éliminez la boîte noire de la création de données en utilisant la même logique dans toutes les entreprises.
* **Large :** Soyez conscient de la portée et de l’impact entiers de la consommation audio et vidéo à travers les partenariats, les plates-formes et les appareils.
* **Sécurisé :** Contrôlez le partage de données côté serveur par le biais de règles et d’une logique.
* **Normalisé :** Parlez la même langue de données que vos partenaires.
* **Exploitable :** Quantifiez les données audio et vidéo pour évaluer les lecteurs, surveiller les tendances et détecter les anomalies via Adobe Analytics.
* **Centralisé :** Collectez les données de mesure audio et vidéo dans un emplacement Adobe.
* **Contractuel :** Soyez facilement en conformité avec les exigences liées au partage des données légales.
* **Rapide :** Envoyez et recevez des données quasiment en temps réel.
* **Facile :** Balisez les lecteurs une fois avec les kits SDK Adobe, partagez des données avec de nombreux partenaires.

## Définitions {#section_ypl_mb3_vbb}

* **Expéditeur :** Client générant des données d’analyse audio et vidéo sur des lecteurs possédés.
* **Récepteur :** Client recevant des données d’analyse audio et vidéo de la part de l’expéditeur.

## Conditions {#section_4758843A8941441B9A4D0D7A61077A6E}

* **Contrat de diffusion multimédia :** Le récepteur et l’expéditeur doivent disposer d’un contrat Adobe Analytics pour les diffusions multimédia avant d’accéder aux données audio et vidéo dans Adobe Analytics. Pour plus de détails, contactez l’équipe de votre compte.
* **Addendum fédéré :** Chaque expéditeur et récepteur doit avoir signé un addendum avec Adobe avant d’envoyer ou de recevoir des données. Un addendum par client est requis, et non un addendum par partenariat. Pour plus de détails, contactez l’équipe de votre compte.
* **Mise en œuvre de Media Analytics :** L’expéditeur doit disposer de Media Analytics mis en œuvre sur tous les lecteurs allant faire partie du jeu de données fédérées. Seules les données de Media Analytics sont disponibles pour la fédération. See documentation: [Measuring audio and video in Adobe Analytics](media-overview.md)

* **Contrat de conseil Adobe :** Pour la configuration initiale des règles fédérées entre le récepteur et l’expéditeur, il est recommandé de travailler avec des services de conseil pour examiner les données et créer l’accord de partage de données.

## Processus {#section_byb_kb3_vbb}

1. L’expéditeur et le récepteur collaborent ensemble pour remplir le formulaire d’accord des règles de fédération.

   _Téléchargez la version actuelle du formulaire ici :_[ Accord de règles de fédération](federated_analytics_form.pdf)

   >[!NOTE]
   >
   >Ce formulaire contient des champs spéciaux pour notre équipe d'ingénieurs et ne doit être modifié qu'avec Adobe Acrobat. [Téléchargez Acrobat gratuitement.](https://get.adobe.com/reader/)

1. Les services de conseil fournissent au récepteur un fichier de données échantillon comportant les données des lecteurs de l’expéditeur afin de confirmer que des règles de partage de données correctes sont définies, à condition que des fichiers de données soient disponibles.
1. L’expéditeur et le récepteur s’assurent que l’accord de partage de données répondra à toutes les exigences contractuelles entre les deux parties.
1. Les services de conseil envoient le formulaire complété au service Adobe Engineering pour configurer les règles de partage de données.
1. Les données sont partagées dans la suite de rapports de développement, où le récepteur examine et valide les données.
1. Lorsque le récepteur confirme que les données sont correctes, le service Adobe Engineering met à jour les règles pour qu’elles pointent vers une suite de rapports de production.
1. Le récepteur examine et valide les données dans la suite de rapports de production.
1. Si des modifications sont par la suite apportées au jeu de données, l’expéditeur ou le récepteur peut envoyer un ticket d’assistance clientèle en vue d’une assistance.

