---
title: Présentation de l’implémentation pour Analytics uniquement
description: Conditions préalables et méthodes d’implémentation pour le module complémentaire Adobe Analytics for Streaming Media, utilisés pour les implémentations Analytics uniquement.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 5%

---

# Présentation de l’implémentation pour Analytics uniquement

Les implémentations Analytics uniquement utilisent le module complémentaire Adobe Analytics for Streaming Media pour envoyer directement des données à Adobe Analytics, sans Edge Network. Ces méthodes restent entièrement prises en charge. Pour les nouvelles mises en œuvre, Adobe recommande plutôt l’implémentation [d’Edge](/help/implementation/edge/overview.md) car elle met les données à la disposition de Customer Journey Analytics, Adobe Journey Optimizer et Real-Time CDP en plus d’Adobe Analytics.

## Conditions préalables

1. **Remplir les conditions préalables générales.** Voir les [conditions préalables générales](/help/getting-started/prereqs.md).

1. **Confirmer une implémentation d’Adobe Analytics.** Une implémentation de médias en flux continu uniquement pour Analytics nécessite une implémentation Adobe Analytics de base. Voir [&#x200B; Implémentation d’Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr).

1. **Obtenir l’URL du serveur de suivi multimédia.** Demandez à votre représentant Adobe Analytics l’URL du serveur de suivi multimédia (l’URL `collection-api-server`). Le domaine suit généralement le modèle `[your_namespace].hb-api.omtrdc.net`.

1. **Téléchargez le SDK ou installez l’extension.** Selon votre plateforme, [téléchargez le SDK actif](/help/getting-started/download-sdks.md) ou installez l’extension de balise requise.

## Choisir la méthode d’implémentation

Chaque page couvre la configuration spécifique aux médias en flux continu. Le code par événement et par variable réside dans [Événements](/help/implementation/events/overview.md) et [Variables](/help/implementation/variables/overview.md).

| Base de code | In-code | Par Le Biais De Balises |
|---|---|---|
| Web (JavaScript) | [JavaScript &#x200B;](javascript.md) | [Extension de balises Media Analytics](javascript-tags.md) |
| Chromecast | [&#x200B; Chromecast &#x200B;](chromecast.md) | — |
| API | [&#x200B; API Media Collection &#x200B;](media-collection-api.md) | — |

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations Analytics uniquement](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Présentation de l’implémentation](/help/implementation/overview.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
>* [Présentation des variables](/help/implementation/variables/overview.md)
