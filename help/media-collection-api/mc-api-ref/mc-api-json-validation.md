---
title: Schémas de validation JSON
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '55'
ht-degree: 100%

---

# Schémas de validation JSON {#json-validation-schemas}

Le serveur principal Media Analytics valide les paramètres de requête pour chaque type d’événement à l’aide des schémas de validation JSON. Ces schémas sont à votre disposition et constituent l’autorité actuelle concernant les types de paramètre utilisés dans l’API MA.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Pour plus d’informations sur l’utilisation des schémas de validation JSON, reportez-vous à la rubrique [Validation des requêtes d’événement.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
