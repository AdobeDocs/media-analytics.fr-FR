---
title: 'Test 2 : interruption des médias'
description: Découvrez le test dʼinterruption des médias utilisé lors de la validation.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# Test 2 - Interruption des médias{#test-media-interruption}

Ce cas de test valide le comportement d’interruption mobile.

## Procédure de test

Vous devez effectuer et enregistrer ces tâches dans l’ordre suivant :

1. **Démarrage du lecteur multimédia**

   Au démarrage du lecteur multimédia, les appels ci-dessous sont envoyés dans l’ordre suivant :

   1. Démarrage d’Adobe Analytics (AppMeasurement)
   1. Démarrage de Media Analytics (pulsations)
   1. Appel de démarrage d’Adobe Analytics de Media Analytics (pulsations) demandé

   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d’appel et les métadonnées, voir [Détails des appels de test.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   Le troisième appel ci-dessus indique au serveur Media Analytics que le SDK Media a demandé que l’appel de démarrage d’Adobe Analytics (`pev2=ms_s`) soit envoyé au serveur Adobe Analytics.

1. **Lire contenu principal pendant au moins 5 minutes sans interruption**

   **Lecture du contenu**

   Pendant la lecture du contenu, le SDK Media envoie des appels de lecture (pulsations) au serveur Media Analytics toutes les dix secondes.

   Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/legacy/validation/test-call-details.md#play-main-content)

   Reportez-vous également aux instructions de [suivi des annonces publicitaires](/help/use-cases/track-ads/track-ads-overview.md) de votre plateforme pour en savoir plus sur ces appels publicitaires.

1. **Déplacer l’application ou le navigateur en arrière-plan**

   Lorsque l’application s’exécute en arrière-plan, seuls les appels `main:pause` doivent être envoyés au serveur Media Analytics, en commençant par VHL version 1.6.6 et ultérieures.

1. **Ramener l’application ou le navigateur au premier plan**

   Au retour depuis l’arrière-plan, la lecture du contenu doit reprendre.

1. **Lire le média de contenu principal pendant au moins 5 minutes sans interruption**

   Pour plus d’informations sur les paramètres d’appel et les métadonnées, voir [Détails des appels de test.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Fermeture du lecteur multimédia**

   Aucun autre appel de suivi ne doit être déclenché après la fermeture du lecteur multimédia.
