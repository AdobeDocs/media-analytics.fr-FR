---
title: Conditions préalables
description: null
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Conditions préalables {#prerequisites}

## Décisions {#decision}

Avant de commencer votre mise en œuvre du suivi, les premières décisions doivent être prises concernant la mise en œuvre correspondant le mieux à votre situation :

* **Media Analytics -** À l’aide des derniers SDK Media (la mise en œuvre standard recommandée) et/ou de l’API Media Collection (RESTful)
* **Milestone -** L’ancienne mise en œuvre de suivi d’Adobe
* **API Data Insertion -** Mise en œuvre du suivi sans utiliser les SDK Media

## Tâches {#prereq-tasks}

Pour une mise en œuvre *Media Analytics*, vous devez effectuer les tâches suivantes avant de commencer :

1. **Activez Experience Cloud.**

   Vous devez mettre en œuvre le service d’identité d’Adobe Experience Platform.

   Le service d’identité active le framework d’identification courant pour les services principaux, les solutions, les attributs du client et les audiences d’Experience Cloud dans le service principal aux personnes Pour ce faire, il attribue un identifiant persistant et unique à un visiteur du site. Lorsque votre organisation met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions Experience Cloud.

   ![](assets/mc_id_service_graphic.png)

   Le service d’ID peut également remplacer les différents ID spécifiques à une solution (par exemple, Analytics AID). Via la fonctionnalité [ID de client et états d’authentification](https://marketing.adobe.com/resources/help/fr_FR/mcvid/mcvid-authenticated-state.html), le service d’ID permet de transmettre vos propres ID de client à Experience Cloud. Toutefois, n’oubliez pas que le service d’ID fonctionne uniquement avec les solutions auxquelles vous vous êtes déjà abonné. Si vous n’êtes pas inscrit pour accéder à d’autres produits, le service d’ID ne fournit pas l’accès.

   Par ailleurs, le service d’ID est un composant à part entière de plusieurs fonctionnalités, améliorations et services actuels et futurs d’Experience Cloud. Actuellement, le service d’ID prend en charge [Analytics](https://www.adobe.com/fr/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/fr/marketing-cloud/data-management-platform.html) et [Target.](https://www.adobe.com/fr/marketing-cloud/testing-targeting.html)

   >[!IMPORTANT]
   >
   >Pour participer à Adobe Experience Cloud Device Co-op, le service Experience Cloud ID est requis.

   Si vous n’avez pas mis en œuvre le service d’ID, c’est le moment idéal d’envisager une stratégie de migration. Pour plus d’informations sur l’importance et le rôle du service d’ID, voir [Pourquoi le service d’identité vous concerne.](https://blogs.adobe.com/digitalmarketing/analytics/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

   >[!IMPORTANT]
   >
   >En l’absence d’information sur l’identifiant utilisateur présente dans les appels spécifiques au média, les [méthodes d’ID de secours](https://docs.adobe.com/content/help/fr-FR/analytics/implementation/javascript-implementation/unique-visitors/visid-fallback.html) par défaut s’appliquent.

   Pour en savoir plus sur Experience Cloud ID, consultez [Aperçu du service Experience Cloud ID](https://marketing.adobe.com/resources/help/fr_FR/mcvid/mcvid-overview.html) et [Service d’identité d’Adobe Experience Platform.](https://marketing.adobe.com/resources/help/fr_FR/mcvid/)

1. **Activez les rapports Adobe Analytics.**

   Pour activer les rapports dans Analytics et voir le contenu et les données de publicité que vous collectez, consultez la rubrique [Activation des rapports multimédia.](/help/media-reports/media-reports-enable.md)

