---
title: Présentation des variables de streaming multimédia
description: Découvrez comment les variables de médias en flux continu sont organisées et comment elles sont mappées dans Adobe Analytics et Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---


# Présentation des variables de streaming multimédia

Les variables sont les données que votre lecteur multimédia fournit sur un flux, telles que le nom du contenu, le type de flux, le nom de l’annonce publicitaire et la qualité de lecture. La plupart des variables sont définies au début de la session et transmises jusqu’à la session fermée par le serveur principal du média, qui les utilise pour renseigner les dimensions et les mesures que vous utilisez dans les rapports. Chaque page de variable explique comment définir cette variable pour chaque méthode d’implémentation prise en charge.

## Envoi des variables à Adobe

Une seule variable transfère la même valeur vers chaque application ou service Adobe, mais le format de cette valeur dépend de l’endroit où vous l’envoyez. Le tableau suivant répertorie chaque application ou service et le format de variable attendu. Le tableau des propriétés de chaque page de variable indique la valeur exacte à utiliser dans chaque format.

| Format des données | Description |
| --- | --- |
| Variable de données contextuelles | Format envoyé à Adobe Analytics, nommé avec un préfixe `a.media` (tel que `a.media.name`). |
| Champ de collection XDM | Format envoyé à Customer Journey Analytics, exprimé sous la forme d’un chemin d’accès au champ XDM (`xdm.mediaCollection.sessionDetails.name`, par exemple). |
| caractéristique Audience Manager | Format transféré vers Audience Manager, précédé du préfixe `c_contextdata` (`c_contextdata.a.media.name`, par exemple). |

>[!MORELIKETHIS]
>
>* [Présentation des événements](/help/implementation/events/overview.md) : événements du lecteur qui comportent des variables
>* [Présentation des dimensions](/help/reporting/dimensions/overview.md) : dimensions de rapport renseignées par les variables
>* [Présentation des mesures](/help/reporting/metrics/overview.md) : mesures de reporting renseignées par les variables
