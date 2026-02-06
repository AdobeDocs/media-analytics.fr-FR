---
title: Migrer les profils vers les nouveaux champs Streaming Media
description: Découvrez comment migrer les profils vers les nouveaux champs Streaming Media
feature: Streaming Media
role: User, Admin, Developer
exl-id: 0f75e594-5216-4ac1-91bd-fa89ab4b2110
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '505'
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

Pour mapper les anciens champs aux nouveaux champs, reportez-vous au paramètre [Content ID](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/audio-video-parameters#content-id) sur la page [Paramètres audio et vidéo](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/audio-video-parameters). L’ancien chemin du champ se trouve sous la propriété « Chemin du champ XDM » tandis que le nouveau chemin du champ se trouve sous la propriété « Chemin du champ XDM de création de rapports ».

## Exemple

Pour suivre plus facilement les instructions de migration, considérez l’exemple de flux de données suivant qui contient une seule règle de filtrage de profil. Dans ce cas, comme il n’existe qu’une seule règle, vous ne devez appliquer les directives de migration qu’une seule fois.

1. Dans Adobe Experience Platform, dans la section [!UICONTROL **Sources**], accédez à l’onglet [!UICONTROL **Flux de données**].

&#x200B;1. Recherchez le flux de données responsable de l’importation des données de médias en flux continu d’Adobe Analytics vers Adobe Experience Platform via Adobe Analytics.

1. Sélectionnez **[!UICONTROL Mettre à jour le flux de données]** pour accéder à l’interface utilisateur de modification, comme illustré dans l’image ci-dessous.

   ![profil de flux de données AEP](assets/aep-dataflow-profile.jpeg)

1. Sélectionnez **[!UICONTROL Suivant]** pour accéder à l’onglet Filtrage .

   ![Onglet Filtre de flux de données AEP](assets/aep-dataflow-filtering-profile.jpeg)

1. Dans l’onglet **[!UICONTROL Filtrage]**, identifiez les règles de filtrage qui reposent sur des champs `media.mediaTimed`.

   ![règles de filtrage des flux de données AEP](assets/dataflow-filtering-rules-profile.jpeg)


   Pour chaque filtre qui utilise l’objet media.mediaTimed, recherchez son correspondant dans l’objet `mediaReporting` à l’aide de la page [Paramètres audio et vidéo](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/audio-video-parameters) pour mapper les anciens champs aux nouveaux champs. L’ancien chemin du champ se trouve sous la propriété « Chemin du champ XDM » tandis que le nouveau chemin du champ se trouve sous la propriété « Chemin du champ XDM de création de rapports ». Par exemple, pour [Media Starts](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/audio-video-parameters#media-starts), le correspondant pour `media.mediaTimed.impressions.value` est `mediaReporting.sessionDetails.isViewed`.

   ![Nouveaux et anciens champs XDM](assets/xdm-fields-new-and-old.jpeg)

1. Faites glisser le champ de `mediaReporting` approprié vers la règle de filtrage et utilisez l’opérateur OR entre les deux règles. Ajoutez la même règle que la règle existante lors de l’utilisation du nouveau champ.

   ![Ajouter des règles de filtrage](assets/add-filter-rules.jpeg)

1. Sélectionnez **[!UICONTROL Suivant]** pour enregistrer vos modifications.
