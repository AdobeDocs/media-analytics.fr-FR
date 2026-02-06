---
title: Comment effectuer le suivi du contenu téléchargé hors ligne dans les services de streaming multimédia
description: Découvrez comment utiliser la fonction Contenu téléchargé pour effectuer le suivi de la consommation multimédia lorsquʼun utilisateur est hors ligne.
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 98%

---

# Suivi du contenu téléchargé {#track-downloaded-content}

## Aperçu  {#overview}

La fonctionnalité Contenu téléchargé permet d’effectuer le suivi de la consommation multimédia lorsqu’un utilisateur est hors ligne. Par exemple, un utilisateur télécharge et installe une application sur un appareil mobile, puis l’utilise pour télécharger du contenu dans le stockage local de l’appareil. Pour effectuer le suivi des données téléchargées, Adobe a développé la fonctionnalité Contenu téléchargé. Grâce à cette fonction, lorsque l’utilisateur lit du contenu stocké localement sur un appareil, les données de suivi sont elles aussi stockées sur l’appareil, indépendamment de la connectivité de celui-ci. Lorsque l’utilisateur met fin à la session de lecture et que l’appareil est à nouveau en ligne, les informations de suivi stockées sont envoyées au serveur principal de l’API Media Collection au sein d’une seule payload. Les informations de suivi stockées sont ensuite traitées et déclarées comme d’habitude dans l’API Media Collection.

Comparez les deux approches :

* En ligne

  Avec l’approche en temps réel, le lecteur multimédia envoie des données de suivi pour chaque événement du lecteur et envoie des pings réseau toutes les dix secondes (toutes les secondes pour les publicités) au serveur principal.

* Hors ligne (fonctionnalité Contenu téléchargé)

  Avec cette approche de traitement par lot, les mêmes événements de session doivent être générés, mais ils sont stockés sur l’appareil jusqu’à ce qu’ils soient envoyés au serveur principal en tant que session unique (voir l’exemple ci-dessous).

Chaque approche a ses avantages et ses inconvénients :
* Le scénario en ligne est suivi en temps réel ; cela nécessite une vérification de la connectivité avant chaque appel réseau.
* Le scénario hors ligne (fonctionnalité Contenu téléchargé) ne nécessite qu’une vérification de la connectivité réseau, mais il requiert également une plus grande empreinte mémoire sur l’appareil.

## Implémentation {#implementation}

### Plateformes prises en charge

Le suivi du contenu est pris en charge sur les appareils mobiles iOS et Android.

### Schémas d’événements

La fonctionnalité Contenu téléchargé est la version hors ligne de l’API Media Collection en ligne (standard). Les données d’événement que votre lecteur associe et envoie au serveur principal doivent donc utiliser les mêmes schémas que ceux que vous utilisez lorsque vous effectuez des appels en ligne. Pour plus d’informations sur ces schémas, voir :
* [Aperçu ;](/help/implementation/media-collection-api/mc-api-overview.md)
* [Validation des requêtes d’événement](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordre des événements

* Le premier événement de la charge utile du lot doit être `sessionStart` conforme à l’usage avec l’API Media Collection.
* **Vous devez inclure `media.downloaded: true`** dans les paramètres de métadonnées standard (clé `params`) de l’événement `sessionStart` pour indiquer au serveur principal que vous envoyez du contenu téléchargé. Si ce paramètre n’est pas présent ou est défini sur « false », l’API renverra un code de réponse 400 (Demande incorrecte). Ce paramètre fait la distinction entre le contenu téléchargé et le contenu en direct sur le serveur principal. Si `media.downloaded: true` est défini sur une session en direct, l’API renverra également une réponse 400.
* La mise en œuvre est chargée de stocker correctement les événements du lecteur dans l’ordre dans lequel ils apparaissent.

### Codes de réponse

* 201 - Created : requête traitée avec succès ; les données sont valides et la session a été créée et sera traitée.
* 400 - Bad Request ; la validation du schéma a échoué, toutes les données sont ignorées, aucune donnée de session ne sera traitée.

## Intégration avec Adobe Analytics {#integration-with-adobe-analtyics}

Lors du calcul des appels de début/fin Analytics pour le scénario de contenu téléchargé, le serveur principal définit un champ Analytics supplémentaire appelé `ts.` Ceux-ci sont des horodatages pour les premier et dernier événements reçus (début et fin). Ce mécanisme permet de placer une session multimédia terminée au bon moment (c’est-à-dire que même si l’utilisateur ne revient pas en ligne pendant plusieurs jours, la session multimédia est indiquée comme ayant eu lieu au moment où le contenu a été visionné). Vous devez activer ce mécanisme du côté Adobe Analytics en créant une _suite de rapports facultative horodatée._ Pour activer une suite de rapports facultative horodatée, consultez [Horodatages facultatifs.](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=fr)

## Comparaison d’exemples de sessions {#sample-session-comparison}

### Contenu en ligne

```
POST /api/v1/sessions HTTP/1.1

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
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### Avis d’obsolescence

>[!IMPORTANT]
>
>Le contenu téléchargé pouvait auparavant être également envoyé à l’API `/api/v1/sessions`. Cette méthode de suivi du contenu téléchargé est **obsolète** et sera **supprimée** dans le futur.


L’API `/api/v1/sessions` accepte uniquement les événements d’initialisation de session.
Lors de l’utilisation de la nouvelle API, l’indicateur `media.downloaded`, auparavant obligatoire, n’est plus nécessaire.
Nous vous recommandons vivement d’utiliser l’API `/api/v1/downloaded` pour obtenir de nouvelles implémentations de contenu téléchargé, mais également de mettre à jour les implémentations existantes qui reposent sur l’ancienne API.


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

## Référence de l’API de suivi multimédia

Pour des informations sur la configuration du contenu téléchargé, voir la [référence de l’API de suivi multimédia](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/).
