---
seo-title: Conditions préalables
title: Conditions préalables
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Conditions préalables{#prerequisites}

## Décisions {#decision}

Avant de commencer votre mise en œuvre du suivi, les premières décisions doivent être prises concernant la mise en œuvre correspondant le mieux à votre situation :

* **Media Analytics -** À l’aide des derniers SDK Media (la mise en œuvre standard recommandée) et/ou de l’API Media Collection (RESTful)
* **Milestone -** L’ancienne mise en œuvre de suivi d’Adobe
* **API Data Insertion -** Mise en œuvre du suivi sans utiliser les SDK Media

## Tâches {#prereq-tasks}

Pour une mise en oeuvre *Media Analytics* , vous devez effectuer les tâches suivantes avant de commencer :

1. **Activez Experience Cloud.**

   Vous devez mettre en oeuvre le service d’identité Adobe Experience Platform.

   Le service Identity Service permet la structure d’identification commune pour les services principaux Experience Cloud, les solutions, les attributs du client et les audiences dans le service principal People. Pour ce faire, il attribue un identifiant persistant et unique à un visiteur du site. Lorsque votre organisation met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Le service d’ID peut également remplacer les différents ID spécifiques à une solution (par exemple, Analytics AID). Via la fonctionnalité [ID de client et états d’authentification](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-authenticated-state.html), le service d’ID permet de transmettre vos propres ID de client à Experience Cloud. Toutefois, n’oubliez pas que le service d’ID fonctionne uniquement avec les solutions auxquelles vous vous êtes déjà abonné. Si vous n’êtes pas inscrit pour accéder à d’autres produits, le service d’ID ne fournit pas l’accès.

   Par ailleurs, le service d’ID est un composant à part entière de plusieurs fonctionnalités, améliorations et services actuels et futurs d’Experience Cloud. Currently, the ID service supports [Analytics,](https://www.adobe.com/marketing-cloud/web-analytics.html) [Audience Manager,](https://www.adobe.com/marketing-cloud/data-management-platform.html) and [Target.](https://www.adobe.com/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Pour participer à Adobe Experience Cloud Device Co-op, le service Experience Cloud ID est requis.

   Si vous n’avez pas mis en œuvre le service d’ID, c’est le moment idéal d’envisager une stratégie de migration. For more information about the importance and role of the ID service, see [Why the Identity Service Should be on Your Radar.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >In the absence of any user ID information present on the media-specific calls, the default analytics [Fallback ID Methods](https://docs-author.corp.adobe.com/content/help/en/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) will apply.

   For additional information about the Experience Cloud ID, see [Experience Cloud ID Overview,](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-overview.html) and [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/)

1. **Activez les rapports Adobe Analytics.**

   Pour activer les rapports dans Analytics et voir le contenu et les données de publicité que vous collectez, consultez la rubrique [Activation des rapports multimédia.](/help/media-reports/media-reports-enable.md)

