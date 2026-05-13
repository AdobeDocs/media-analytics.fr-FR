---
title: Migrer les profils vers les nouveaux champs Streaming Media
description: Découvrez comment migrer les profils vers les nouveaux champs Streaming Media
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
TQID: https://experienceleague.adobe.com/c1WHnEeZnI3PP6aO40pDHpJCi2Z0ERiNY8lCj4wyMiU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 533
ht-degree: 0%

---

# Migrer les profils vers les nouveaux champs de streaming multimédia

Ce document décrit le processus de migration du service de filtrage de profil qui existe en plus des flux de collecte de données Adobe activés pour Adobe Analytics pour les données de médias en flux continu. La migration convertit le service de filtrage de profil de l’utilisation du type de données des services de streaming multimédia d’Adobe appelé « Media » vers l’utilisation du nouveau type de données correspondant appelé « [Détails de création de rapports multimédia](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) ».

## Migration de profils

Pour migrer le filtrage de profil de l’ancien type de données appelé « Media » vers le nouveau type de données appelé « [Détails des rapports multimédia](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) », vous devez modifier les règles de filtrage de profil existantes :

1. Dans Adobe Experience Platform, dans la section [!UICONTROL **Sources**], accédez à l’onglet [!UICONTROL **Flux de données**].

1. Recherchez le flux de données responsable de l’importation des données de médias en flux continu d’Adobe Analytics vers Adobe Experience Platform via la collecte de données Adobe.

1. Sélectionnez [!UICONTROL **Mettre à jour le flux de données**] pour modifier la configuration du filtrage de profil en remplaçant chaque règle personnalisée qui contient un champ obsolète par le nouveau champ correspondant du nouvel objet XDM.

1. Recherchez les filtres contenant les champs de l’objet « Media » obsolète.

1. Ajoutez ces filtres en ajoutant des champs à partir du nouvel objet « Détails des rapports multimédia ».

1. Utilisez un opérateur OR entre les deux champs ;

1. Vérifiez que les profils fonctionnent toujours comme prévu.

Consultez le paramètre [ID de contenu](/help/reporting/dimensions/content.md) et le reste des variables de médias en flux continu documentés sous [Services de médias en flux continu](/help/media-overview.md) pour mapper les anciens champs aux nouveaux champs. L’ancien chemin du champ se trouve sous la propriété « Chemin du champ XDM » tandis que le nouveau chemin du champ se trouve sous la propriété « Chemin du champ XDM de création de rapports ».

## Exemple

Pour suivre plus facilement les instructions de migration, considérez l’exemple de flux de données suivant qui contient une seule règle de filtrage de profil. Dans ce cas, comme il n’existe qu’une seule règle, vous ne devez appliquer les directives de migration qu’une seule fois.

1. Dans Adobe Experience Platform, dans la section [!UICONTROL **Sources**], accédez à l’onglet [!UICONTROL **Flux de données**].

&#x200B;1. Recherchez le flux de données responsable de l’importation des données de médias en flux continu d’Adobe Analytics vers Adobe Experience Platform via Adobe Analytics.

1. Sélectionnez **[!UICONTROL Mettre à jour le flux de données]** pour accéder à l’interface utilisateur de modification, comme illustré dans l’image ci-dessous.

   ![profil de flux de données &#x200B;](assets/aep-dataflow-profile.jpeg)

1. Sélectionnez **[!UICONTROL Suivant]** pour accéder à l’onglet Filtrage .

   ![Onglet Filtre de flux de données &#x200B;](assets/aep-dataflow-filtering-profile.jpeg)

1. Dans l’onglet **[!UICONTROL Filtrage]**, identifiez les règles de filtrage qui reposent sur des champs `media.mediaTimed`.

   ![règles de filtrage des flux de données &#x200B;](assets/dataflow-filtering-rules-profile.jpeg)


   Pour chaque filtre qui utilise l’objet media.mediaTimed, recherchez son correspondant dans l’objet `mediaReporting` à l’aide des variables de médias en flux continu documentées sous [Services de médias en flux continu](/help/media-overview.md) pour mapper les anciens champs aux nouveaux champs. L’ancien chemin du champ se trouve sous la propriété « Chemin du champ XDM » tandis que le nouveau chemin du champ se trouve sous la propriété « Chemin du champ XDM de création de rapports ». Par exemple, pour [Media Starts](/help/reporting/metrics/media-starts.md), le correspondant pour `media.mediaTimed.impressions.value` est `mediaReporting.sessionDetails.isViewed`.

   ![Nouveaux et anciens champs XDM](assets/xdm-fields-new-and-old.jpeg)

1. Faites glisser le champ de `mediaReporting` approprié vers la règle de filtrage et utilisez l’opérateur OR entre les deux règles. Ajoutez la même règle que la règle existante lors de l’utilisation du nouveau champ.

   ![Ajouter des règles de filtrage](assets/add-filter-rules.jpeg)

1. Sélectionnez **[!UICONTROL Suivant]** pour enregistrer vos modifications.
