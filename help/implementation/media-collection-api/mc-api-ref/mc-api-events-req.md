---
title: Point d’entrée de requête d’événement de � de l’API Streaming Media Collection
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
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 0%

---

# Requête events{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## Paramètre URI

`sid` : ID de session renvoyé à partir d’une [requête Sessions](mc-api-sessions-req.md).

## Corps de la requête

Le corps de la requête doit être JSON et doit avoir la même structure que cet exemple de corps de requête :

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

* `playerTime` (obligatoire)
   * `playhead` - Doit être en secondes, mais il peut s’agir d’un flottant.
   * `ts` - Date et heure ; doit être en millisecondes.
* `eventType` (obligatoire)
* `params` (facultatif)
* `customMetadata` (facultatif ; envoyer uniquement avec les types d’événements `adStart` et `chapterStart`)
* `qoeData` (facultatif)

Pour obtenir une liste des types d’événements valides et des exemples d’implémentation par SDK, voir [Présentation des événements](/help/implementation/events/overview.md).

>[!IMPORTANT]
>
>***Suivi des annonces publicitaires -**vous pouvez uniquement effectuer le suivi des annonces publicitaires dans un`adBreak`*.
>
>En l’absence de `adBreakStart` et `adBreakComplete` « fins de livre » autour des publicités, les événements `adStart` et `adComplete` seront simplement ignorés et la durée de la publicité correspondante sera suivie en tant que durée du contenu principal. Cela pourrait avoir un impact significatif sur les données agrégées qui seront disponibles dans Adobe Analytics.

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

| Code de réponse HTTP | Description | Éléments d&#39;action client |
|---|---|---|
| **204** | **Pas de contenu.** <br/><br/>L’appel Heartbeat a réussi. | S.O. |
| 400 **** | **Requête incorrecte.** <br/><br/>Le format de la demande n’était pas correct. | Vérifiez le [Schémas de validation JSON](mc-api-json-validation.md) pour le type de requête. |
| 404 **** | **Introuvable.** <br/><br/>L’ID de session de la session multimédia est introuvable dans le service principal. | L’application cliente doit utiliser l’API [Sessions request](mc-api-sessions-req.md) pour créer une autre session multimédia et effectuer le suivi sur celle-ci dans des rapports. |
| 410 **** | **Parti.** <br/><br/>La session multimédia a été trouvée dans le service principal, mais le client ne peut plus y signaler d’activité. | L’application cliente doit utiliser l’API [Sessions request](mc-api-sessions-req.md) pour créer une autre session multimédia et effectuer le suivi sur celle-ci dans des rapports. |
| 500 **** | **Erreur du serveur** | S.O. |
