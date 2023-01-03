---
title: En savoir plus sur les conditions préalables requises pour les médias en flux continu.
description: Prise en main d’Adobe Analytics for Streaming Media. Découvrez ce dont vous avez besoin pour implémenter Adobe Analytics for Streaming Media.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: b022bed6b7be0cc97caaaf6b7bbc42474a57b400
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 96%

---

# Conditions préalables {#prerequisites}

Pour implémenter Adobe Analytics for Streaming Media, effectuez les tâches suivantes :

1. **Confirmer votre modèle de tarification des médias en flux continu**<br>
Le modèle de tarification actuel est basé sur les flux vidéo. Si nécessaire, contactez votre représentant commercial ou votre gestionnaire de compte pour signer une nouvelle commande de vente, car l’analyse des médias en flux continu est vendue séparément d’Adobe Analytics.

1. **Confirmer que vous mettez en œuvre Adobe Analytics**<br>
Les médias en flux continu pour Adobe Analytics nécessitent également une mise en œuvre de base d’Adobe Analytics. Pour plus d’informations, voir [Implémentation d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr).

1. **Obtenir l’URL du serveur de suivi multimédia**<br>
Demandez à votre représentant Adobe Analytics de vous fournir l’URL du serveur de suivi multimédia. Il s’agit de 
l’URL `collection-api-server` du SDK Mobile, du SDK JavaScript et du serveur de suivi non-collection-api pour Roku. Les noms de domaine pour l’implémentation de l’API sont les suivants : `[your_namespace].hb-api.omtrdc.net`.

1. **Télécharger le SDK Media actuel ou mettre en œuvre les extensions requises**<br>
Selon le chemin d’implémentation, [téléchargez le SDK actuel](download-sdks.md) pour les plateformes web, mobiles ou de type OTT. Les extensions requises doivent être mises en oeuvre pour activer les chemins d’accès des extensions Adobe Analytics pour les médias en streaming.

1. **Activer les rapports Adobe Analytics**<br>
Pour activer les rapports dans Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports dans Analytics. Voir [Activation des rapports multimédia](/help/reporting/media-reports-enable.md).

1. **Activer Experience Cloud**<br>


## Implémentez Adobe Experience Platform Identity Service {#implement-id}

Le **service d’identités** active le framework d’identification courant pour les services principaux d’Experience Cloud, les solutions, les attributs du client et les audiences dans le service principal des Personnes. Pour ce faire, le service attribue un identifiant persistant et unique à un visiteur du site. Lorsque votre organisation met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions Experience Cloud.

![Graphique du service d’ID](assets/mc_id_service_graphic.png)

Le service d’ID peut également remplacer les différents ID spécifiques à une solution (par exemple, Analytics AID). Via la fonctionnalité [ID de client et états d’authentification](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html?lang=fr), le service d’ID permet de transmettre vos propres ID de client à Experience Cloud. Toutefois, n’oubliez pas que le service d’ID fonctionne uniquement avec les solutions auxquelles vous vous êtes déjà abonné. Si vous n’êtes pas abonné pour accéder à d’autres produits, le service d’ID ne fournit pas l’accès.

Le service d’ID est un composant à part entière de plusieurs fonctionnalités, améliorations et services d’Experience Cloud. Actuellement, le service d’ID prend en charge [Analytics](https://www.adobe.com/fr/marketing-cloud/web-analytics.html), [Audience Manager](https://www.adobe.com/fr/marketing-cloud/data-management-platform.html) et [Target](https://www.adobe.com/fr/marketing-cloud/testing-targeting.html).

Si vous n’avez pas mis en œuvre le service d’ID, c’est le moment idéal d’envisager une stratégie de migration. Pour plus d’informations sur l’importance et le rôle du service d’ID, voir [Pourquoi le service d’identité vous concerne.](https://theblog.adobe.com/why-new-adobe-marketing-cloud-id-service-should-be-on-your-radar/)

Pour en savoir plus sur Experience Cloud ID, consultez [Aperçu du service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) et [Service d’identité d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).
