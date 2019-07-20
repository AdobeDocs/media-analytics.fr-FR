---
seo-title: Prise en charge des métadonnées personnalisées
title: Prise en charge des métadonnées personnalisées
uuid: df 4109 dd -9 fca -4 c 33-a 7 d 5-8 e 6 eec 257527
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Prise en charge des métadonnées personnalisées{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Ces informations doivent être fournies dans la clé JSON, `customMetadata`, positionnées à côté de la clé `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. La clé ne doit contenir que des caractères alphanumériques, un caractère de soulignement et un point.

[Événements API Collection MA](../mc-api-ref/mc-api-events-req.md)

