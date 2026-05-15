---
title: Présentation des événements multimédia en flux continu
description: Découvrez les types d’événements multimédia et l’ordre dans lequel ils doivent être envoyés.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 4%

---


# Événements de streaming multimédia

Le suivi des médias en flux continu fonctionne en envoyant une séquence d’appels d’événement, chacun représentant une transition d’état du lecteur, à un point d’entrée de collecte de données Adobe. Chaque événement appartient à une session active qui commence par un appel [sessionStart](session/session-start.md) et se termine par [sessionComplete](session/session-complete.md) ou [sessionEnd](session/session-end.md).

## Workflow d’événement

La liste suivante affiche l’ordre des événements requis pour une lecture VOD type avec une publicité preroll et un chapitre :

1. **[Début de session](session/session-start.md)** : toujours le premier événement ; crée la session et renvoie un ID de session
2. **[Début de la coupure publicitaire](ads/ad-break-start.md)** : requis avant tout événement publicitaire
3. **[Début de la publicité](ads/ad-start.md)** → **[Fin de la publicité](ads/ad-complete.md)** (ou **[Saut de la publicité](ads/ad-skip.md)**)
4. **[Coupure publicitaire terminée](ads/ad-break-complete.md)** : obligatoire après toutes les publicités de la coupure
5. **[Lecture](playback/play.md)** : signale que la lecture du contenu commence ou reprend
6. **[Début du chapitre](chapters/chapter-start.md)** : facultatif ; marque le début d’un chapitre
7. **[Ping](playback/ping.md)** : envoyé toutes les 10 secondes pendant le contenu principal, toutes les secondes pendant les publicités
8. **[Chapitre terminé](chapters/chapter-complete.md)** : facultatif ; marque la fin d’un chapitre
9. **[Démarrage de la pause](playback/pause-start.md)** → **[Lecture](playback/play.md)** (reprise) : pour toute pause
10. **[Début de la mémoire tampon](playback/buffer-start.md)** → **[Lecture](playback/play.md)** (reprise) : pour toute mise en mémoire tampon
11. **[Session terminée](session/session-complete.md)** : lorsque la visionneuse atteint la fin du contenu

Utilisez [Fin de session](session/session-end.md) au lieu de Fin de session si la visionneuse abandonne la session avant d’atteindre la fin du contenu.

## Cycle de vie d’une session

Une session expire automatiquement si l’une des conditions suivantes est remplie :

* Aucun événement n’est reçu pendant **10 minutes**
* Aucun mouvement de tête de lecture pendant **30 minutes**

## Référence d’événement

| Événement | Catégorie | Mesure associée |
| --- | --- | --- |
| [Début de la session](session/session-start.md) | Session | [Démarrage des médias](/help/reporting/metrics/media-starts.md) |
| [Fin de la session](session/session-complete.md) | Session | [Fin du contenu](/help/reporting/metrics/content-completes.md) |
| [Fin de session](session/session-end.md) | Session | — |
| [Lecture](playback/play.md) | Lecture | [Le contenu démarre](/help/reporting/metrics/content-starts.md) |
| [Démarrer la pause](playback/pause-start.md) | Lecture | [Événements Pause](/help/reporting/metrics/pause-events.md) |
| [ Début de la mémoire tampon ](playback/buffer-start.md) | Lecture | [Événements de mémoire tampon](/help/reporting/metrics/buffer-events.md) |
| [Changement de débit](playback/bitrate-change.md) | Lecture | [Modifications de débit](/help/reporting/metrics/bitrate-changes.md) |
| [ Ping ](playback/ping.md) | Lecture | — |
| [Début de la coupure publicitaire](ads/ad-break-start.md) | Publicités | — |
| [Début de la publicité](ads/ad-start.md) | Publicités | [La publicité commence](/help/reporting/metrics/ad-starts.md) |
| [Publicité terminée](ads/ad-complete.md) | Publicités | [Fin de la publicité](/help/reporting/metrics/ad-completes.md) |
| [Saut d’annonce publicitaire](ads/ad-skip.md) | Publicités | — |
| [Coupure publicitaire terminée](ads/ad-break-complete.md) | Publicités | — |
| [ Début du chapitre ](chapters/chapter-start.md) | Chapitres | [Démarrage du chapitre](/help/reporting/metrics/chapter-starts.md) |
| [Chapitre terminé](chapters/chapter-complete.md) | Chapitres | [Fin du chapitre](/help/reporting/metrics/chapter-completes.md) |
| [Saut de chapitre](chapters/chapter-skip.md) | Chapitres | — |
| [Début état](player-state/state-start.md) | État du lecteur | Varie selon l’état |
| [Fin de l’état](player-state/state-end.md) | État du lecteur | Varie selon l’état |
| [Erreur](error.md) | Qualité | [ Flux impactés par l’erreur ](/help/reporting/metrics/error-impacted-streams.md) |

>[!MORELIKETHIS]
>
>* [Schémas de validation JSON](/help/implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md) : vérification de la structure de la payload de requête pour chaque type d’événement
>* [Point d’entrée de requête events](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) : référence de point d’entrée de l’API Media Collection
>* [Point d’entrée de requête de sessions](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) : créez une session avant d’envoyer des événements
>* [Suivi de l’état du lecteur](/help/use-cases/player-state-tracking/implementation-and-reporting.md) : détails d’implémentation du début et de la fin de l’état
