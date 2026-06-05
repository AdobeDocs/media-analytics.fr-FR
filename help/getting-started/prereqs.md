---
title: En savoir plus sur les conditions préalables requises pour les services de streaming multimédia Adobe
description: Prise en main des services de streaming multimédia. Découvrez ce dont vous avez besoin pour la mise en œuvre.
uuid: 4c0b37f3-8615-4cc0-b9c9-eeb029067064
exl-id: 85ab1dbd-f4a7-4f11-afc9-8d5000e2de70
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/e9iYwDwT-zSSZ3hV20U1w7p-MtKaK4Q8-vGMCrnenpc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 10%

---

# Conditions préalables {#prerequisites}

Avant de commencer la mise en œuvre des services de streaming multimédia d’Adobe, effectuez les tâches suivantes :

1. **Confirmer votre modèle de tarification**<br>
Le modèle de tarification actuel pour le module complémentaire de collecte de médias en flux continu Customer Journey Analytics et le module complémentaire Adobe Analytics pour les médias en flux continu repose sur les flux vidéo. Si nécessaire, contactez votre représentant commercial ou l’équipe chargée du compte Adobe, car le module complémentaire est vendu séparément pour Adobe Analytics et Adobe Experience Platform.

1. **Activer les rapports Adobe Analytics** *(implémentations Analytics uniquement)*<br>
Pour activer les rapports dans Analytics et afficher le contenu et les données de publicité que vous collectez, vous devez activer les rapports. Voir [Configurer des rapports pour les implémentations Analytics uniquement](/help/reporting/setup/analytics-reporting.md).

1. **Configurer l’identité**<br>

   Les exigences de configuration des identités varient selon votre méthode d’implémentation :

   * **Implémentations Edge** : l’identité est gérée via la configuration de l’espace de noms d’identité Adobe Experience Platform. Aucune configuration distincte du service d’identités n’est requise. Voir [Présentation de l’implémentation d’](/help/implementation/edge/overview.md) pour plus d’informations.

   * **Implémentations Analytics uniquement** : le service Adobe Experience Platform Identity doit être activé pour identifier les visiteurs de manière cohérente au sein des solutions d’entreprise CX. Identity Service attribue un ID persistant unique à chaque visiteur du site et permet de partager cet ID avec toutes les solutions d’entreprise CX auxquelles vous êtes abonné.

     Pour plus d’informations, consultez la documentation du service d’identités Adobe Experience Platform [&#128279;](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).

1. **Afficher les conditions préalables supplémentaires pour votre méthode d’implémentation**

   Selon la manière dont vous prévoyez d’implémenter les services de médias en flux continu, consultez les conditions préalables requises pour l’une des méthodes d’implémentation suivantes :

   * [Présentation de l’implémentation pour Analytics uniquement](/help/implementation/analytics-only/overview.md)

   * [Présentation de l’implémentation d’Edge](/help/implementation/edge/overview.md)

   Utilisez la [vue d’ensemble de l’implémentation](/help/implementation/overview.md) pour déterminer la méthode d’implémentation qui vous convient.
