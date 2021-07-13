---
title: Schémas de validation JSON des analyses de médias en flux continu
description: Que sont les schémas de validation JSON des médias en flux continu et comment sont-ils utilisés pour déterminer les paramètres corrects du corps de la requête pour chaque type d’événement ?
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 64%

---

# Schémas de validation JSON{#json-validation-schemas}

Le serveur principal Media Analytics valide les paramètres de requête pour chaque type d’événement à l’aide des schémas de validation JSON. Ces schémas sont à votre disposition et constituent l’autorité actuelle concernant les types de paramètre utilisés dans l’API MA.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Pour plus d’informations sur l’utilisation des schémas de validation JSON, reportez-vous à la rubrique [Validation des requêtes d’événement.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
