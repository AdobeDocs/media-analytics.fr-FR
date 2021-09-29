---
title: API Streaming Media Collection - Point dʼentrée de requêtes de sessions
description: « Quels sont les paramètres et les réponses des points d’entrée de requêtes de sessions de l’API Media Collection ? »
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ef881900766be773256e2732953f7b63c5d488fa
workflow-type: ht
source-wordcount: '130'
ht-degree: 100%

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
   * `playhead` - Si le contenu est diffusé en direct, la tête de lecture doit correspondre à la seconde actuelle du jour, 0 &lt;= tête de lecture &lt; 86400. Si le contenu est enregistré, la tête de lecture doit correspondre à la seconde actuelle du contenu, 0 &lt;= tête de lecture &lt; durée du contenu. La valeur peut être un nombre à virgule flottante.
   * `ts` - Date et heure ; doit être en millisecondes ; Temps universel coordonné (UTC).
* `eventType` (Obligatoire)

   **Valeur valide :** `sessionStart`
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
