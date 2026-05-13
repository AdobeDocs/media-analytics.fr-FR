---
title: Configuration d’un SDK mobile à l’aide de balises pour les services de streaming multimédia
description: Découvrez comment mettre en œuvre les services de streaming multimédia d’Adobe pour les applications mobiles.
feature: Streaming Media
role: User, Admin, Developer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
TQID: https://experienceleague.adobe.com/IfnXB76Qycsic-ezOzZX4X-5RakbTQ0tlt7va6q2fZ8
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 199
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
