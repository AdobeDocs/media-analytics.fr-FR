---
title: Mesures calculées du streaming multimédia
description: Apprenez en plus sur les mesures calculées et les formules de mesure dʼAdobe Streaming Media.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 100%

---

# Mesures calculées {#calculated-metrics}

Les mesures calculées pour le streaming multimédia sont des mesures personnalisées qui vous permettent dʼobtenir des données ciblées sur les streaming multimédia, telles que le temps passé sur la publicité ou la moyenne des publicités par flux multimédia.

Pour plus dʼinformations sur les mesures calculées Adobe Analytics, voir [Mesures calculées (dérivées) et mesures calculées avancées](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=fr) dans le guide des composants Adobe Analytics.

>[!NOTE]
>
>Ces mesures calculées ont été introduites le 13/09/18.

| Mesure | Description | Formule |
|---|---|---|
| Nombre moyen de publicités par flux de média | Démarrages de publicité par démarrages de média | `Ad Starts / Media Starts` |
| Nombre moyen de chapitres par flux de média | Démarrages de chapitre par démarrages de média | `Chapter Start / Media Starts` |
| Temps moyen passé sur le média | Temps total passé par démarrages de média (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Temps moyen Temps passé sur le contenu | Temps passé sur le contenu par démarrage de contenu (HH:MM:SS) | `Content Time Spent / Content Start` |
| Temps moyen passé sur la publicité | Temps passé sur la publicité par démarrage de publicité (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Temps moyen Passé sur le chapitre | Temps passé sur le chapitre par démarrage de chapitre (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Taux d’achèvement du média | Taux de contenu terminé par rapport au média initié (%) | `Content Completes/ Media Starts` |
| Taux de contenus terminés | Taux de contenus terminés par rapport aux démarrages de contenu (%) | `Content Completes / Content Starts` |
| Taux d’achèvement de la publicité | Taux de publicités terminées par rapport aux démarrages de publicité (%) | `Ad Completes / Ad Starts` |
| Taux de chapitres terminés | Taux de chapitres terminés par rapport aux démarrages de chapitre (%) | `Chapter Completes / Chapter Starts` |
| Taux d’abandon avant le démarrage | Taux de pertes avant le début par rapport aux démarrages de contenu multimédia (%) | `Drops before Starts / Media Starts` |
| Taux de la durée de mise en pause du contenu | Taux de la durée totale de mise en pause par rapport au temps passé sur le contenu (%) | `Total Pause Duration / Content Time Spent` |
| Taux de la durée de la mémoire tampon du contenu | Taux de la durée totale de la mémoire tampon par rapport au temps passé sur le contenu (%) | `Total Buffer Duration / Content Time Spent` |
| Taux du temps jusqu’au démarrage du contenu | Taux du temps jusqu’au démarrage par rapport au temps passé sur le contenu (%) | `Time to Start / Content Time Spent` |
| Taux du temps passé sur la publicité | Taux du temps passé sur la publicité par rapport au temps passé sur le contenu (%) | `Ad Time Spent / Content Time Spent` |
