---
seo-title: Suivi du contenu téléchargé
title: Suivi du contenu téléchargé
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Suivi du contenu téléchargé{#track-downloaded-content}

## Aperçu {#overview}

La fonction Contenu téléchargé permet de suivre la consommation des médias lorsqu’un utilisateur est hors ligne. Par exemple : un utilisateur télécharge et installe une application sur un appareil mobile. L’utilisateur télécharge ensuite du contenu à l’aide de l’application et le stocke localement sur l’appareil. Pour suivre ces données téléchargées, Adobe a développé la fonctionnalité Contenu téléchargé. Avec cette fonctionnalité, lorsque l’utilisateur lit le contenu à partir du stockage d’un périphérique, les données de suivi sont stockées sur le périphérique, quelle que soit la connectivité du périphérique. Lorsque l’utilisateur termine la session de lecture et que le périphérique revient en ligne, les informations de suivi stockées sont envoyées au serveur principal de l’API de collecte de médias dans une charge utile unique. A partir de là, le traitement et la création de rapports se déroulent normalement dans l’API de collecte de médias.

Comparez les deux approches :

* En ligne

   Avec cette approche en temps réel, le lecteur multimédia envoie des données de suivi sur chaque événement du lecteur, et envoie des pings réseau toutes les dix secondes (toutes les secondes pour les publicités), une par une au serveur principal.

* Offline (fonctionnalité Contenu téléchargé)

   Avec cette approche de traitement par lot, les mêmes événements de session doivent être générés, mais ils sont stockés sur le périphérique jusqu’à ce qu’ils soient envoyés au serveur principal en tant que session unique (voir l’exemple ci-dessous).

Chaque approche présente ses avantages et ses inconvénients :
* Le scénario en ligne est suivi en temps réel; cela nécessite une vérification de la connectivité avant chaque appel réseau.
* Le scénario hors ligne (fonctionnalité Contenu téléchargé) ne nécessite qu’une vérification de la connectivité réseau, mais nécessite également une plus grande empreinte mémoire sur le périphérique.

## Implémentation {#implementation}

### Schémas d’événements

La fonctionnalité Contenu téléchargé est simplement la version hors ligne de l’API de collecte de médias en ligne (standard). Les données d’événement que votre lecteur associe et envoie au serveur principal doivent donc utiliser les mêmes schémas que ceux que vous utilisez lorsque vous effectuez des appels en ligne. Pour plus d’informations sur ces schémas, voir :
* [Aperçu;](/help/media-collection-api/mc-api-overview.md)
* [Validation des requêtes d’événement](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordre des événements

* Le premier événement de la charge utile par lot doit être `sessionStart` conforme à l’usage avec l’API de collecte de médias.
* **Vous devez inclure`media.downloaded: true`** dans les paramètres de métadonnées standard (`params` clé) de l’ `sessionStart` événement pour indiquer au serveur principal que vous envoyez du contenu téléchargé. Si ce paramètre n’est pas présent ou est défini sur false lorsque vous envoyez des données téléchargées, l’API renvoie un code de réponse 400 (mauvaise requête). Ce paramètre fait la distinction entre le contenu téléchargé et le contenu en direct sur le serveur principal. (Notez que si `media.downloaded: true` est défini sur une session en direct, l’API renverra également une réponse 400.)
* La mise en œuvre est chargée de stocker correctement les événements du lecteur dans l’ordre dans lequel ils apparaissent.

### Codes de réponse

* 201 - Created: Successful Request ; les données sont valides et la session a été créée et sera traitée.
* 400 - Bad Request ; échec de la validation des schémas, toutes les données sont ignorées, aucune donnée de session ne sera traitée.

## Intégration avec Adobe Analytics {#integration-with-adobe-analtyics}

Lors du calcul des appels de début/fin Analytics pour le scénario de contenu téléchargé, le serveur principal définit un champ Analytics supplémentaire appelé `ts.` Horodatages pour les premier et dernier événements reçus (début et fin). Ce mécanisme permet de placer une session multimédia terminée au bon moment (c.-à-d., même si l’utilisateur ne revient pas en ligne pendant plusieurs jours, la session multimédia est signalée comme ayant eu lieu au moment où le contenu a été réellement visionné). Vous devez activer ce mécanisme du côté Adobe Analytics en créant une _suite de rapports facultative horodatée._ Pour activer une suite de rapports facultative horodatée, consultez [Horodatages facultatifs.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Comparaison d’exemples de sessions {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### Contenu en ligne

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### Contenu téléchargé

```
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

