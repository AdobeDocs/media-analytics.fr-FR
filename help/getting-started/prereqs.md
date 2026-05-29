---
title: En savoir plus sur les conditions préalables requises pour les services de streaming multimédia Adobe
description: Prise en main des services de streaming multimédia. Découvrez ce dont vous avez besoin pour la mise en œuvre.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 489
ht-degree: 46%

---

# Conditions préalables {#prerequisites}

Avant de commencer la mise en œuvre des services de streaming multimédia d’Adobe, effectuez les tâches suivantes :

1. **Consultez la présentation des services de streaming multimédia Adobe**<br>
Avant de commencer la mise en œuvre des services de streaming multimédia, consultez la [présentation des services de streaming multimédia d’](/help/media-overview.md) pour vous assurer qu’elle répond à vos besoins.

1. **Confirmer votre modèle de tarification**<br>
Le modèle de tarification actuel pour le module complémentaire de collecte de médias en flux continu Customer Journey Analytics et le module complémentaire Adobe Analytics pour les médias en flux continu repose sur les flux vidéo. Si nécessaire, contactez votre représentant commercial ou l’équipe chargée du compte Adobe, car le module complémentaire est vendu séparément pour Adobe Analytics et Adobe Experience Platform.

1. **Activer les rapports Adobe Analytics**<br>
Pour activer les rapports dans Analytics ou Customer Journey Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports. Voir [Activation des rapports multimédia](/help/implementation/media-sdk/setup/media-reports-enable.md).

1. **Mise en œuvre du service Adobe Experience Platform Identity dans CX Enterprise**

   Le **Service d’identités** offre un framework d’identification commun aux services principaux d’entreprise CX, aux solutions, aux attributs du client et aux audiences dans le service principal des Personnes. Pour ce faire, le service attribue un identifiant persistant et unique à un visiteur du site. Lorsque votre entreprise met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions d’entreprise CX.

   ![Graphique du service d’ID](assets/mc_id_service_graphic.png)

   Le service d’ID peut également remplacer les différents ID spécifiques à une solution (par exemple, Analytics AID). Grâce à la fonctionnalité [ID de client et états d’authentification](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=fr), le service d’ID vous permet de transmettre vos propres ID de client à CX Enterprise. Toutefois, n’oubliez pas que le service d’ID fonctionne uniquement avec les solutions auxquelles vous vous êtes déjà abonné. Si vous n’êtes pas abonné pour accéder à d’autres produits, le service d’ID ne fournit pas l’accès.

   Le service d’ID fait partie intégrante de nombreuses fonctionnalités, améliorations et services de CX Enterprise. Actuellement, le service d’ID prend en charge [Analytics](https://www.adobe.com/fr/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/fr/marketing-cloud/data-management-platform.html) et [Target](https://www.adobe.com/fr/marketing-cloud/testing-targeting.html).

   Si vous n’avez pas mis en œuvre le service d’ID, c’est le moment idéal d’envisager une stratégie de migration. Pour plus d’informations sur l’importance et le rôle du service d’ID, voir [Pourquoi le service d’identité vous concerne.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Pour en savoir plus sur Experience Cloud ID, consultez [Aperçu du service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) et [Service d’identité d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).

1. **Afficher les conditions préalables supplémentaires pour votre méthode d’implémentation**

   Selon la manière dont vous prévoyez d’implémenter les services de médias en flux continu, consultez les conditions préalables requises pour l’une des méthodes d’implémentation suivantes :

   * [Conditions préalables pour les implémentations Adobe Analytics uniquement](/help/implementation/media-sdk/setup/prerequisites-analytics.md)

   * [Conditions préalables pour les implémentations Edge](/help/implementation/edge/prerequisites-edge.md)

   Utilisez la [vue d’ensemble de l’implémentation](/help/implementation/overview.md) pour déterminer la méthode d’implémentation qui vous convient.
