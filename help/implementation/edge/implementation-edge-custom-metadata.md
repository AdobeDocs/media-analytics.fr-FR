---
title: Prise en charge des métadonnées personnalisées - Format XDM
description: Découvrez comment envoyer des métadonnées personnalisées avec des événements de suivi multimédia à l’aide du format XDM Experience Edge.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 80caffab1630b138724b310e3bdcc58f682a2f8b
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---


# Prise en charge des métadonnées personnalisées - Format XDM

L’API Experience Edge vous permet d’envoyer des métadonnées personnalisées de média avec des champs XDM standard dans des événements d’API `sessionStart`, `adStart` et `chapterStart`. Les métadonnées personnalisées de média envoyées via le format XDM peuvent être transférées vers **&#x200B;**&#x200B;et **Adobe Experience Platform**.

Pour les implémentations de l’API Media Collection, voir [Prise en charge des métadonnées personnalisées](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md).

## Vue d’ensemble

Les métadonnées personnalisées de média peuvent être envoyées à deux emplacements dans une requête Experience Edge, chacun avec un comportement de routage différent :

| Emplacement | Envoyé à Adobe Analytics | Envoyé à Adobe Experience Platform | Exemple d’utilisation |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅ Oui | ✅ Oui | Données métiers nécessaires dans les deux systèmes |
| `_data` | ✅ Oui | ❌ No | Indicateurs spécifiques à Analytics ou indications de traitement |

Les métadonnées personnalisées s’appliquent à trois types d’événements :

| Événement | Les Métadonnées S’Appliquent À |
|-------|-------------------|
| `sessionStart` | Contenu principal (session entière) |
| `adStart` | Publicité individuelle |
| `chapterStart` | Chapitre ou segment de contenu |

## Structure

### `xdm.mediaCollection.customMetadata` (Analytics + AEP)

Les métadonnées personnalisées sont un **tableau d’objets nom-valeur** à l’intérieur de l’objet `mediaCollection` :

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

&lt;InlineAlert variant="warning" slots="text" />

`customMetadata` doit être un **tableau** à l’intérieur du `mediaCollection`, et non au niveau racine `xdm`.

**Incorrect:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**Correct :**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data` (Analytics uniquement)

L’objet `_data` est un concept d’Experience Edge spécial qui envoie des données exclusivement à Adobe Analytics, en contournant les jeux de données AEP. Les métadonnées personnalisées doivent être placées sous `__adobe.analytics.contextData`.

Contrairement à `xdm.mediaCollection.customMetadata` qui utilise un **tableau d’objets nom-valeur**, le mappage `_data` utilise un **objet clé-valeur** plat directement sous `contextData` :

| Approche | Structure | Destination |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | Tableau d’objets `{"name": "...", "value": "..."}` | Analytics + AEP |
| `_data.__adobe.analytics.contextData` | `{"key": "value"}` d’objet clé-valeur plate | Analytics uniquement |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### Conventions de dénomination

- **Format XDM :** préfixe avec espace de noms client utilisant un trait de soulignement. Vous pouvez également créer des structures dans votre groupe de champs personnalisés client, telles que `_<tenant>.<struct_name>.<field_name>`.
- **`_data`format : les champs** sont placés sous `_data.__adobe.analytics.contextData` — aucun préfixe de trait de soulignement n’est requis sur le nom du champ (par exemple, `debugFlag`)

## Métadonnées personnalisées du contenu principal

Envoyé avec `sessionStart`. S’applique au média principal faisant l’objet d’un suivi et reste disponible tout au long des appels de publicité et de chapitre. Toutes les métadonnées personnalisées définies ici seront automatiquement fusionnées par le serveur principal du média lors des appels de fermeture correspondants. Elle est incluse avec toute métadonnée personnalisée spécifique définie pour les annonces publicitaires et les chapitres.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Requête

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## Ajout de métadonnées personnalisées

Envoyé avec `adStart`. Spécifique à chaque publicité individuelle. Les métadonnées personnalisées d’`sessionStart` sont également automatiquement fusionnées par le serveur principal du média lors de l’appel de fermeture de l’annonce publicitaire avec toutes les métadonnées personnalisées spécifiques à l’annonce définies ici.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Requête

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## Métadonnées personnalisées de chapitre

Envoyé avec `chapterStart`. Spécifique à chaque chapitre ou segment de contenu. Les métadonnées personnalisées de `sessionStart` sont également automatiquement fusionnées par le serveur principal de médias lors de l’appel de fermeture du chapitre avec toutes les métadonnées personnalisées spécifiques au chapitre définies ici.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Requête

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## Utilisation de l’objet `_data` (métadonnées Analytics uniquement)

Utilisez l’objet `_data` lorsque vous avez besoin de métadonnées dans Adobe Analytics qui ne doivent **pas** être stockées dans des jeux de données AEP (par exemple, des indicateurs temporaires, des variables de débogage ou des indications de traitement spécifiques à Analytics).

&lt;InlineAlert variant="warning" slots="text" />

Les données envoyées via `_data` ne sont pas stockées dans Adobe Experience Platform et ne sont pas disponibles pour Real-Time CDP, Journey Orchestration ou d’autres services AEP.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Requête

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

Dans cet exemple :

- `_mycompany.league` → envoyées à Analytics et à AEP
- `debugMode` et `testFlag` (sous `_data.__adobe.analytics.contextData`) → envoyés à Analytics uniquement


## Emplacement des données en aval

&lt;InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata` est le **chemin d’API entrant** utilisé pour envoyer des métadonnées personnalisées avec des événements. Après traitement, les données sont transférées vers Adobe Analytics en tant que variables de données contextuelles et stockées dans Adobe Experience Platform sous `mediaReporting.customMetadata` et en tant que champs aplatis de niveau supérieur.

**Adobe Analytics :**

- Après traitement, les métadonnées personnalisées sont transférées vers Adobe Analytics en tant que variables de données contextuelles. Le préfixe `_tenant` est automatiquement supprimé. Les règles de traitement ne référencent donc que le chemin du champ après `_tenant` (par exemple, `_mycompany.contentCategory` devient `contentCategory`)
- Les données envoyées via `_data` sont également transférées vers Adobe Analytics et disponibles via des règles de traitement
- Utilisez des règles de traitement pour mapper des variables de données contextuelles à des eVars, des props ou d’autres variables Analytics. Pour plus d’informations, consultez [Mappage de variables de données pour Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/data-var-mapping).

**Adobe Experience Platform:**

- Les champs de métadonnées personnalisés doivent être définis comme des champs personnalisés dans votre schéma XDM (par exemple, `_mycompany`) et ils peuvent être stockés et interrogés dans AEP sous la forme de champs aplatis

  ![Définition d’un champ personnalisé dans un schéma XDM](assets/custom_metadata.png)
- Pour les rapports et les requêtes, les métadonnées personnalisées sont disponibles sous `mediaReporting.customMetadata` ainsi que sous la forme de champs aplatis de niveau supérieur. Utilisez la solution la plus adaptée à votre cas d’utilisation.
- Accessible pour la segmentation, Journey Orchestration et l’activation de Real-Time CDP

## Comportement

- Toutes les valeurs de métadonnées personnalisées doivent être des **chaînes**. Convertissez les nombres et les booléens avant l’envoi.
- `sessionStart` métadonnées sont conservées pendant toute la session ; les mises à jour nécessitent une nouvelle session
- Chaque événement `adStart` et `chapterStart` peut comporter différentes métadonnées personnalisées
- Préférez les champs XDM standard (`sessionDetails`, `advertisingDetails`, `chapterDetails`) aux métadonnées personnalisées lorsqu’un champ standard existe


## Documentation connexe

- [&#x200B; Prise en charge des métadonnées personnalisées &#x200B;](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md). — API MC (format JSON)
- [Type de données Détails de la collecte de médias &#x200B;](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/media-collection-details) — Référence du schéma XDM
- [&#x200B; Mappage des variables de données pour Adobe Experience Platform Edge Network &#x200B;](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/data-var-mapping) — Mappage des données contextuelles Analytics pour les champs XDM

<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->
