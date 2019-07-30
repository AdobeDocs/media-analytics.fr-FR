---
seo-title: Prise en charge des métadonnées personnalisées
title: Prise en charge des métadonnées personnalisées
uuid: df 4109 dd -9 fca -4 c 33-a 7 d 5-8 e 6 eec 257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Prise en charge des métadonnées personnalisées{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Ces informations doivent être fournies dans la clé JSON, `customMetadata`, positionnées à côté de la clé `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. La clé ne doit contenir que des caractères alphanumériques, un caractère de soulignement et un point.

[Événements API Collection MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

