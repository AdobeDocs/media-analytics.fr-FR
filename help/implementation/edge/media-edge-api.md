---
title: Configurer l’API Media Edge pour les médias en flux continu
description: Envoyez directement des données de médias en flux continu à Edge Network à l’aide de l’API Media Edge.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Configurer l’API Media Edge pour les médias en flux continu

Si vous ne pouvez pas utiliser Web SDK, Mobile SDK ou Roku SDK (par exemple, sur un runtime personnalisé ou non pris en charge), vous pouvez envoyer directement des données de médias en flux continu à Edge Network à l’aide de l’API Media Edge. L’API utilise des appels HTTP RESTful et est entièrement personnalisable.

* **Conditions préalables** : terminez la [présentation de l’implémentation d’Edge](overview.md) (schéma, jeu de données, flux de données avec [!UICONTROL Media Analytics] activé).

## Envoi d’événements multimédia à Edge Network

Les événements multimédia sont envoyés aux points d’entrée `/ee/va/v1/`, indexés à votre flux de données par le paramètre de requête `configId`. Par exemple, une session commence par une requête POST à `sessionStart` :

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

La réponse renvoie l’identifiant de session que tous les événements suivants doivent inclure. Pour le jeu de points d’entrée complet, les formats de requête/réponse et la spécification OpenAPI, consultez la [Référence de l’API Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

## Suivi des événements multimédia

Voir l’onglet **API Media Edge** sur chaque page [événement](/help/implementation/events/overview.md) et [variable](/help/implementation/variables/overview.md) pour connaître les payloads exactes.

## Étape suivante

Une fois l’implémentation terminée, vous pouvez [Configurer des rapports pour les implémentations d’Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Référence de l’API Media Edge ](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [Présentation des événements](/help/implementation/events/overview.md)
>* [Présentation des variables](/help/implementation/variables/overview.md)
