---
title: En Savoir Plus Sur Les Chronologies De Suivi Multimédia
description: Explorez plus en détail la chronologie du curseur de lecture et les actions de l’utilisateur correspondant. Découvrez les détails de chaque action et des demandes qui l’accompagnent.
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
exl-id: 16b15e03-5581-471f-ab0c-077189dd32d6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 97%

---

# Chronologie 1 : Regarder jusqu’à la fin du contenu{#timeline-view-to-end-of-content}

## VOD, publicités preroll, mise en pause, mise en mémoire tampon, affichage du contenu jusqu’à la fin

Les diagrammes suivants illustrent la chronologie du curseur de lecture et la chronologie correspondante des actions d’un utilisateur. Les détails de chaque action et des demandes qui l’accompagnent sont présentés ci-dessous.

![Contenu de l’API](assets/va_api_content.png)

![Actions de l’API](assets/va_api_actions.png)

## Détails de l’action

### Action 1 - Démarrage de la session {#Action-1}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Bouton Lecture automatique ou bouton Lecture enfoncé, début du chargement de la vidéo. | 0 | 0 | `/api/v1/sessions` |

Cet appel signale _l’intention de l’utilisateur de lire_ une vidéo.

Il renvoie un ID de session (`{sid}`) au client, utilisé pour identifier tous les appels de suivi suivants dans la session. L’état du lecteur n’est pas encore « lecture », mais à la place, « démarrage ». 

Les paramètres de session obligatoires doivent être inclus dans la carte `params` du corps de la requête. Pour plus d’informations sur les sessions, consultez la documentation de l’API Media Collection.

Sur le serveur principal, cet appel génère un appel de lancement d’Adobe Analytics.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"sessionStart, params" {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Action 2 - Démarrage du minuteur de ping {#Action-2}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application démarre le minuteur d’événement de ping | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

Démarrez le minuteur de ping de votre application. Le premier événement ping doit alors se déclencher après 1 seconde en cas de publicités preroll ou après 10 secondes dans le cas contraire.

### Action 3 - Début de la coupure publicitaire {#Action-3}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Suivi du début de la coupure publicitaire preroll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Les publicités ne peuvent être suivies que dans une coupure publicitaire.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Action 4 - Démarrage de la publicité {#Action-4}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité preroll N°1 commence | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Démarrez le suivi de la première publicité preroll, qui dure 15 secondes. Incluez des métadonnées personnalisées avec ce `adStart` .

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType":"adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement"
    },
    "customMetadata": {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

**REMARQUE : entre les événements AdBreakStart et AdStart, aucun événement de lecture supplémentaire ne devrait se produire.**

### Action 5 - Pings de publicité {#Action-5}

#### Action 5.1 - Ping de publicité 1 {#Action-5-1}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les secondes pendant dans une publicité.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### Action 5.2 - Ping de publicité 2 {#Action-5-2}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 2 | 0 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les secondes pendant dans une publicité.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

#### Action 5.3 - Ping de publicité 3 {#Action-5-3}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 3 | 0 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les secondes pendant dans une publicité.

>[!NOTE]
>
>Les publicités suivantes dans la chronologie ne montrent pas la série de pings d’une seconde
>par souci de concision...

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Action 6 - Fin de la publicité {#Action-6}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité preroll N°1 est terminé | 15 | 0 | `/api/v1/sessions/{sid}/events` |

Suivez la fin de la première publicité preroll.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Action 7 - Démarrage de la publicité {#Action-7}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité preroll N°2 commence | 15 | 0 | `/api/v1/sessions/{sid}/events` |

Suivez le début de la seconde publicité preroll, qui dure 7 secondes.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 8 - Pings de publicité {#Action-8}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 20 | 0 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les secondes.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Action 9 - Fin de la publicité {#Action-9}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité preroll N°2 est terminé | 22 | 0 | `/api/v1/sessions/{sid}/events` |

Suivez la fin de la seconde publicité preroll.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Action 10 - Fin de la coupure publicitaire {#Action-10}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la coupure publicitaire preroll est terminé | 22 | 0 | `/api/v1/sessions/{sid}/events` |

La coupure publicitaire est terminée. Tout au long de la coupure publicitaire, l’état de lecture est resté sur « lecture ».

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Action 11 - Lecture du contenu {#Action-11}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Suivi de l’événement de lecture | 22 | 0 | `/api/v1/sessions/{sid}/events` |

Après l’événement `adBreakComplete`, placez le lecteur à l’état « lecture » à l’aide de l’événement `play`.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### Action 12 - Ping {#Action-12}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 30 | 8 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes.

```json
{
    "playerTime": {
        "playhead": 8,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Action 13 - Début de la mémoire tampon {#Action-13}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’événement de début de la mémoire tampon a eu lieu | 33 | 11 | `/api/v1/sessions/{sid}/events` |

Suivez le déplacement du lecteur à l’état « mise en mémoire tampon ».

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    }, "eventType": "bufferStart"
}
```

### Action 14 - Fin de la mémoire tampon {#Action-14}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| La mémoire tampon a pris fin, l’application suit la reprise du contenu | 36 | 11 | `/api/v1/sessions/{sid}/events` |

La mise en mémoire tampon se terminant au bout de 3 secondes, replacez le lecteur à l’état « lecture ». Vous devez envoyer un autre événement de suivi de lecture provenant de la mise en mémoire tampon.  **L’appel`play` après un `bufferStart` impliquant un appel « bufferEnd » au serveur principal,** un événement `bufferEnd` n’est pas nécessaire.

```json
{
    "playerTime": {
        "playhead": 11,
        "ts": "<timestamp>"
    },
    "eventType": "play"
}
```

### Action 15 - Ping {#Action-15}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 40 | 15 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes.

```json
{
    "playerTime": {
        "playhead": 15,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Action 16 - Début de la coupure publicitaire {#Action-16}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la coupure publicitaire mid-roll commence | 46 | 21 | `/api/v1/sessions/{sid}/events` |

Publicité mid-roll d’une durée de 8 secondes : envoyez `adBreakStart` .

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### Action 17 - Démarrage de la publicité {#Action-17}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité mid-roll N°3 commence | 46 | 21 | `/api/v1/sessions/{sid}/events` |

Suivez la publicité mid-roll.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://example.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Action 18 - Ping de publicité {#Action-18}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 50 | 21 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Action 19 - Fin de la publicité {#Action-19}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité mid-roll N°1 est terminé | 54 | 21 | `/api/v1/sessions/{sid}/events` |

La publicité mid-roll est terminée.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Action 20 - Fin de la coupure publicitaire {#Action-20}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité mid-roll est terminé | 54 | 21 | `/api/v1/sessions/{sid}/events` |

La coupure publicitaire est terminée.

```json
{
    "playerTime": {
        "playhead": 21,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Action 21 - Ping {#Action-21}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 60 | 27 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes.

```json
{
    "playerTime": {
        "playhead": 27,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Action 22 - Pause {#Action-22}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’utilisateur a appuyé sur Pause | 64 | 31 | `/api/v1/sessions/{sid}/events` |

L’action de l’utilisateur déplace l’état de lecture sur « pause ».

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    },
    "eventType": "pauseStart"
}
```

### Action 23 - Ping {#Action-23}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 70 | 31 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes. Le lecteur est toujours à l’état « mémoire tampon » ; l’utilisateur est bloqué à 20 secondes de contenu. Suractivité...

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Action 24 - Lecture {#Action-24}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’utilisateur a appuyé sur Lecture pour reprendre le contenu principal | 74 | 31 | `/api/v1/sessions/{sid}/events` |

Déplacez l’état de lecture sur « lecture ».  **L’appel `play` après un événement `pauseStart` impliquant un appel « resume » au serveur principal,** un événement `resume` n’est pas nécessaire.

```json
{
    "playerTime": {
        "playhead": 31,
        "ts": "<timestamp>"
    }, "eventType": "play"
}
```

### Action 25 - Ping {#Action-25}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 80 | 37 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes.

```json
{
    "playerTime": {
        "playhead": 37,
        "ts": "<timestamp>"
    }, "eventType": "ping"
}
```

### Action 26 - Fin de la session {#Action-26}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’utilisateur termine de regarder le contenu jusqu’à la fin. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

Envoyez `sessionComplete` au serveur principal pour indiquer que l’utilisateur a fini de regarder le contenu entier.

```json
{
    "playerTime": {
        "playhead": 45,
        "ts": "<timestamp>"
    }, "eventType": "sessionComplete"
}
```

>[!NOTE]
>
>**Aucun événement de recherche ? -** Il n’y a pas de prise en charge explicite des événements `seekStart` ou `seekComplete` dans l’API Media Collection. C’est parce que certains lecteurs génèrent un très grand nombre de ces événements lorsque l’utilisateur final est en train de balayer, et que plusieurs centaines d’utilisateurs pourraient facilement étrangler la bande passante réseau d’un service principal. Adobe évite un support explicite aux événements de recherche en calculant la durée des pulsations en fonction de l’horodatage de l’appareil, plutôt que de la position de la tête de lecture.
