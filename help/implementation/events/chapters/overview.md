---
title: Suivi des chapitres et des segments
description: Comment mettre en œuvre le suivi des chapitres et des segments avec le SDK Media.
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 191
ht-degree: 39%

---


# Suivi des chapitres et des segments

Le suivi des chapitres et des segments est disponible pour les chapitres ou les segments médias personnalisés. Certaines utilisations courantes du suivi des chapitres consistent à définir des segments personnalisés basés sur le contenu média, tels que les manches au baseball, ou à définir des segments de contenu entre les coupures publicitaires. Le suivi des chapitres n’est **pas** requis pour les mises en œuvre de suivi multimédia principal.

Le suivi des chapitres comprend les démarrages de chapitre, les fins de chapitre, et les chapitres ignorés. Utilisez l’API du lecteur multimédia avec une logique de segmentation personnalisée pour identifier les événements de chapitre et renseigner les variables de chapitre.

## Événements du lecteur

| Événement du lecteur | Action |
| --- | --- |
| Début du chapitre | Créer un objet de chapitre ; appeler ChapterStart |
| Chapitre terminé | Chapitre d’appel terminé |
| Saut de chapitre | Appeler ChapterSkip |

## Procédure de mise en œuvre

1. Identifiez le moment où l’événement de début de chapitre se produit et créez l’objet de chapitre. Voir [Nom du chapitre](/help/implementation/variables/chapters/chapter-name.md), [Position du chapitre](/help/implementation/variables/chapters/chapter-position.md), [Longueur du chapitre](/help/implementation/variables/chapters/chapter-length.md) et [Décalage du chapitre](/help/implementation/variables/chapters/chapter-offset.md) pour la définition des champs.
1. Vous pouvez éventuellement créer des variables de données contextuelles pour les métadonnées de chapitre personnalisées.
1. Appelez [Chapitre start](/help/implementation/events/chapters/chapter-start.md) pour commencer à suivre le chapitre.
1. Lorsque la lecture atteint la limite de fin du chapitre, appelez [Chapitre terminé](/help/implementation/events/chapters/chapter-complete.md).
1. Si l’utilisateur ou l’utilisatrice ignore le chapitre avant de terminer, appelez [Ignorer le chapitre](/help/implementation/events/chapters/chapter-skip.md).
1. Pour des chapitres supplémentaires, répétez les étapes 1 à 5.
