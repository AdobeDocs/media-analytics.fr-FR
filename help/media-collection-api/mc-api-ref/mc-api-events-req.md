---
seo-title: Requête events
title: Requête events
uuid: b 237 f 0 a 0-dc 29-418 b -89 ee -04 c 596 a 27 f 39
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Requête events{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Paramètre URI

`sid`: ID de session renvoyé par une [demande de session.](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Corps de la demande

Le corps de la demande doit être JSON et doit avoir la même structure que cet exemple de corps de demande :

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Obligatoire)
   * `playhead` : Doit être spécifié en secondes, mais peut être une valeur flottante.
   * `ts` : Horodatage ; doit être spécifié en millisecondes.
* `eventType` (Obligatoire)
* `params` (Facultatif)
* `customMetadata` (Facultatif ; send only with `adStart` and `chapterStart` event types)
* `qoeData` (Facultatif)

Pour obtenir la liste des types d’événement valides pour cette version, reportez-vous à la rubrique [Types et descriptions d’événement.](../../media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Suivi des publicités :**vous pouvez uniquement effectuer le suivi des publicités à l'intérieur d'`adBreak`* un seul.
>
>En l’absence des « serre-livres » `adBreakStart` et `adBreakComplete` autour des publicités, les événements `adStart` et `adComplete` sont simplement ignorés, et la durée de publicité correspondante est suivie en tant que durée de contenu principal. Cela pourrait avoir un impact significatif sur les données agrégées qui seront disponibles dans Adobe Analytics.

## Réponse

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## Codes de réponse HTTP

| Code de réponse HTTP | Description | Éléments d’action du client |
|---|---|---|
| **204** | **Aucun contenu.** <br/><br/>L’appel Heartbeat a réussi. | S.O. |
| **400** | **Demande incorrecte.** <br/><br/>Le format de la requête est incorrect. | Cherchez le type de requête dans les [schémas de validation JSON](../../media-collection-api/mc-api-ref/mc-api-json-validation.md). |
| **404** | **Introuvable.**<br/><br/>L'ID de session de la session multimédia est introuvable dans le service principal. | L’application du client doit utiliser l’API de la [requête sessions](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour créer une autre session multimédia et générer des rapports de suivi sur celle-ci. |
| **410** | **Supprimé.**<br/><br/>La session de média a été trouvée dans le service principal mais le client ne peut plus les rapporter. | L’application du client doit utiliser l’API de la [requête sessions](../../media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour créer une autre session multimédia et générer des rapports de suivi sur celle-ci. |
| **500** | **Erreur interne du serveur** | S.O. |

