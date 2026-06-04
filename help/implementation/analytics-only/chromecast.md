---
title: Configuration de Chromecast pour les médias en flux continu
description: Installez et configurez Media SDK pour Chromecast pour les implémentations de médias en flux continu Analytics uniquement.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 10%

---

# Configuration de Chromecast pour les médias en flux continu

Media SDK for Chromecast envoie directement à Adobe Analytics des données de médias en flux continu depuis les applications de réception Chromecast. Le SDK et sa documentation sont hébergés sur GitHub.

* **Conditions préalables** :
   * Terminez la [présentation de l’implémentation pour Analytics uniquement](overview.md).
   * [Téléchargez Media SDK for Chromecast](/help/getting-started/download-sdks.md).

## Installation et configuration de SDK

Ajoutez le SDK à votre application de réception Chromecast et configurez le dispositif de suivi comme décrit dans les références canoniques :

* [Configuration du SDK Chromecast](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Référence de l’API SDK Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## Suivi des événements multimédia

Une fois le dispositif de suivi créé, suivez chaque événement multimédia à l’aide de sa méthode de suivi. Voir l’onglet **Chromecast** sur chaque page [event](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les appels exacts.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations Analytics uniquement](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Référence de l’API SDK Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [Présentation des événements](/help/implementation/events/overview.md)
>* [Présentation des variables](/help/implementation/variables/overview.md)
