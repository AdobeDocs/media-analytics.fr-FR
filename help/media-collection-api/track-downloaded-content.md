---
seo-title: Suivi du contenu téléchargé
title: Suivi du contenu téléchargé
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# Suivi du contenu téléchargé{#track-downloaded-content}

## Aperçu {#section_hcy_3pk_cfb}

La fonction Contenu téléchargé permet de suivre la consommation des médias lorsqu'un utilisateur est hors ligne. Par exemple : un utilisateur télécharge et installe une application sur un appareil mobile. L’utilisateur télécharge ensuite du contenu à l’aide de l’application et le stocke localement sur l’appareil. Pour suivre ces données téléchargées, Adobe a développé la fonctionnalité Contenu téléchargé. Avec cette fonctionnalité, lorsque l'utilisateur lit le contenu à partir du stockage d'un périphérique, les données de suivi sont stockées sur le périphérique, quelle que soit la connectivité du périphérique. Lorsque l'utilisateur termine la session de lecture et que le périphérique renvoie en ligne, les informations de suivi stockées sont envoyées au serveur principal de l'API de collecte de médias à l'intérieur d'une charge utile unique. A partir de là, le traitement et les rapports se produisent normalement dans l'API de collecte de médias.

Contrastez les deux approches :

* En ligne

   Avec cette approche en temps réel, le lecteur multimédia envoie les données de suivi à chaque événement du lecteur et envoie les chaînes réseau toutes les dix secondes (toutes les secondes pour les publicités), un par un par rapport à l'arrière-plan.

* Hors ligne (fonctionnalité Contenu téléchargé)

   Avec cette approche de traitement par lot, les mêmes événements de session doivent être générés, mais ils sont stockés sur le périphérique jusqu'à ce qu'ils soient envoyés au serveur principal en tant que session unique (voir l'exemple ci-dessous).

Chaque approche présente ses avantages et inconvénients :
* Le scénario en ligne effectue une suivi en temps réel ; ceci requiert une vérification de connectivité avant chaque appel réseau.
* Le scénario hors ligne (fonctionnalité Contenu téléchargé) ne nécessite qu'une vérification de la connectivité réseau, mais nécessite également un plus grand encombrement de mémoire sur le périphérique.

## Implémentation {#section_jhp_jpk_cfb}

### Schémas d'événements

La fonctionnalité Contenu téléchargé est simplement la version hors ligne de l'API de collecte de médias en ligne (standard) de l'API de collecte de médias, de sorte que les données d'événement de votre lecteur et les envois vers le serveur principal utilisent les mêmes schémas d'événement que ceux que vous utilisez lorsque vous effectuez des appels en ligne. Pour plus d'informations sur ces schémas, voir :
* [Aperçu;](/help/media-collection-api/mc-api-overview.md)
* [Validation des requêtes d’événement](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordre des événements

* Le premier événement dans la charge utile du lot doit être `sessionStart` conforme à l'API de collecte de médias.
* **Vous devez inclure`media.downloaded: true`** dans les paramètres de métadonnées standard (`params` clé) l' `sessionStart` événement pour indiquer au serveur principal que vous envoyez du contenu téléchargé. Si ce paramètre n'est pas présent ou est défini sur false lorsque vous envoyez des données téléchargées, l'API renvoie un code de réponse 400 (Requête incorrecte). Ce paramètre distingue le contenu téléchargé par rapport au contenu en direct. (Notez que si `media.downloaded: true` est défini sur une session en direct, l’API renverra également une réponse 400.)
* La mise en œuvre est chargée de stocker correctement les événements du lecteur dans l’ordre dans lequel ils apparaissent.

### Codes de réponse

* 201 - Created: Successful Request ; les données sont valides et la session a été créée et sera traitée.
* 400 - Bad Request ; échec de la validation des schémas, toutes les données sont ignorées, aucune donnée de session ne sera traitée.

## Intégration avec Adobe Analytics {#section_cty_kpk_cfb}

Lors du calcul des appels start/close Analytics pour le scénario de contenu téléchargé, l'arrière-plan définit un champ Analytics supplémentaire appelé `ts.` « This are timestamps for the first and last events received (start and complete). Ce mécanisme permet à une session multimédia terminée d'être placée au bon moment (c'est-à-dire, même si l'utilisateur ne revient pas en ligne pendant plusieurs jours), il est signalé que la session du média a eu lieu au moment où le contenu a été réellement consulté). Vous devez activer ce mécanisme du côté Adobe Analytics en créant une _suite de rapports facultative horodatée._ Pour activer une suite de rapports facultative horodatée, consultez [Horodatages facultatifs.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Comparaison d’exemples de sessions {#section_qnk_lpk_cfb}

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

