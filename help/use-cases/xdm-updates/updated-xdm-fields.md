---
title: Migration d’une implémentation du connecteur source Analytics vers les champs XDM Streaming Media mis à jour
description: Découvrez comment migrer une implémentation du connecteur source Analytics vers des champs XDM Streaming Media mis à jour
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a0a357c3fe7e958b0b6491c84f17f26a806ea205
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Mettre à jour une implémentation du connecteur source Analytics vers de nouveaux champs XDM pour les médias en flux continu

>[!NOTE]
>
>Ces informations sont destinées aux organisations qui utilisent le connecteur source [Analytics](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/adobe-applications/analytics) pour importer des données de médias en flux continu d’Adobe Analytics dans Adobe Experience Platform en vue de les utiliser avec la création de rapports Customer Journey Analytics ou tout autre service Platform.
>
>Les modifications n’ont aucune incidence sur Adobe Analytics en tant qu’application autonome, y compris la collecte, le traitement et la création de rapports de données. Les outils tels que les flux de données et les règles de traitement ne sont pas affectés. Aucune mise à jour de l’implémentation d’Analytics n’est donc requise.

Une nouvelle implémentation de la collecte de données Adobe (connecteur source Analytics) pour le service Streaming Media est désormais disponible. Elle migre d’un ensemble de champs XDM à un autre.

## Nouveau chemin du champ XDM

Dans le cadre de cette migration, le chemin d’accès au champ XDM `mediaReporting` a été ajouté aux schémas XDM utilisés dans les flux de collecte de données Adobe (connecteur source Analytics). Tout schéma de collecte de données Adobe existant et nouvellement généré inclura automatiquement ce nouveau champ.

## Remplacement de l’ancien chemin du champ XDM

Tous les flux de collecte de données Adobe (connecteur source Analytics) qui transfèrent des données de médias en flux continu d’Adobe Analytics vers Adobe Experience Platform envoient actuellement des données à la fois sur le nouveau chemin de champ XDM `mediaReporting` et sur l’ancien chemin de champ XDM `media.mediaTimed`. Ces deux parcours seront disponibles pendant trois mois, jusqu’à la fin octobre 2025. Après octobre, les champs de `media.mediaTimed` seront entièrement abandonnés et les données ingérées après octobre n’incluront que des `mediaReporting`. Après l’obsolescence, les champs de `media.mediaTimed` ne seront plus visibles dans l’interface utilisateur du schéma Adobe Experience Platform et l’ingestion des données sur ces champs s’arrêtera. Par conséquent, ces champs ne seront plus disponibles pour une utilisation dans aucun service Adobe Experience Platform.

Les données ingérées avant cette date resteront disponibles pour la création de rapports.

## Autres différences avec le nouveau chemin du champ XDM

Avec la nouvelle implémentation du connecteur source Adobe pour les médias en flux continu, les appels de maintien en vie d’Adobe Analytics sont désormais ingérés dans Adobe Experience Platform.

Auparavant, ces appels n’étaient pas pris en compte dans les applications Platform telles que Customer Journey Analytics. Par conséquent, votre organisation peut observer les différences suivantes dans les rapports :

* **Nombre précis de sessions** : dans certains cas, cela peut signifier une déflation du nombre de sessions, car les appels de maintien en vie permettent de maintenir les sessions utilisateur actives même en l’absence d’interactions multimédia directes. Ces appels de maintien en vie sont générés toutes les 20 minutes après le dernier événement, par lecture de média, dans le but de maintenir la visite ouverte. Pour assurer un suivi de session optimal dans Customer Journey Analytics, il est recommandé de configurer l’expiration de la visite sur 30 minutes dans la vue de données.

* **Augmentation du nombre d’événements** : car les appels persistants sont désormais comptabilisés dans la mesure Événements Customer Journey Analytics. Si vous souhaitez exclure les appels de persistance du compte rendu des performances, vous pouvez créer un filtre qui exclut les événements dont le type d’événement est `media.keepalive`.

Cette modification assure un meilleur alignement entre les rapports Analytics et CJA.

## Migration de votre configuration existante

Pour garantir une transition fluide, tous les clients doivent migrer les configurations existantes des champs `media.mediaTimed` vers les champs `mediaReporting` avant la fin octobre 2025. Les zones affectées sont celles qui dépendent de l’utilisation de `media.mediaTimed` et elles doivent être migrées comme indiqué dans les sections suivantes.

### Customer Journey Analytics**

Les rapports CJA peuvent être migrés de deux manières :

>[!NOTE]
>
>Après avoir choisi l’une des options suivantes, vous devez remplacer manuellement chaque champ `media.mediaTimed` utilisé dans les rapports Customer Journey Analytics par son champ dérivé correspondant ou son chemin d’accès au champ XDM de création de rapports.

* **Pour conserver les données historiques** : les équipes d’Adobe ont développé un modèle Customer Journey Analytics prédéfini qui introduit un ensemble de champs dérivés qui combinent les anciens et les nouveaux champs XDM en un seul champ. Ce modèle peut être activé par connexion Customer Journey Analytics sur demande. Contactez l’équipe d’assistance Adobe pour obtenir de l’aide sur l’activation des nouveaux champs. Ces champs dérivés ne sont pas pris en compte dans la limite de champs dérivés de votre organisation.

  Pour afficher la liste des mappages, voir [Mappage des paramètres Media Analytics pour Adobe Experience Platform et Customer Journey Analytics](/help/use-cases/xdm-updates/parameters-mapping.md).

* **Si des données historiques ne sont pas requises** : il suffit d’utiliser le chemin du champ XDM de création de rapports au moment de la création de rapports. Pour plus d’informations, voir [Migrer Customer Journey Analytics pour utiliser les nouveaux champs Streaming Media](/help/use-cases/xdm-updates/migrate-cja-setup.md).

### Real-Time CDP

Toutes les audiences et tous les profils doivent être basés sur des `mediaReporting`. Pour plus d’informations, voir [Migration des profils vers les nouveaux champs Streaming Media](/help/use-cases/xdm-updates/migrate-profiles.md).

### Flux de données et collecte de données

Les configurations dynamiques et le mappage de données doivent utiliser `mediaReporting`. Pour plus d’informations, voir [Migrer la préparation des données pour les champs personnalisés vers les nouveaux champs Streaming Media](/help/use-cases/xdm-updates/migrate-dataprep.md).

### Autres services qui doivent être migrés

* Adobe Journey Optimizer : les configurations de campagne et de parcours doivent intégrer `mediaReporting`.

* Transfert d’événement : seuls les champs `mediaReporting` doivent être inclus dans les configurations.

* Query Services : les requêtes doivent référencer des champs de `mediaReporting`.

* Configurations des balises : toutes les configurations de balisage doivent faire référence aux champs `mediaReporting`.

* Connexions et destinations : les flux de données d&#39;import et d&#39;export doivent être structurés autour de champs `mediaReporting`.

N’oubliez pas que tout autre flux qui repose sur des champs `media.mediaTimed` est affecté et nécessite des mises à jour logiques.

## Étapes suivantes et assistance

Tous les clients qui utilisent la collecte de données Adobe pour les médias en flux continu doivent effectuer leur migration au cours de la période de transition désignée.

Pour toute question ou besoin d’assistance, n’hésitez pas à contacter l’équipe d’assistance d’Adobe.

