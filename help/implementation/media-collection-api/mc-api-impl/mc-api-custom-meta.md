---
title: Prise en charge des métadonnées personnalisées de l’API Media Collection
description: Découvrez comment fournir des paires clé-valeur personnalisées sur les événements sessionStart, chapterStart et adStart.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 435
ht-degree: 5%

---

# Prise en charge des métadonnées personnalisées de l’API Media Collection

L’API Media Collection vous permet d’envoyer des paires clé-valeur personnalisées avec des paramètres standard dans les événements `sessionStart`, `adStart` et `chapterStart`. Les métadonnées personnalisées sont transférées vers **&#x200B;**&#x200B;avec les événements de fermeture de média correspondants.

Pour rendre ces données disponibles dans Analysis Workspace, les clients doivent définir des eVars personnalisées et configurer des règles de traitement pour les remplir en fonction de leur cas d’utilisation. Une fois mappées à des eVars ou des props, les données sont également disponibles dans Adobe Experience Platform par le biais des chemins eVar correspondants, à condition que le [&#x200B; connecteur source Analytics &#x200B;](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/analytics) soit configuré.

Pour les implémentations basées sur XDM utilisant Experience Edge, consultez [Prise en charge des métadonnées personnalisées - Format XDM](/help/implementation/edge/custom-metadata.md).

## Vue d’ensemble

Les métadonnées personnalisées sont incluses dans le corps de la requête sous la forme d’un objet `customMetadata`, positionné à côté de la clé `params`. Elle s’applique à trois types d’événements :

| Événement | Les Métadonnées S’Appliquent À |
|-------|-------------------|
| `sessionStart` | Contenu principal (session entière) |
| `adStart` | Publicité individuelle |
| `chapterStart` | Chapitre ou segment de contenu |

## Structure

Les métadonnées personnalisées sont un **objet** plat (paires clé-valeur) au niveau de l’événement, avec la clé `params` :

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### Paramètres obligatoires par type d’événement

| Événement | `params` requis |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### Principales exigences en matière de dénomination

* Évitez d’utiliser le préfixe `media.` dans les clés de métadonnées personnalisées. Il mappe vers les champs de média standard et peut les remplacer dans les rapports Analytics
* Le préfixe `a.` est réservé aux métadonnées Adobe standard et ne doit pas être utilisé

## Métadonnées personnalisées du contenu principal

Envoyé avec `sessionStart`. S’applique au média principal faisant l’objet d’un suivi et reste disponible tout au long des appels de publicité et de chapitre. Toutes les métadonnées personnalisées définies ici seront automatiquement fusionnées par le serveur principal du média lors des appels de fermeture correspondants. Elle est incluse avec toute métadonnée personnalisée spécifique définie pour les annonces publicitaires et les chapitres.

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## Ajout de métadonnées personnalisées

Envoyé avec `adStart`. Spécifique à chaque publicité individuelle. Les métadonnées personnalisées d’`sessionStart` sont également automatiquement fusionnées par le serveur principal du média lors de l’appel de fermeture de l’annonce publicitaire avec toutes les métadonnées personnalisées spécifiques à l’annonce définies ici.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## Métadonnées personnalisées de chapitre

Envoyé avec `chapterStart`. Spécifique à chaque chapitre ou segment de contenu. Les métadonnées personnalisées de `sessionStart` sont également automatiquement fusionnées par le serveur principal de médias lors de l’appel de fermeture du chapitre avec toutes les métadonnées personnalisées spécifiques au chapitre définies ici.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## Comportement

* Toutes les valeurs de métadonnées personnalisées doivent être des **chaînes**. Convertissez les nombres et les booléens avant l’envoi.
* Les métadonnées personnalisées s’affichent dans Analytics avec un préfixe `c.` (par exemple, `contentCategory` → `c.contentCategory`)
* Mapper des métadonnées personnalisées à des eVars, des props ou des variables de données contextuelles via des règles de traitement Analytics
* `sessionStart` métadonnées sont conservées pendant toute la session ; les mises à jour nécessitent une nouvelle session
* Chaque événement `adStart` et `chapterStart` peut comporter différentes métadonnées personnalisées

>[!MORELIKETHIS]
>* [Prise en charge des métadonnées personnalisées - Format XDM](/help/implementation/edge/custom-metadata.md)
>* [Connecteur source Adobe Analytics pour les données de suite de rapports](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/analytics)
