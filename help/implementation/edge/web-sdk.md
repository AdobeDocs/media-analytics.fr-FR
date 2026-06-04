---
title: Configurer le SDK web pour les médias en flux continu
description: Configurez Adobe Experience Platform Web SDK (alloy.js) pour envoyer des données de médias en flux continu à Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# Configurer le SDK web pour les médias en flux continu

Le composant `streamingMedia` de Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview) (`alloy.js`, version 2.20.0 ou ultérieure) collecte les données de session multimédia sur votre site Web et les envoie à Edge Network. Cette page traite de la configuration intégrée au code (`alloy.js`). Pour configurer le SDK web via des balises à la place, voir [Configurer l’extension de balise du SDK web pour les médias en flux continu](web-sdk-tags.md).

* **Conditions préalables** :
   * Terminez la présentation de l’implémentation d’[](overview.md) (schéma, jeu de données, flux de données avec [!UICONTROL Media Analytics] activé).
   * Installez Web SDK version 2.20.0 ou ultérieure. Voir [Installation du SDK Web](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/install/overview).

## Configuration du composant streamingMedia

Ajoutez le composant `streamingMedia` à votre configuration `alloy` :

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Pour plus d’informations sur la configuration, voir la commande ](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia).[`streamingMedia`

### Migration à partir de Media JS SDK

Si vous effectuez une migration à partir du SDK Media JS (3.x), la commande [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/getmediaanalyticstracker) de Web SDK renvoie une instance de suivi qui expose les mêmes API que le SDK Media [3.x](/help/implementation/analytics-only/javascript.md), de sorte que vos appels de suivi existants continuent à fonctionner.

## Suivi des événements multimédia

Une fois le SDK configuré, envoyez chaque événement multimédia en appelant [`sendEvent`](https://experienceleague.adobe.com/fr/docs/experience-platform/collection/js/commands/sendevent/overview). Voir l’onglet **Web SDK** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les payloads exactes.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations d’Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Présentation du SDK web](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)
>* [Présentation des événements](/help/implementation/events/overview.md)
>* [Présentation des variables](/help/implementation/variables/overview.md)
