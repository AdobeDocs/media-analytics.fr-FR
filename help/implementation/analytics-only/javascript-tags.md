---
title: Configurer l’extension de balise Media Analytics
description: Utilisez l’extension de balises Adobe Media Analytics (3.x SDK) for Audio and Video pour implémenter des médias en flux continu Analytics uniquement.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 14%

---

# Configurer l’extension de balise Media Analytics

L’extension de balises Adobe Media Analytics (3.x SDK) for Audio and Video déploie Media SDK for JavaScript (3.x) via les balises, sans installation manuelle de JavaScript. Cette page couvre la configuration Balises. Pour installer le SDK dans le code à la place, voir [Configuration de JavaScript pour les médias en flux continu](javascript.md). Pour les nouvelles mises en œuvre, considérez le chemin d’accès Edge [Extension de balise Web SDK](/help/implementation/edge/web-sdk-tags.md) recommandé.

* **Conditions préalables** : suivez les [Présentation de l’implémentation pour Analytics uniquement](overview.md).

## Installation et configuration de l’extension

Ajoutez l’instance de suivi Media à un site acceptant les balises en installant et en configurant l’extension dans l’interface utilisateur de collecte de données. Pour les détails d’installation et de configuration, voir [Extension Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=fr).

## Suivi des événements multimédia

Une fois l’extension configurée, suivez chaque événement multimédia à l’aide de sa méthode de suivi. Consultez l’onglet **Media SDK JS 3.x** sur chaque page [event](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les appels exacts.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations Analytics uniquement](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Extension Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=fr)
>* [Configuration de JavaScript pour les médias en flux continu (dans le code)](javascript.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
