---
seo-title: Aperçu
title: Aperçu
uuid: c 14 bdbef -5846-4 d 31-8 a 14-8 e 9 e 0 e 9 c 9861
translation-type: tm+mt
source-git-commit: a7ddd2b281252bee2686a0fa53ce8da59553df4b

---


# Aperçu{#overview}

L’API Media Collection constitue l’alternative RESTful d’Adobe au kit SDK Media côté client. Grâce à l’API Media Collection, votre lecteur peut effectuer le suivi des événements audio et vidéo à l’aide d’appels HTTP RESTful. L'API de collecte de médias offre le même suivi en temps réel du kit de développement multimédia, plus une fonction supplémentaire :

* **Suivi du contenu téléchargé**

   Cette fonctionnalité permet de suivre les médias pendant qu'un utilisateur est hors ligne, grâce au stockage local de données d'événement jusqu'à ce que le périphérique de l'utilisateur renvoie en ligne. (Consultez la rubrique [Suivi du contenu téléchargé](track-downloaded-content.md) pour en savoir plus.)

L’API Media Collection est essentiellement un adaptateur, agissant comme une version côté serveur du kit SDK Media. Cela signifie que certains aspects de la documentation du kit de développement multimédia sont également pertinents pour l'API de collecte de médias. For example, both solutions use the same [Audio and Video Parameters](../metrics-and-metadata/audio-video-parameters.md), and the collected Audio and Video tracking data leads to the same [Reporting and Analysis.](../media-reports/media-reports-enable.md)

## Flux de données de suivi multimédia {#section_pwq_n34_qbb}

Un lecteur multimédia implémentant l'API de collecte de médias effectue des appels de suivi d'API restful directement au serveur de suivi multimédia, tandis qu'un lecteur implémentant le kit de développement multimédia effectue des appels de suivi aux API du SDK à l'intérieur de l'application du lecteur. L’un des effets des appels sur le Web est que le lecteur mettant en œuvre l’API Media Collection doit gérer une partie du traitement que le kit SDK Media gère automatiquement. (Details in [Media Collection Implementation.](mc-api-impl/mc-api-quick-start.md))

Les données de suivi capturées avec l'API de collecte de médias sont envoyées et traitées initialement différemment des données de suivi capturées dans un lecteur de SDK Media, mais le même moteur de traitement sur le serveur principal est utilisé pour les deux solutions.

![](assets/col_api_overview_simple.png)

## API Overview {#section_y4n_mcl_kcb}

**URI :** Procurez-vous cette information auprès de votre représentant Adobe.

**Méthode HTTP :** POST, avec corps de requête JSON.

### API Calls {#mc-api-calls}

* **`sessions`-** Établit une session avec le serveur et renvoie un ID de session utilisé dans `events` les appels suivants. Votre application appelle ceci une fois au début d’une session de suivi.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** Envoie les données du suivi multimédia.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Request Body {#mc-api-request-body}

```
{ 
    "playerTime": { 
        "playhead": {playhead position in seconds}, 
        "ts": {timestamp in milliseconds} 
    }, 
    "eventType": {event-type}, 
    "params": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "qoeData" : { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "customMetadata": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    } 
} 
```

* `playerTime` - obligatoire pour toutes les requêtes.
* `eventType` - obligatoire pour toutes les requêtes.
* `params` : Obligatoire pour certains `eventTypes` ; vérifiez le [schéma de validation JSON](mc-api-ref/mc-api-json-validation.md) pour déterminer quels eventTypes sont obligatoires et lesquels sont facultatifs.

* `qoeData` - Facultatif pour toutes les requêtes.
* `customMetadata` - Facultatif pour toutes les requêtes, mais uniquement envoyé avec `sessionStart`, `adStart`et les types `chapterStart` d'événement.

Pour chaque `eventType`, il existe un [schéma de validation JSON](mc-api-ref/mc-api-json-validation.md) disponible publiquement que vous devez utiliser pour vérifier les types de paramètre et savoir si un paramètre est facultatif ou obligatoire pour un événement particulier.

### Types d’événement {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`

