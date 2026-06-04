---
title: Configurer l’extension de balise Web SDK pour les médias en flux continu
description: Configurez la collecte de médias en flux continu dans l’extension de balises Adobe Experience Platform Web SDK.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Configurer l’extension de balise Web SDK pour les médias en flux continu

L’extension de balise Adobe Experience Platform Web SDK vous permet de configurer la collecte de médias en flux continu dans l’interface utilisateur de collecte de données, sans code de configuration `alloy.js`. Cette page couvre la configuration Balises. Pour configurer le SDK Web dans le code à la place, voir [Configurer le SDK Web pour les médias en flux continu](web-sdk.md).

* **Conditions préalables** :
   * Terminez la présentation de l’implémentation d’[](overview.md) (schéma, jeu de données, flux de données avec [!UICONTROL Media Analytics] activé).
   * Installer et configurer l’extension de balise Web SDK Voir la [présentation de l’extension de balise Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview).

## Configuration des médias en flux continu dans l’extension

1. Dans l’interface utilisateur de collecte de données, ouvrez votre propriété web et sélectionnez **[!UICONTROL Extensions]**.
1. Sur l’extension Adobe Experience Platform Web SDK **installée, sélectionnez**[!UICONTROL  Configurer ]**.**
1. Développez la section **[!UICONTROL Streaming Media]** et définissez les éléments suivants :
   * **[!UICONTROL Canal]** : nom du canal indiqué pour chaque session.
   * **[!UICONTROL Nom du lecteur]** : nom du lecteur multimédia utilisé.
   * **[!UICONTROL Version de l’application]** — La version de votre application de lecteur.
   * **[!UICONTROL Intervalle de ping principal]** et **[!UICONTROL Intervalle de ping des publicités]** — la cadence de ping (en secondes) pour le contenu principal et les publicités.
1. Enregistrez la configuration de l’extension et publiez vos modifications.

## Suivi des événements multimédia

Une fois l’extension configurée, envoyez chaque événement multimédia avec l’action **[!UICONTROL Envoyer l’événement]** (ou la commande `sendEvent`). Voir l’onglet **Web SDK** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les payloads exactes.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations d’Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Présentation de l’extension de balise Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [Configurer le SDK Web pour les médias en flux continu (dans le code)](web-sdk.md)
>* [Présentation des événements](/help/implementation/events/overview.md)
