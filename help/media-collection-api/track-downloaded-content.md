---
seo-title: Suivi du contenu téléchargé
title: Suivi du contenu téléchargé
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Suivi du contenu téléchargé{#track-downloaded-content}

## Aperçu {#section_hcy_3pk_cfb}

L’API Contenu téléchargé permet d’effectuer le suivi de la consommation multimédia lorsqu’un utilisateur est hors ligne. Par exemple : un utilisateur télécharge et installe une application sur un appareil mobile. L’utilisateur télécharge ensuite du contenu à l’aide de l’application et le stocke localement sur l’appareil. Pour effectuer le suivi des données téléchargées, Adobe a développé l’API Contenu téléchargé. Grâce à cette API, lorsque l’utilisateur lit du contenu stocké localement sur un appareil, les données de suivi sont elles aussi stockées sur l’appareil, indépendamment de la connectivité de celui-ci. Lorsque l'utilisateur termine la session de lecture et que le périphérique est en ligne, les informations de suivi stockées sont envoyées à l'API de collecte de supports à l'intérieur d'une charge utile unique. À partir de là, le traitement et la création de rapports s’effectuent comme d’habitude dans l’API Media Collection, sur laquelle est basée l’API Contenu téléchargé.

Contrastez les deux approches :

* API Media Collection

   Avec cette approche en temps réel, le lecteur multimédia envoie les données de suivi à chaque événement du lecteur et envoie les chaînes réseau toutes les dix secondes (toutes les secondes pour les publicités), un par un par rapport à l'arrière-plan.

* API de contenu téléchargé

   Avec cette approche de traitement par lot, les mêmes événements de session doivent être générés mais stockés sur le périphérique jusqu'à ce qu'ils soient envoyés au serveur principal en tant que session unique (voir l'exemple ci-dessous).

Chaque approche a ses avantages et ses inconvénients : l’API Media Collection effectue un suivi en temps réel, mais requiert un test de connectivité avant chaque appel de réseau ; l’API Downloaded Content ne nécessite qu’un test de connectivité réseau, mais requiert plus de mémoire sur l’appareil.

## Implémentation {#section_jhp_jpk_cfb}

### Schémas d'événements

L'API de contenu téléchargé repose sur l'API de collecte de médias. Par conséquent, les données d'événement qui sont envoyées par votre lecteur et envoyées nécessitent que les mêmes schémas d'événements soient utilisés comme dans l'API de collecte de médias. For information on these schemas, see: [Overview;](/help/media-collection-api/mc-api-overview.md) and [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordre des événements

* Le premier événement dans la charge utile de traitement par lots doit être `sessionStart`.
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. Si ce paramètre n’est pas présent ou est défini sur false, l’API Downloaded Content renverra un code de réponse 400 (Demande incorrecte), Ainsi, le serveur principal peut faire la distinction entre le contenu téléchargé et le contenu en direct, et le traiter en conséquence. (Notez que si `media.downloaded: true` est défini sur une session en direct, l’API Media Collection renverra également une réponse 400.)

* La mise en œuvre est chargée de stocker correctement les événements du lecteur dans l’ordre dans lequel ils apparaissent.

### Codes de réponse

* 201 - Created: Successful Request ; les données sont valides et la session a été créée et sera traitée.
* 400 - Bad Request ; échec de la validation des schémas, toutes les données sont ignorées, aucune donnée de session ne sera traitée.

## Intégration avec Adobe Analytics {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. Il s'agit des horodatages pour les premiers et derniers événements reçus (démarrage et fin). Ce mécanisme permet à une session multimédia terminée d'être placée au bon moment (c'est-à-dire, même si l'utilisateur ne revient pas en ligne pendant plusieurs jours), il est signalé que la session du média a eu lieu au moment où le contenu a été réellement consulté). Vous devez activer ce mécanisme du côté Adobe Analytics en créant une *suite de rapports facultative horodatée*. Pour activer une suite de rapports facultative horodatée, consultez [Horodatages facultatifs.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## Comparaison d’exemples de sessions {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### API Media Collection

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

### API de contenu téléchargé

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
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

