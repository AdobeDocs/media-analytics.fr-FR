---
title: Configuration d’un SDK mobile à l’aide de balises pour les médias en flux continu
description: Découvrez comment mettre en oeuvre Adobe Streaming Media pour les applications mobiles.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 31%

---

# Installation des SDK mobiles {#install-mobile-sdks}

Pour mettre en oeuvre des médias en flux continu pour les applications mobiles sur Android ou iOS, installez et configurez les éléments suivants :

* **SDK Mobile Adobe Experience Platform**

   Pour collecter des données, utilisez Balises dans Adobe Experience Platform. Les balises dans Adobe Experience Platform représentent une solution de gestion des balises qui vous permet de déployer le code Analytics parallèlement à d’autres exigences de balisage.

* **SDK Media pour Android** ou **SDK Media pour iOS**

* **Extension Adobe Media Analytics for Audio and Video**

Pour télécharger les SDK et des ressources de documentation supplémentaires, voir [Obtention des SDK Media, des extensions à l’aide de balises et des SDK OTT](/help/getting-started/download-sdks.md)

* **Obtention de paramètres de configuration valides**

   Vous pouvez obtenir ces paramètres auprès d’un représentant d’Adobe après avoir configuré votre compte Analytics.

* **Incluez les API suivantes dans votre lecteur multimédia**

   * *Une API pour vous abonner aux événements du lecteur* - Le SDK Media exige d’appeler un ensemble d’API simples lorsque des événements se produisent dans votre lecteur.

   * *Une API qui fournit des informations sur le lecteur* - Cela inclut des informations sur la lecture en cours telles que le nom du média, la position de la tête de lecture, les publicités ou le chapitre.
