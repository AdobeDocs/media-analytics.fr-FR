---
title: Requête sessions
description: null
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Requête sessions {#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## Paramètres URI

Aucun

## Corps de requête

Le corps de requête doit être JSON et doit avoir la même structure que le corps de cet exemple de corps de requête :

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (Obligatoire)
   * `playhead` : Doit être spécifié en secondes, mais peut être une valeur flottante.
   * `ts` : Horodatage ; doit être spécifié en millisecondes.
* `eventType` (Obligatoire)

   **Valeur valide :**`sessionStart`
* `params` (Obligatoire)
* `customMetadata` (Facultatif)
* `qoeData` (Facultatif)

## Réponse

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` header - La partie `/api/v1/` fournit la version de l’API. La partie qui suit `[…]sessions/` correspond à l’ID de session.

## Codes de réponse

| Code de réponse HTTP | Description |
|---|---|
| 201 | Session créée |
| 400 | Requête incorrecte |
| 500 | Erreur du serveur |

