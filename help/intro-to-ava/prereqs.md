---
title: En savoir plus sur les conditions préalables requises pour les médias en flux continu
description: Prise en main d’Adobe Analytics Streaming Media. Découvrez ce dont vous avez besoin pour mettre en oeuvre Adobe Analytics for Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: '"Media Analytics, configuration système requise"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 93%

---

# Conditions préalables {#prerequisites}

## Décisions {#decision}

Avant de commencer la mise en œuvre de votre suivi, vous devez prendre quelques décisions initiales concernant la mise en œuvre correspondant le mieux à votre situation :

* **Media Analytics -** utilisation des derniers SDK Media (mise en œuvre standard recommandée) et/ou de l’API Media Collection (RESTful)
* **Milestone -** l’ancienne mise en œuvre du suivi Adobe
* **API Data Insertion -** mise en œuvre du suivi sans utiliser de SDK Media

## Tâches {#prereq-tasks}

Pour une mise en œuvre *Media Analytics*, vous devez effectuer les tâches suivantes avant de commencer :

1. **Activez Experience Cloud.**

   Vous devez mettre en œuvre le service d’identité d’Adobe Experience Platform.

   Le service d’identité active le framework d’identification courant pour les services principaux, les solutions, les attributs du client et les audiences d’Experience Cloud dans le service principal aux personnes Pour ce faire, le service attribue un identifiant persistant et unique à un visiteur du site. Lorsque votre organisation met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Le service d’ID peut également remplacer les différents ID spécifiques à une solution (par exemple, Analytics AID). Via la fonctionnalité [ID de client et états d’authentification](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=fr), le service d’ID permet de transmettre vos propres ID de client à Experience Cloud. Toutefois, n’oubliez pas que le service d’ID fonctionne uniquement avec les solutions auxquelles vous vous êtes déjà abonné. Si vous n’êtes pas abonné pour accéder à d’autres produits, le service d’ID ne fournit pas l’accès.

   Par ailleurs, le service d’ID est un composant à part entière de plusieurs fonctionnalités, améliorations et services actuels et futurs d’Experience Cloud. Actuellement, le service d’ID prend en charge [Analytics](https://www.adobe.com/fr/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/fr/marketing-cloud/data-management-platform.html) et [Target.](https://www.adobe.com/fr/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Pour participer à Adobe Experience Cloud Device Co-op, le service Experience Cloud ID est requis.

   Si vous n’avez pas mis en œuvre le service d’ID, c’est le moment idéal d’envisager une stratégie de migration. Pour plus d’informations sur l’importance et le rôle du service d’ID, voir [Pourquoi le service d’identité vous concerne.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   Pour en savoir plus sur Experience Cloud ID, consultez [Aperçu du service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) et [Service d’identité d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).

1. **Activez les rapports Adobe Analytics.**

   Pour activer les rapports dans Analytics et voir le contenu et les données de publicité que vous collectez, consultez la rubrique [Activation des rapports multimédia.](/help/media-reports/media-reports-enable.md)
