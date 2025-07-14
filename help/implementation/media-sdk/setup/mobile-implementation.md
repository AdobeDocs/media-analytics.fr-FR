---
title: Configuration d’un SDK mobile à l’aide de balises pour Streaming Media
description: Découvrez comment implémenter Adobe Streaming Media pour les applications mobiles.
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 82%

---

# Installer les SDK mobiles {#install-mobile-sdks}

Pour implémenter Streaming Media Collection pour les applications mobiles sur Android ou iOS, installez et configurez les éléments suivants :

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
