---
title: Schémas de validation JSON
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Schémas de validation JSON {#json-validation-schemas}

Le serveur principal Media Analytics valide les paramètres de requête pour chaque type d’événement à l’aide des schémas de validation JSON. Ces schémas sont à votre disposition et constituent l’autorité actuelle concernant les types de paramètre utilisés dans l’API MA.

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

Pour plus d’informations sur l’utilisation des schémas de validation JSON, reportez-vous à la rubrique [Validation des requêtes d’événement.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
