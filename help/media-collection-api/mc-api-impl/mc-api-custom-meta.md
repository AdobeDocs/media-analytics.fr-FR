---
title: Prise en charge des métadonnées personnalisées
description: Prise en charge des métadonnées personnalisées
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# Prise en charge des métadonnées personnalisées {#custom-metadata-support}

Vous pouvez fournir des paires clé-valeur personnalisées sur les événements `sessionStart`, `chapterStart` et `adStart`. Ces informations doivent être fournies dans la clé JSON, `customMetadata`, positionnées à côté de la clé `params`.

La clé JSON `customMetadata` doit contenir un objet de paires clé-valeur. La clé ne doit contenir que des caractères alphanumériques, un caractère de soulignement et un point.

[Evénements d’API MA Collection](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
