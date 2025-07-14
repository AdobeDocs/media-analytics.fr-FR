---
title: Découvrez les chronologies de suivi des médias ‐ Lʼutilisateur abandonne la session
description: Apprenez en plus sur la chronologie du curseur de lecture et lʼaction correspondante de lʼutilisateur lorsquʼune session vidéo est abandonnée. Découvrez les détails de chaque action et requête.
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
exl-id: 0c6a89f4-7949-4623-8ed9-ce1d1547bdfa
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 100%

---

# Chronologie 2 : L’utilisateur abandonne la session {#timeline--2-user-abandons-session}

## VOD, publicité preroll, publicités mid-roll, utilisateur abandonne le contenu tôt

Les diagrammes suivants illustrent la chronologie du curseur de lecture et la chronologie correspondante des actions d’un utilisateur. Les détails de chaque action et des demandes qui l’accompagnent sont présentés ci-dessous.

![Contenu de l’API](assets/va_api_content_2.png)

![Actions de l’API](assets/va_api_actions_2.png)

## Détails de l’action

### Action 1 - Démarrage de la session {#Action-1}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Bouton Lecture automatique ou bouton Lecture enfoncé | 0 | 0 | `/api/v1/sessions` |

Cet appel signale _l’intention de l’utilisateur de lire_ une vidéo. Il renvoie un ID de session (`{sid}`) au client, utilisé pour identifier tous les appels de suivi suivants dans la session. L’état du lecteur n’est pas encore « en cours de lecture », mais à la place, « en cours de démarrage ».  Les [paramètres de session obligatoires](../mc-api-ref/mc-api-sessions-req.md) doivent être inclus dans la carte `params` du corps de la requête.  Sur le serveur principal, cet appel génère un appel de lancement d’Adobe Analytics.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "sessionStart",
    "params": {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
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
| L’application démarre le minuteur d’événement de ping | 0 | 0 | |

Démarrez le minuteur de ping de votre application. Le premier événement ping doit alors se déclencher après 1 seconde en cas de publicités preroll ou après 10 secondes dans le cas contraire.

### Action 3 - Début de la coupure publicitaire {#Action-3}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Suivi du début de la coupure publicitaire preroll | 0 | 0 | `/api/v1/sessions/{sid}/events` |

Les publicités preroll doivent être suivies. Les annonces publicitaires ne peuvent être suivies que dans une coupure publicitaire.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakStart",
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

Une publicité de 12 secondes commence.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Action 5 - Pings de publicité {#Action-5}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les secondes. (Les pings de publicité suivants ne se pas montrés, dans un souci de concision.)

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
| Le suivi de la publicité preroll N°1 est terminé | 12 | 0 | `/api/v1/sessions/{sid}/events` |

La première publicité preroll est terminée.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adComplete"
}
```

### Action 7 - Fin de la coupure publicitaire {#Action-7}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la coupure publicitaire preroll est terminé | 12 | 0 | `/api/v1/sessions/{sid}/events` |

La coupure publicitaire est terminée. Tout au long de la coupure publicitaire, le lecteur est resté à l’état « lecture ».

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "adBreakComplete"
}
```

### Action 8 - Lecture du contenu {#Action-8}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Suivi de l’événement de lecture | 12 | 0 | `/api/v1/sessions/{sid}/events` |

Déplacez le lecteur vers l’état « en cours de lecture » ; commencez le suivi du début de la lecture du contenu.

```json
{
    "playerTime": {
        "playhead": 0,
        "ts": "<timestamp>"
    },
    "eventType": "play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Action 9 - Ping {#Action-9}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 20 | 8 | `/api/v1/sessions/{sid}/events` |

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

### Action 10 - Ping {#Action-10}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 30 | 18 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes.

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Action 11 - Erreur {#Action-11}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Une erreur se produit, l’application envoie des informations d’erreur. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 20,
        "ts": "<timestamp>"
    },
    "eventType": "error"
}
```

### Action 12 - Lecture du contenu {#Action-12}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application récupère après l’erreur, l’utilisateur appuie sur Lecture. | 37 | 20 | `/api/v1/sessions/{sid}/events` |

```json
{
    "playerTime": {
        "playhead": 18,
        "ts": "<timestamp>"
    },
    "eventType":"play",
    "qoeData": {
        "bitrate": 10000
    }
}
```

### Action 13 - Ping {#Action-13}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’application envoie un événement ping | 40 | 28 | `/api/v1/sessions/{sid}/events` |

Envoyez un ping au serveur principal toutes les 10 secondes.

```json
{
    "playerTime": {
        "playhead": 28,
        "ts": "<timestamp>"
    },
    "eventType": "ping"
}
```

### Action 14 - Début de la coupure publicitaire {#Action-14}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la coupure publicitaire mid-roll commence | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Annonce publicitaire mid-roll d’une durée de 8 secondes : envoyez `adBreakStart`.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType":"adBreakStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Action 15 - Démarrage de la publicité {#Action-15}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| Le suivi de la publicité mid-roll N°1 commence | 45 | 33 | `/api/v1/sessions/{sid}/events` |

Suivez l’annonce publicitaire mid-roll.

```json
{
    "playerTime": { "playhead": 33, "ts": "<timestamp>"
    },
    "eventType": "adStart",
    "params": {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
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

### Action 16 - Fermeture de l’application {#Action-16}

| Action | Chronologie des actions (secondes) | Position du curseur de lecture (secondes) | Demande client |
| --- | :---: | :---: | --- |
| L’utilisateur ferme l’application. L’application détermine que l’utilisateur a abandonné l’affichage et ne revient pas sur cette session. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

Envoyez `sessionEnd` au serveur principal VA pour indiquer que la session doit être fermée immédiatement, sans autre traitement.

```json
{
    "playerTime": {
        "playhead": 33,
        "ts": "<timestamp>"
    },
    "eventType": "sessionEnd"
}
```
