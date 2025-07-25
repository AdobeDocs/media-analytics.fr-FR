---
title: 'Test 2 : interruption des médias'
description: Découvrez le test dʼinterruption des médias utilisé lors de la validation.
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '249'
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
