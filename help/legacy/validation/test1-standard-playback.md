---
title: Test 1 Lecture standard
description: Découvrez le test de lecture standard utilisé dans la validation.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
exl-id: 3781f0f7-be75-43e5-a40b-a34956dce36e
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 100%

---

# Test 1 - Lecture standard{#test-standard-playback}

Ce cas de test valide la lecture et le séquencement généraux.

Les mises en œuvre de Media Analytics incluent deux types d’appels de suivi :
* Appels effectués directement sur votre serveur Adobe Analytics (AppMeasurement) - Ces appels surviennent sur les événements « Démarrage du média » et « Démarrage de la publicité ».
* Appels effectués sur le serveur Media Analytics (pulsations) - Ceux-ci comprennent les appels en bande et hors-bande :
   * En bande - Le SDK envoie des appels de lecture chronométrés ou « pings » à des intervalles de 10 secondes pendant la lecture du contenu et à des intervalles d’une seconde pendant les publicités.
   * Hors-bande - Ces appels peuvent se produire à tout moment, notamment en cas de pauses, de mises en mémoire tampon, d’erreurs, de contenu terminé, de publicité terminée, etc.

>[!NOTE]
>Le suivi multimédia se comporte de la même manière sur toutes les plateformes.

## Procédure de test

Exécutez et enregistrez les actions suivantes (dans l’ordre) :

1. **Charger la page ou l’application**

   **Serveurs de suivi** (pour tous les sites Web et les applications mobiles) :

   * **Serveur Adobe Analytics (AppMeasurement) -** Un serveur de suivi RDC ou CNAME se résolvant sur un serveur de suivi RDC est requis pour le service d’identifiant visiteur Experience Cloud. Le serveur de suivi Adobe Analytics doit se terminer par « `.sc.omtrdc.net` » ou être un serveur CNAME.

   * **Serveur Media Analytics (Heartbeats) -** Ce serveur a toujours le format « `[namespace].hb.omtrdc.net` », où `[namespace]` spécifie le nom de votre société. Ce nom est fourni par Adobe.

   Vous devez valider certaines variables clés universelles pour tous les appels de suivi :

   **Identifiant visiteur Adobe (`mid`) :** La variable `mid` est utilisée pour capturer la valeur définie dans le cookie AMCV. La variable `mid` est la principale valeur d’identification pour les sites Web et les applications mobiles, et elle indique également que le service d’identification des visiteurs Experience Cloud est configuré correctement. Elle se trouve dans les appels Adobe Analytics (AppMeasurement) et Media Analytics (pulsations).

   * **Appel de démarrage d’Adobe Analytics**

     | Paramètre | Valeur (exemple) |
     |---|---|
     | `pev2` | ms_s |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de page de site Web**

     | Paramètre | Valeur (exemple) |
     |---|---|
     | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de cycle de vie**

     | Paramètre | Valeur (exemple) |
     |---|---|
     | `pev2` | ADBINTERNAL:Lifecycle |
     | `mid` | 30250035503789876473484580554595324209 |

   * **Appel de démarrage de Media Analytics**

     | Paramètre | Valeur (exemple) |
     |---|---|
     | `s:event:type` | start |

     >[!NOTE]
     >
     >Sur les appels de démarrage Media Analytics (`s:event:type=start`), les valeurs `mid` peuvent ne pas être présentes. Ceci est normal. Il se peut qu’elles n’apparaissent pas avant les appels de lecture de Media Analytics (`s:event:type=play`).

   * **Appel de lecture de Media Analytics**

     | Paramètre | Valeur (exemple) |
     |---|---|
     | `s:event:type` | play |
     | `s:user:mid` | 30250035503789876473484580554595324209 |

1. **Démarrage du lecteur multimédia**

   Lorsque le lecteur multimédia démarre, le SDK Media envoie les appels clés aux deux serveurs dans l’ordre suivant :

   1. Serveur Adobe Analytics - Appel de démarrage
   1. Serveur Media Analytics - Appel de démarrage
   1. Serveur Media Analytics - « Appel de démarrage d’Adobe Analytics demandé »

   Les deux premiers appels ci-dessus contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d’appel et les métadonnées, voir [Détails des appels de test.](/help/legacy/validation/test-call-details.md#start-the-media-player)

   Le troisième appel ci-dessus indique au serveur Media Analytics que le SDK Media a demandé que l’appel de démarrage d’Adobe Analytics (`pev2=ms_s`) soit envoyé au serveur Adobe Analytics.

1. **Afficher la coupure publicitaire si possible**

   * **Démarrage de publicité**

   Au démarrage de la publicité, les appels clés ci-dessous sont envoyés dans l’ordre suivant :

   1. Serveur Adobe Analytics - Appel de démarrage de la publicité
   1. Serveur Media Analytics - Appel de démarrage de la publicité
   1. Serveur Media Analytics - « Appel de démarrage de la publicité d’Adobe Analytics demandé »

   Les deux premiers appels contiennent des métadonnées et des variables supplémentaires. Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/legacy/validation/test-call-details.md#view-ad-playback)

   Le troisième appel indique au serveur Media Analytics que le SDK Media a demandé que l’appel de démarrage de la publicité d’Adobe Analytics (`pev2=msa_s`) soit envoyé au serveur Adobe Analytics.

   * **Lecture de la publicité**

     Pendant la lecture de la publicité, le SDK Media Analytics envoie des événements de lecture de type « publicité » au serveur Media Analytics toutes les secondes.

   * **Fin de la publicité**

     Au point 100 % sur une publicité, un appel de fin de Media Analytics doit être envoyé.

1. **Suspendre la lecture de la publicité pendant 30 secondes si possible.** **Pause de la publicité**

   Pendant la pause de la publicité, les appels de pulsation ou « pings » de Media Analytics sont envoyés par le SDK au serveur Media Analytics toutes les secondes.

   >[!NOTE]
   >
   >La valeur du curseur de lecture doit rester constante pendant la pause.

   Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/legacy/validation/test-call-details.md#ma-ad-pause-call)

1. **Lire le contenu principal pendant 10 secondes sans interruption.** **Lecture du contenu**

   Lors de la lecture du contenu principal, le SDK Media envoie des pulsations (appels de lecture) au serveur Media Analytics toutes les 10 secondes.

   Remarques :

   * La position du curseur de lecteur doit augmenter de 10 à chaque appel de lecture.
   * La valeur `l:event:duration` représente le nombre de millisecondes qui se sont écoulées depuis le dernier appel de suivi, et doit être plus ou moins constante pour chaque appel de 10 secondes.

     Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/legacy/validation/test-call-details.md#play-main-content)

1. **Suspendre la lecture pendant au moins 30 secondes.** Lors de la mise en pause du lecteur multimédia, les appels d’événement de pause sont envoyés par le SDK au serveur Media Analytics toutes les 10 secondes. Après la pause, les événements de lecture reprennent normalement.

   Pour les paramètres d’appel et les métadonnées, voir [Test des détails d’appel.](/help/legacy/validation/test-call-details.md#pause-main-content)

1. **Rechercher/faire défiler le média.** Lors du défilement du curseur de lecture multimédia, aucun appel de suivi spécial n’est envoyé. Toutefois, lorsque la lecture multimédia reprend après le défilement, la valeur du curseur de lecture doit refléter la nouvelle position dans le contenu principal.

1. **Lecture du média (VOD uniquement).** Lorsque le média est relu, un nouvel ensemble d’appels de démarrage du contenu multimédia doit être envoyé (comme s’il s’agissait d’un nouveau départ).

1. **Afficher le média suivant dans la liste de lecture** Au démarrage du média suivant dans une liste de lecture, un nouvel ensemble d’appels de démarrage du contenu multimédia doit être envoyé.

1. **Changement de média ou de flux.** Lors du changement de diffusion en direct, un appel de fin Media Analytics pour la première diffusion ne doit pas être envoyé. Les appels de démarrage et de lecture du contenu multimédia doivent commencer par le nouveau nom d’affichage et de diffusion et avec les valeurs du curseur de lecture et de durée correctes pour le nouvel affichage.
