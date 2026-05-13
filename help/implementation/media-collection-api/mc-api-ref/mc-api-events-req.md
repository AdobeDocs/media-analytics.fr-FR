---
title: API Streaming Media Collection ‐ Point dʼentrée de la requête events
description: Quels sont les paramètres et les réponses des points d’entrée des requêtes d’événements de l’API Media Collection ?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 76%

---

# Requête events{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## Paramètre URI

`sid` : ID de session renvoyé à partir d’une [requête Sessions](mc-api-sessions-req.md).

## Corps de requête

Le corps de requête doit être JSON et doit avoir la même structure que le corps de cet exemple de corps de requête :

```json
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

Pour obtenir la liste des types d’événement valides pour cette version, reportez-vous à la rubrique [Types et descriptions d’événement.](mc-api-event-types.md)

>[!IMPORTANT]
>
>***Suivi des publicités -** Vous pouvez uniquement suivre les publicités dans un`adBreak`*.
>
>En l’absence des « serre-livres » `adBreakStart` et `adBreakComplete` autour des publicités, les événements `adStart` et `adComplete` sont simplement ignorés, et la durée de publicité correspondante est suivie en tant que durée de contenu principal. Cela pourrait avoir un impact significatif sur les données agrégées qui seront disponibles dans Adobe Analytics.

## Réponse

```text
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
| **204** | **Pas de contenu.** <br/><br/>L’appel Heartbeat a réussi. | S.O. |
| **400** | **Requête incorrecte.** <br/><br/>Le format de la demande n’était pas correct. | Recherchez les [schémas de validation JSON](mc-api-json-validation.md) pour le type de requête. |
| **404** | **Introuvable.** <br/><br/>L’ID de session de la session multimédia est introuvable dans le service principal. | L’application client doit utiliser l’API de [demande Sessions](mc-api-sessions-req.md) pour créer une autre session multimédia et en effectuer le suivi dans les rapports. |
| **410** | **Parti.** <br/><br/>La session multimédia a été trouvée dans le service principal, mais le client ne peut plus y signaler d’activité. | L’application client doit utiliser l’API de [demande Sessions](mc-api-sessions-req.md) pour créer une autre session multimédia et en effectuer le suivi dans les rapports. |
| **500** | **Erreur du serveur** | S.O. |
