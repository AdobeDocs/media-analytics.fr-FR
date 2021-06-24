---
title: Prise en charge des métadonnées personnalisées
description: '"Découvrez comment fournir des paires clé-valeur personnalisées sur les événements sessionStart, chapterStart et adStart."'
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 88%

---

# Prise en charge des métadonnées personnalisées{#custom-metadata-support}

Vous pouvez fournir des paires clé-valeur personnalisées sur les événements `sessionStart`, `chapterStart` et `adStart`. Ces informations doivent être fournies dans la clé JSON, `customMetadata`, positionnées à côté de la clé `params`.

La clé JSON `customMetadata` doit contenir un objet de paires clé-valeur. La clé ne doit contenir que des caractères alphanumériques, un caractère de soulignement et un point.

[Événements d’API MA Collection](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## Exemple

Actuellement, vous pouvez envoyer un événement `sessionStart` avec la paire clé-valeur suivante :

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Pour la configuration ci-dessus, les données de rapport envoyées à Analytics sont les suivantes :

`c.a.media.channel=channel-2`

### Recommandation

Nous vous recommandons d’utiliser un espace de noms distinct pour les métadonnées personnalisées. Par exemple :

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

Dans l’exemple recommandé, les données de rapport pour les métadonnées personnalisées envoyées à Analytics sont les suivantes :

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
