---
title: Prise en charge des métadonnées personnalisées
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Prise en charge des métadonnées personnalisées {#custom-metadata-support}

Vous pouvez fournir des paires clé-valeur personnalisées sur les événements `sessionStart`, `chapterStart` et `adStart`. Ces informations doivent être fournies dans la clé JSON, `customMetadata`, positionnées à côté de la clé `params`.

La clé JSON `customMetadata` doit contenir un objet de paires clé-valeur. La clé ne doit contenir que des caractères alphanumériques, un caractère de soulignement et un point.

[Evénements d’API MA Collection](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

