---
title: Configuration d’un SDK mobile à l’aide de balises pour les services de streaming multimédia
description: Découvrez comment mettre en œuvre les services de streaming multimédia d’Adobe pour les applications mobiles.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 70%

---

# Installer les SDK mobiles {#install-mobile-sdks}

Pour mettre en œuvre les services de streaming multimédia d’Adobe pour les applications mobiles sur Android ou iOS, installez et configurez les éléments suivants :

* **SDK Mobile Adobe Experience Platform**

  Pour collecter des données, utilisez l’une des méthodes suivantes :
   * Balises dans Adobe Experience Platform Les balises dans Adobe Experience Platform représentent une solution de gestion des balises qui vous permet de déployer le code Analytics parallèlement à d’autres exigences de balisage.
   * Adobe Experience Platform Edge

* **SDK Media pour Android** ou **SDK Media pour iOS**

* **Extension Adobe Media Analytics for Audio and Video**

Pour télécharger les SDK et des ressources de documentation supplémentaires, consultez [Obtenir des SDK Media, des extensions à l’aide de balises et des SDK OTT](/help/getting-started/download-sdks.md).

* **Obtenir des paramètres de configuration valides**

  Vous pouvez obtenir ces paramètres auprès d’un représentant Adobe une fois votre compte d’analyse configuré.

* **Incluez les API suivantes dans votre lecteur multimédia**

   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.

   * *Une API qui fournit des informations sur le lecteur* – Inclut des informations sur la lecture en cours telles que le nom du média, la position de la tête de lecture, les annonces publicitaires ou le chapitre.
