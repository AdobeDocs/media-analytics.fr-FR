---
seo-title: Prise en charge des métadonnées personnalisées
title: Prise en charge des métadonnées personnalisées
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Prise en charge des métadonnées personnalisées{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Ces informations doivent être fournies dans la clé JSON, `customMetadata`, positionnées à côté de la clé `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. La clé ne doit contenir que des caractères alphanumériques, un caractère de soulignement et un point.

[Evénements API de collection MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

