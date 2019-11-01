---
title: Requête events
description: null
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Requête events{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Paramètre URI

`sid`: ID de session renvoyé à partir d’une demande de [session.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Corps de requête

L’organisme de requête doit être JSON et avoir la même structure que cet organisme de requête d’exemple :

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
* `customMetadata` (Facultatif) envoyer uniquement avec les types `adStart` et `chapterStart` d’événements)
* `qoeData` (Facultatif)

Pour obtenir la liste des types d’événement valides pour cette version, reportez-vous à la rubrique [Types et descriptions d’événement.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Suivi des publicités -**Vous pouvez uniquement effectuer le suivi des publicités à l’intérieur d’une`adBreak`*.
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
| **400** | **Demande incorrecte.** <br/><br/>Le format de la requête est incorrect. | Cherchez le type de requête dans les [schémas de validation JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md). |
| **404** | **Introuvable.** <br/><br/>L'ID de session pour la session multimédia est introuvable dans le service principal. | L’application du client doit utiliser l’API de la [requête sessions](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour créer une autre session multimédia et générer des rapports de suivi sur celle-ci. |
| **410** | **Supprimé.** <br/><br/>La session multimédia a été trouvée dans le service principal, mais le client ne peut plus lui signaler l’activité. | L’application du client doit utiliser l’API de la [requête sessions](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour créer une autre session multimédia et générer des rapports de suivi sur celle-ci. |
| **500** | **Erreur interne du serveur** | S.O. |

