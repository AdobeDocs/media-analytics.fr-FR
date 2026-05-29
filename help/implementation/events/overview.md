---
title: Présentation des événements multimédia en flux continu
description: Découvrez les types d’événements multimédia et l’ordre dans lequel ils doivent être envoyés.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---


# Événements de streaming multimédia

Le suivi des médias en flux continu fonctionne en envoyant une séquence d’appels d’événement à un point d’entrée de collecte de données Adobe, chacun représentant une transition dans l’état du lecteur. Chaque événement appartient à une session active ouverte par un appel [Début de session](session/session-start.md). Les sessions se ferment automatiquement à l’expiration ou peuvent être fermées immédiatement à l’aide d’un appel [Fin de session](session/session-end.md).

Les événements sont regroupés en six catégories (session, lecture, annonces, chapitres, état du lecteur et qualité), couvrant chacune un aspect distinct de l’expérience multimédia.

## Événements de session

Les événements de session s’appliquent à tout type de suivi multimédia, notamment : la vidéo à la demande, les diffusions en direct, les podcasts et les livres audio. Ils définissent les limites de la session de suivi elle-même. L’événement de session le plus important est [Début de session](session/session-start.md), car presque tous les autres types d’événement dépendent de l’ID de session qu’ils génèrent. Envoyez-le comme tout premier événement lorsqu’un utilisateur lance une session, par exemple lorsqu’il appuie sur play ou lorsque le lecteur commence la lecture automatique.

Une fois qu’une session est ouverte, utilisez [Fin de session](session/session-complete.md) ou [Fin de session](session/session-end.md) pour indiquer comment l’expérience de visionnage s’est terminée. La session d’envoi se termine lorsque le spectateur atteint la fin naturelle du contenu : la vidéo se termine, l’épisode de podcast se termine ou le dernier chapitre d’un livre audio se termine. La session terminée ne ferme pas la session ; elle reste ouverte jusqu’à son expiration naturelle, de sorte que tous les événements de fin, tels qu’un ping final, sont toujours capturés.

Si la visionneuse quitte avant d’avoir atteint la fin, envoyez [Fin de session](session/session-end.md) pour fermer la session immédiatement. Envoyez uniquement la fin de session lorsqu’aucun événement supplémentaire ne se produit ; par exemple, lorsque le lecteur est détruit ou que la page est déchargée. La fin de session est un événement hard close : une fois envoyée, la session est terminée et aucun autre événement ne peut être suivi en dessous. Dans la plupart des cas, il est plus sûr de laisser la session expirer naturellement. Par exemple, la visionneuse se met indéfiniment en pause, l’application passe en arrière-plan ou le contenu ne se charge pas.

Une session expire automatiquement si aucun événement n’est reçu pendant 10 minutes ou si aucun mouvement du curseur de lecture n’est détecté pendant 30 minutes. Si l’une des conditions est remplie et que la visionneuse revient au contenu, vous devez appeler à nouveau le Démarrage de session pour ouvrir une nouvelle session avant d’envoyer d’autres événements.

## Événements de lecture

Les événements de lecture effectuent le suivi des transitions d’état dans le lecteur multimédia tout au long d’une session. Ils constituent le cœur du flux d’événements et s’appliquent à tout type de contenu.

L’événement de lecture principal est [&#x200B; Lecture &#x200B;](playback/play.md). Après avoir appelé le début de la session, la lecture signale que la lecture du contenu a commencé, qu’il s’agisse du début initial, d’un déclencheur de lecture automatique ou de tout retour à l’état de lecture. [Démarrer la pause](playback/pause-start.md) indique que l’utilisateur a suspendu la lecture. Il n’existe aucun événement de reprise dédié ; lorsque la visionneuse reprend, envoyez à nouveau la lecture. La lecture fonctionne de la même manière après un blocage de la mise en mémoire tampon : envoyez [Début de la mise en mémoire tampon](playback/buffer-start.md) lorsque le lecteur se bloque en attente de données, puis suivez avec Lecture lorsque la mise en mémoire tampon est résolue.

Envoyez [Ping](playback/ping.md) toutes les 10 secondes pendant la lecture du contenu principal et toutes les secondes pendant la lecture des publicités. Ping maintient la session active et enregistre les mouvements du curseur de lecture. Sur les SDK mobiles, les pings sont envoyés automatiquement. Sur toutes les autres plateformes, ils doivent être envoyés manuellement.

Envoyez le [changement de débit](playback/bitrate-change.md) chaque fois que l’algorithme de débit adaptatif du lecteur passe à un niveau de qualité différent. L’inclusion de la nouvelle valeur de débit dans les données QoE permet la création de rapports de débit moyen.

## Ajouter des événements

Les événements publicitaires effectuent le suivi de la publicité dans une session multimédia. Les scénarios courants incluent les annonces pré-roll avant le début d’une vidéo, les annonces mid-roll insérées à intervalles réguliers au cours d’une vidéo de forme longue ou d’une diffusion en direct, et les annonces post-roll après la fin du contenu. Une seule coupure publicitaire peut contenir une ou plusieurs publicités individuelles.

Chaque coupure publicitaire suit la même structure. [Début de la coupure publicitaire](ads/ad-break-start.md) ouvre la coupure et [Fin de la coupure publicitaire](ads/ad-break-complete.md) la ferme. Ces deux événements se comportent comme des bookends qui encapsulent tous les événements publicitaires individuels. Pendant la pause, envoyez [début de la publicité](ads/ad-start.md) lorsque chaque publicité individuelle commence à être lue. Suivez-la avec [Annonce terminée](ads/ad-complete.md) si l’annonce publicitaire est lue sur toute sa longueur, ou [Annonce ignorée](ads/ad-skip.md) si la visionneuse sélectionne le bouton Ignorer. Si vous omettez l’un des deux bookends, tous les événements publicitaires de la coupure sont ignorés et la durée de l’annonce est incorrectement attribuée au contenu principal.

L’exemple suivant montre la séquence d’événements correcte pour une seule coupure publicitaire contenant trois publicités, où la visionneuse a ignoré la troisième :

1. Début de la coupure publicitaire
2. Démarrage de la publicité
3. Publicité terminée
4. Démarrage de la publicité
5. Publicité terminée
6. Démarrage de la publicité
7. Annonce publicitaire ignorée
8. Coupure publicitaire terminée

## Événements de chapitre

Les événements de chapitre sont facultatifs et effectuent le suivi des segments de contenu nommés dans une session. Ils sont bien adaptés au contenu naturellement divisé en parties discrètes. Parmi les exemples courants, citons les chapitres d’un livre audio, les actes dans un documentaire, les leçons dans un cours vidéo ou les segments dans un épisode de podcast. Utilisez des événements de chapitre lorsque vous souhaitez comprendre l’engagement des observateurs au niveau du segment, par exemple pour identifier les chapitres que les audiences ont tendance à ignorer.

Envoyer [Début du chapitre](chapters/chapter-start.md) lorsqu’un chapitre commence. Si la visionneuse observe jusqu’à la fin du chapitre, envoyez [Chapitre terminé](chapters/chapter-complete.md). Si la visionneuse effectue une recherche au-delà de la limite du chapitre sans la regarder jusqu’à la fin, envoyez [Saut de chapitre](chapters/chapter-skip.md) à la place. Un chapitre doit être fermé avec un chapitre terminé ou un saut de chapitre avant qu&#39;un nouveau chapitre puisse s&#39;ouvrir ; les chapitres ne peuvent pas se chevaucher.

## Événements d’état du lecteur

Les événements d’état du lecteur suivent la façon dont les visionneuses interagissent avec les contrôles du lecteur tout au long d’une session. Ils sont utiles pour comprendre l’utilisation des fonctionnalités d’accessibilité, par exemple la fréquence à laquelle les visionneuses activent le sous-titrage ou désactivent le son. Ils révèlent également des modèles de comportement de visualisation tels que l’affichage plein écran par rapport à l’affichage en ligne et le multitâche image dans image.

Les cinq états traçables sont les suivants : `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` et `inFocus`. Envoyez [Début de l’état](player-state/state-start.md) lorsque le lecteur entre dans l’un de ces états et [Fin de l’état](player-state/state-end.md) lorsqu’il se ferme. Plusieurs états peuvent être actifs en même temps. Une visionneuse peut être active simultanément en plein écran et en sourdine. Plusieurs états peuvent se terminer au cours du même appel d’événement.

## Événements d’erreur

L’événement [Error](error.md) enregistre un échec de lecture au cours d’une session : une requête de flux ayant échoué, une erreur de codec ou un échec de diffusion externe. Envoyez-le chaque fois qu’une erreur significative se produit. Un événement d’erreur ne ferme pas la session ; la lecture peut continuer et les événements suivants sont suivis sous la même session. Si l’erreur est irrécupérable, suivez-la avec Fin de session pour fermer explicitement la session.
