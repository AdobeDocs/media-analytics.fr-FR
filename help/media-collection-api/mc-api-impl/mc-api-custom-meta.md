---
title: Prise en charge des métadonnées personnalisées
description: Prise en charge des métadonnées personnalisées
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
source-git-commit: 962bb8b6859ca8964efcb2f3ba0dc566a5e24c3e
workflow-type: ht
source-wordcount: '115'
ht-degree: 100%

---

# Prise en charge des métadonnées personnalisées {#custom-metadata-support}

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
