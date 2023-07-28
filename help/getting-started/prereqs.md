---
title: En savoir plus sur les conditions préalables requises pour les médias en flux continu.
description: Prise en main d’Adobe Analytics for Streaming Media. Découvrez ce dont vous avez besoin pour implémenter Adobe Analytics for Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 75%

---

# Conditions préalables  {#prerequisites}

Avant de commencer à implémenter les médias en flux continu, effectuez les tâches suivantes :

1. **Présentation des médias en flux continu**<br>
Avant de commencer à implémenter les médias en flux continu, passez en revue les [Présentation des médias en flux continu](/help/media-overview.md) pour vous assurer que les médias en flux continu répondent à vos besoins.

1. **Confirmer votre modèle de tarification des médias en flux continu**<br>
Le modèle de tarification actuel est basé sur les flux vidéo. Si nécessaire, contactez votre représentant commercial ou votre équipe de compte d’Adobe pour signer une nouvelle commande de ventes, car les analyses de médias en flux continu sont vendues séparément d’Adobe Analytics.

1. **Activer les rapports Adobe Analytics**<br>
Pour activer les rapports dans Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports dans Analytics. Voir [Activation des rapports multimédia](/help/reporting/media-reports-enable.md).

1. **Mise en oeuvre du service Adobe Experience Platform Identity dans Experience Cloud**

   Le **service d’identités** active le framework d’identification courant pour les services principaux d’Experience Cloud, les solutions, les attributs du client et les audiences dans le service principal des Personnes. Pour ce faire, le service attribue un identifiant persistant et unique à un visiteur du site. Lorsque votre organisation met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions Experience Cloud.

   ![Graphique du service d’ID](assets/mc_id_service_graphic.png)

   Le service d’ID peut également remplacer les différents ID spécifiques à une solution (par exemple, Analytics AID). Via la fonctionnalité [ID de client et états d’authentification](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=fr), le service d’ID permet de transmettre vos propres ID de client à Experience Cloud. Toutefois, n’oubliez pas que le service d’ID fonctionne uniquement avec les solutions auxquelles vous vous êtes déjà abonné. Si vous n’êtes pas abonné pour accéder à d’autres produits, le service d’ID ne fournit pas l’accès.

   Le service d’ID est un composant à part entière de plusieurs fonctionnalités, améliorations et services d’Experience Cloud. Actuellement, le service d’ID prend en charge [Analytics](https://www.adobe.com/fr/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/fr/marketing-cloud/data-management-platform.html) et [Target](https://www.adobe.com/fr/marketing-cloud/testing-targeting.html).

   Si vous n’avez pas mis en œuvre le service d’ID, c’est le moment idéal d’envisager une stratégie de migration. Pour plus d’informations sur l’importance et le rôle du service d’ID, voir [Pourquoi le service d’identité vous concerne.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Pour en savoir plus sur Experience Cloud ID, consultez [Aperçu du service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) et [Service d’identité d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).

1. **Afficher les conditions préalables supplémentaires pour votre méthode de mise en oeuvre**

   Selon la manière dont vous prévoyez de mettre en oeuvre les médias en flux continu, consultez les conditions préalables à l’une des méthodes de mise en oeuvre suivantes :

   * [Conditions préalables pour les implémentations Adobe Analytics uniquement](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * Conditions préalables pour les implémentations Edge
