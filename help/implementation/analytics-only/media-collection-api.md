---
title: Configurer l’API Media Collection pour les médias en flux continu
description: Utilisez l’API Media Collection pour envoyer directement des données de médias en flux continu à Adobe Analytics avec des appels HTTP RESTful.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# Configurer l’API Media Collection pour les médias en flux continu

L’API Media Collection envoie directement des données de médias en flux continu à Adobe Analytics à l’aide d’appels HTTP RESTful. Dans la mesure où il est entièrement personnalisable, il prend en charge le suivi personnalisé et les appareils que les SDK ne couvrent pas. Utilisez-le lorsqu’un SDK n’est pas une option pour votre plateforme.

* **Conditions préalables** : suivez les [Présentation de l’implémentation pour Analytics uniquement](overview.md).

## Mise en œuvre de l’API

Ouvrez une session avec une requête `sessionStart`, puis envoyez les événements suivants à la session qu’elle renvoie. Pour obtenir des instructions complètes sur les formats de requête/réponse, les paramètres, les schémas de validation et l’implémentation, consultez la [Référence de l’API Media Collection](../media-collection-api/mc-api-overview.md).

## Suivi des événements multimédia

Consultez l’onglet **API Media Collection** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les payloads exactes.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations Analytics uniquement](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Référence de l’API Media Collection ](../media-collection-api/mc-api-overview.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
>* [Présentation des variables](/help/implementation/variables/overview.md)
