---
seo-title: Overview
title: Présentation de l’API Streaming Media Collection
description: Découvrez l’API Media Collection et la façon dont votre lecteur peut suivre les événements vidéo et audio à l’aide d’appels HTTP RESTful.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '357'
ht-degree: 100%

---

# Présentation de l’API Media Collection{#overview}

L’API Media Collection constitue l’alternative RESTful d’Adobe au SDK Media côté client. Grâce à l’API Media Collection, votre lecteur peut effectuer le suivi des événements audio et vidéo à l’aide d’appels HTTP RESTful.

L’API Media Collection est essentiellement un adaptateur, agissant comme une version côté serveur du SDK Media. Cela signifie que certains aspects de la documentation du SDK Media sont également pertinents pour l’API Media Collection. Par exemple, les deux solutions utilisent les mêmes [paramètres de médias en flux continu](../variables/audio-video-parameters.md), et les données de suivi de médias en flux continu collectées conduisent aux mêmes [rapports et analyses.](/help/reporting/media-reports-enable.md)

## Flux de données de suivi multimédia {#media-tracking-data-flows}

Un lecteur multimédia mettant en œuvre l’API Media Collection effectue des appels de suivi d’API RESTful directement au serveur principal de suivi multimédia, tandis qu’un lecteur mettant en œuvre le kit SDK Media effectue des appels de suivi aux API SDK dans l’application de lecteur. L’un des effets des appels sur le Web est que le lecteur mettant en œuvre l’API Media Collection doit gérer une partie du traitement que le kit SDK Media gère automatiquement. (Détails dans [Mise en œuvre de Media Collection.](mc-api-impl/mc-api-quick-start.md))

Les données de suivi capturées avec l’API Media Collection sont envoyées et traitées initialement différemment des données de suivi capturées dans un lecteur SDK Media, mais le même moteur de traitement sur le serveur principal est utilisé pour les deux solutions.

![](assets/col_api_overview_simple.png)

## Présentation de l’API {#api-overview}

**URI :** procurez-vous cette information auprès de votre représentant Adobe.

**Méthode HTTP :** POST, avec corps de requête JSON.

### Appels API {#mc-api-calls}

* **`sessions`-** Établit une session avec le serveur et renvoie un ID de session utilisé dans les appels `events` suivants. Votre application appelle ceci une fois au début d’une session de suivi.

   `{uri}/api/v1/sessions`

* **`events`-** Envoie des données de suivi multimédia.

   `{uri}/api/v1/sessions/{session-id}/events`

### Corps de requête {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` : Obligatoire pour toutes les requêtes.
* `eventType` : Obligatoire pour toutes les requêtes.
* `params` : Obligatoire pour certains `eventTypes` ; vérifiez le [schéma de validation JSON](mc-api-ref/mc-api-json-validation.md) pour déterminer quels eventTypes sont obligatoires et lesquels sont facultatifs.

* `qoeData` : Facultatif pour toutes les requêtes.
* `customMetadata` : Facultatif pour toutes les requêtes, mais uniquement envoyé avec les types d’événement `sessionStart`, `adStart` et `chapterStart`.

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
