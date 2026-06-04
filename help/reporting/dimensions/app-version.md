---
title: Version de l’application
description: Indique la version de l’application de lecteur multimédia utilisée pour chaque session de diffusion en continu.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---


# Version de l’application

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Version de l’application**. Voir [Version de l’application](/help/implementation/variables/core/app-version.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Version de l’application** indique la chaîne de version de l’application du lecteur multimédia configurée à l’initialisation de SDK. Utilisez-le pour identifier les versions du lecteur en cours d’utilisation, corrélez les changements de qualité ou de comportement avec des versions spécifiques et donnez la priorité à la prise en charge des versions couramment utilisées.

>[!NOTE]
>
>Cette dimension capture la version de votre **application de lecteur multimédia**, et non la bibliothèque SDK Adobe. La version de la bibliothèque SDK d’Adobe est collectée automatiquement en tant que champ interne distinct.

## Mode de remplissage de cette dimension

La version de l’application est définie une seule fois lors de l’initialisation de SDK et est automatiquement incluse dans chaque requête de démarrage de session.

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Collecté automatiquement via le mappage des champs XDM lors de l’utilisation d’implémentations Edge. Pour les implémentations Analytics uniquement, mappez les `media.sdkVersion` de données contextuelles à un eVar personnalisé à l’aide d’une [&#x200B; règle de traitement &#x200B;](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md). |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | Aucune colonne de flux de données dédiée. Pour les implémentations Analytics uniquement, utilisez la colonne de flux de données de l’eVar personnalisée configurée via la règle de traitement. |
| Audience Manager | `c_contextdata.media.sdkVersion` (implémentations Analytics uniquement) |

## Éléments de dimension

Chaque élément correspond à la chaîne de version littérale configurée à l’initialisation de SDK. Utilisez un schéma de version cohérent dans toutes vos implémentations afin que les chaînes de version soient cumulées de manière prévisible dans les rapports.
