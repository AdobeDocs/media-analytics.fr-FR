---
title: Média téléchargé
description: Indique les sessions qui ont lu du contenu hors ligne téléchargé.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 6%

---


# Média téléchargé

>[!BEGINSHADEBOX]

*Cette page couvre la dimension de reporting **Médias téléchargés**. Voir [Indicateur de média téléchargé](/help/implementation/variables/core/media-downloaded-flag.md) pour savoir comment collecter cette variable.*

>[!ENDSHADEBOX]

La dimension **Média téléchargé** signale les sessions qui ont lu du contenu hors ligne précédemment téléchargé plutôt qu’un flux en direct depuis Internet. Utilisez-le pour séparer la lecture hors ligne des sessions en flux continu lors de la comparaison de l’engagement, de l’achèvement ou de la qualité.

## Mode de remplissage de cette dimension

L’indicateur téléchargé est défini par le lecteur de l’une des trois façons suivantes. Initialisez le dispositif de suivi avec l’indicateur (Mobile SDK), envoyez le `sessionStart` à la variante de point d’entrée `/downloaded` (API Media Edge directe) ou incluez le `media.downloaded: true` dans les paramètres `sessionStart` (API Media Collection).

| Système de reporting | Source |
| --- | --- |
| Adobe Analytics | Créez une [règle de traitement](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) qui mappe le `a.media.downloaded` à un eVar. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Flux de données | `evar1`-`evar250`, `post_evar1`-`post_evar250` (l’eVar à laquelle votre règle de traitement `a.media.downloaded` mappée) |

## Éléments de dimension

| Valeur | Description |
| --- | --- |
| `true` | La session a été lue et le contenu a été téléchargé hors ligne. |
| (vide) | La session a été diffusée en direct. Le champ est omis plutôt que défini sur `false`. |
