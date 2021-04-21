---
title: Requête events
description: Requête events
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 100%

---

# Requête events {#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Paramètre URI

`sid` : ID de session renvoyé à partir d’une [requête sessions.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Corps de requête

Le corps de requête doit être JSON et doit avoir la même structure que le corps de cet exemple de corps de requête :

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
* `customMetadata` (Facultatif ; envoyer uniquement avec les types d’événements `adStart` et `chapterStart`)
* `qoeData` (Facultatif)

Pour obtenir la liste des types d’événement valides pour cette version, reportez-vous à la rubrique [Types et descriptions d’événement.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Suivi des publicités -** Vous pouvez uniquement suivre les publicités dans un`adBreak`*.
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

| Code de réponse HTTP | Description | Éléments d’action client |
|---|---|---|
| **204** | **Aucun contenu.** <br/><br/>L’appel Heartbeat a réussi. | S.O. |
| **400** | **Requête incorrecte.**<br/><br/>Le format de la requête est incorrect. | Recherchez les [schémas de validation JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) pour le type de requête. |
| **404** | **Non trouvé.** <br/><br/>L’ID de session pour la session multimédia n’a pas été trouvé dans le service principal. | L’application client doit utiliser l’API de [demande Sessions](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour créer une autre session multimédia et en effectuer le suivi dans les rapports. |
| **410** | **Parti.** <br/><br/>La session multimédia a été trouvée dans le service principal, mais le client ne peut plus générer de rapports d’activité sur celle-ci. | L’application client doit utiliser l’API de [demande Sessions](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) pour créer une autre session multimédia et en effectuer le suivi dans les rapports. |
| **500** | **Erreur du serveur** | S.O. |
