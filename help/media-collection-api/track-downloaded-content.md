---
title: Suivi du contenu téléchargé
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Suivi du contenu téléchargé {#track-downloaded-content}

## Aperçu {#overview}

La fonctionnalité Contenu téléchargé permet d’effectuer le suivi de la consommation multimédia lorsqu’un utilisateur est hors ligne. Par exemple, un utilisateur télécharge et installe une application sur un appareil mobile. L’utilisateur télécharge ensuite du contenu à l’aide de l’application et le stocke localement sur l’appareil. Pour effectuer le suivi des données téléchargées, Adobe a développé la fonctionnalité Contenu téléchargé. Grâce à cette fonction, lorsque l’utilisateur lit du contenu stocké localement sur un appareil, les données de suivi sont elles aussi stockées sur l’appareil, indépendamment de la connectivité de celui-ci. Lorsque l’utilisateur met fin à la session de lecture et que l’appareil est à nouveau en ligne, les informations de suivi stockées sont envoyées au serveur principal de l’API Media Collection au sein d’une seule charge utile. A partir de là, le traitement et la création de rapports se déroulent normalement dans l’API Media Collection.

Comparez les deux approches :

* En ligne

   Avec l’approche en temps réel, le lecteur multimédia envoie des données de suivi à chaque événement du lecteur et envoie des pings réseau toutes les dix secondes (toutes les secondes pour les publicités) au serveur principal.

* Hors ligne (fonctionnalité Contenu téléchargé)

   Avec cette approche de traitement par lot, les mêmes événements de session doivent être générés, mais ils sont stockés sur le périphérique jusqu’à ce qu’ils soient envoyés au serveur principal en tant que session unique (voir l’exemple ci-dessous).

Chaque approche a ses avantages et ses inconvénients :
* Le scénario en ligne est suivi en temps réel ; cela nécessite une vérification de la connectivité avant chaque appel réseau.
* Le scénario hors ligne (fonctionnalité Contenu téléchargé) ne nécessite qu’une vérification de la connectivité réseau, mais il requiert également une plus grande empreinte mémoire sur le périphérique.

## Implémentation {#implementation}

### Schémas d’événements

La fonctionnalité Contenu téléchargé est simplement la version hors ligne de l’API Media Collection en ligne (standard). Les données d’événement que votre lecteur associe et envoie au serveur principal doivent donc utiliser les mêmes schémas que ceux que vous utilisez lorsque vous effectuez des appels en ligne. Pour plus d’informations sur ces schémas, voir :
* [Aperçu ;](/help/media-collection-api/mc-api-overview.md)
* [Validation des requêtes d’événement](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordre des événements

* Le premier événement de la charge utile du lot doit être `sessionStart` conforme à l’usage avec l’API Media Collection.
* **Vous devez inclure`media.downloaded: true`** dans les paramètres de métadonnées standard (clé`params`) de`sessionStart`l’événement pour indiquer au serveur principal que vous envoyez du contenu téléchargé. Si ce paramètre n’est pas présent ou est défini sur « false », l’API renverra un code de réponse 400 (Demande incorrecte), Ce paramètre fait la distinction entre le contenu téléchargé et le contenu en direct sur le serveur principal. (Notez que si`media.downloaded: true`est défini sur une session en direct, l’API renverra également une réponse 400.)
* La mise en œuvre est chargée de stocker correctement les événements du lecteur dans l’ordre dans lequel ils apparaissent.

### Codes de réponse :

* 201 - Created : requête traitée avec succès ; les données sont valides et la session a été créée et sera traitée.
* 400 - Bad Request ; la validation du schéma a échoué, toutes les données sont ignorées, aucune donnée de session ne sera traitée.

## Intégration avec Adobe Analytics {#integration-with-adobe-analtyics}

Lors du calcul des appels de début/fin Analytics pour le scénario de contenu téléchargé, le serveur principal définit un champ Analytics supplémentaire appelé `ts.`. Ceux-ci sont des horodatages pour les premier et dernier événements reçus (début et fin). Ce mécanisme permet de placer une session multimédia terminée au bon moment (c’est-à-dire que même si l’utilisateur ne revient pas en ligne pendant plusieurs jours, la session multimédia est indiquée comme ayant eu lieu au moment où le contenu a été visionné). Vous devez activer ce mécanisme du côté Adobe Analytics en créant une _suite de rapports facultative horodatée._ Pour activer une suite de rapports facultative horodatée, consultez [Horodatages facultatifs.](https://docs.adobe.com/content/help/fr-FR/analytics/admin/admin-tools/timestamp-optional.html)

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

