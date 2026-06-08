---
title: Suivi de la lecture du contenu
description: Découvrez le suivi de la lecture principale, y compris le suivi du chargement et du démarrage des médias, ainsi que la mise en pause et la fin des médias.
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 807
ht-degree: 3%

---


# Suivi de la lecture du contenu

Le suivi de la lecture principale couvre le chargement du média, le démarrage, la mise en pause, la reprise, la fin et la fin de la session. Bien que cela ne soit pas obligatoire, la mise en mémoire tampon et le suivi de la recherche sont également des composants principaux d’une implémentation de lecture complète.

## Événements du lecteur

| Événement du lecteur | Action |
| --- | --- |
| Charge du média | Créer un objet média ; appeler SessionStart |
| Démarrage du média | Lecture d’appel |
| Pause | PauseStart de l’appel |
| Reprendre à partir de la pause | Lecture d’appel |
| Fin du média | Fin de la session d’appel |
| Abandon/déchargement du média | Call SessionEnd |
| La mise en mémoire tampon commence | DébutTamponAppel |
| Fin de la mise en mémoire tampon | Lecture des appels (CV) |
| Recherche de démarrages | Appel à SeekStart |
| Recherche de fins | Appel de SeekComplete ; puis appel de Play |

## Procédure de mise en œuvre

1. **Identifier le moment où l’utilisateur déclenche la lecture** (l’utilisateur clique sur lecture ou la lecture automatique se déclenche). Créez un objet média avec le nom de contenu, l’identifiant, la longueur, le type de diffusion et le type de média. Voir [Nom du contenu](/help/implementation/variables/core/content-name.md), [Identifiant du contenu](/help/implementation/variables/core/content-id.md), [Longueur du contenu](/help/implementation/variables/core/content-length.md), [Type de flux](/help/implementation/variables/core/stream-type.md) et [Type de contenu](/help/implementation/variables/core/content-type.md) pour obtenir des définitions de champ.
1. **Vous pouvez éventuellement joindre des métadonnées** : métadonnées standard (émission, saison, épisode, etc.) et les variables de données contextuelles personnalisées. Pour obtenir des références de clés de métadonnées standard, consultez [Programme](/help/implementation/variables/standard-metadata/show.md), [Saison](/help/implementation/variables/standard-metadata/season.md), [Épisode](/help/implementation/variables/standard-metadata/episode.md), [Genre](/help/implementation/variables/standard-metadata/genre.md) et [Réseau](/help/implementation/variables/standard-metadata/network.md).
1. **Appelez [Début de session](/help/implementation/events/session/session-start.md)** pour commencer à suivre la session. Cette opération charge les données et les métadonnées et démarre la mesure de QoS du temps de démarrage. SessionStart effectue le suivi de l’*intention* de lecture, et non de la première image.
1. **Appeler [Lire](/help/implementation/events/playback/play.md)** lorsque la première image du contenu s’affiche à l’écran.
1. **Appel [Démarrage de la pause](/help/implementation/events/playback/pause-start.md)** lorsque le lecteur est en pause. Appelez à nouveau la fonction Lire lorsque la lecture reprend. Il n’existe pas d’événement de reprise distinct.
1. **Appel [Fin de la session](/help/implementation/events/session/session-complete.md)** lorsque la visionneuse atteint la fin du contenu.
1. **Appel [Fin de session](/help/implementation/events/session/session-end.md)** lorsque le lecteur est déchargé ou que la visionneuse abandonne le contenu sans atteindre la fin. SessionEnd ferme immédiatement la session ; aucun autre événement ne peut être suivi après.

>[!IMPORTANT]
>
>`SessionEnd` marque la fin d’une session de suivi. Si la session a été visionnée jusqu’à la fin, appelez le `SessionComplete` avant de `SessionEnd`. Tout autre appel de tracking est ignoré après `SessionEnd`, à l&#39;exception de `SessionStart` pour une nouvelle session.

## Lecture principale

Les exemples suivants montrent un flux de session complet, du début à la fin de la session, en passant par la fin du contenu.

Pour plus d’informations sur l’implémentation par plateforme, consultez les sections [Début de session](/help/implementation/events/session/session-start.md), [Lecture](/help/implementation/events/playback/play.md), [Début de pause](/help/implementation/events/playback/pause-start.md), [Fin de session](/help/implementation/events/session/session-complete.md) et [Fin de session](/help/implementation/events/session/session-end.md).

## Mise en mémoire tampon

Le début de la mémoire tampon indique que le lecteur attend des données. La fin de la mémoire tampon est déduite lorsque vous envoyez un événement de lecture après BufferStart (API basées sur XDM). Sur Mobile SDK, appelez également explicitement BufferComplete.

Pour plus d’informations sur l’implémentation, voir [Début de la mémoire tampon](/help/implementation/events/playback/buffer-start.md).

## Recherche en cours

Le bouton Démarrer la recherche signale que la visionneuse est en train de nettoyer. La fin de la recherche est suivie de Lecture pour reprendre la lecture du contenu.

Pour plus d’informations sur l’implémentation, voir [Démarrage de la pause](/help/implementation/events/playback/pause-start.md) (démarrage de la recherche) et [Lecture](/help/implementation/events/playback/play.md) (fin de la recherche).

## Gérer les interruptions de l’application

La lecture dans une application multimédia peut être interrompue de différentes manières. Par exemple, lorsque l’utilisateur appuie sur pause, que l’application passe en arrière-plan ou qu’un appel téléphonique arrive. Quelle que soit la cause, les instructions de suivi sont les mêmes :

1. Appelez **PauseStart** lorsque l’application est interrompue (passage en arrière-plan, pause du média, etc.).
1. Appelez **Play** lorsque l’application revient au premier plan et/ou que le média reprend la lecture.

>[!NOTE]
>
>N’appelez pas SessionStart lorsque l’application revient de l’arrière-plan. L’appel de SessionStart entraîne la non-prise en compte de la lecture jusqu’à ce point dans le temps de lecture total, et la perte des marqueurs de progression, des segments et des limites de chapitre précédents.

**Quand une session en pause doit-elle se terminer ?** Si l’application n’autorise pas la lecture en arrière-plan, appelez PauseStart immédiatement, puis appelez SessionEnd après environ une minute en arrière-plan. L’application ne peut pas continuer à envoyer des pings de pause à partir de l’arrière-plan et le fait de maintenir la session ouverte indéfiniment offre une mauvaise expérience. Si l’application ne prend pas en charge la lecture en arrière-plan (applications audio, applications de podcast vidéo), continuez à envoyer des pings en arrière-plan.

**Redémarrage après une longue période en arrière-plan :** si l’application a été exécutée en arrière-plan suffisamment longtemps pour que la session expire (inactivité de 30 minutes), appelez SessionEnd pour fermer proprement toute session restante, puis appelez SessionStart pour commencer une nouvelle session lorsque la visionneuse revient.

## Reprise des sessions inactives

Une session expire automatiquement si aucun événement n’est reçu pendant 10 minutes ou s’il n’y a aucun mouvement du curseur de lecture pendant 30 minutes. Si l’utilisateur revient après l’expiration d’une session, appelez à nouveau SessionStart pour ouvrir une nouvelle session.

**Reprise entre les appareils (transfert entre appareils) :** lorsqu’une visionneuse transfère la lecture entre les appareils (par exemple, la diffusion d’un téléphone vers un téléviseur), utilisez l’indicateur de reprise pour regrouper les sessions dans les rapports Analytics :

1. Sur l’**appareil source**, appelez SessionEnd lorsque la visionneuse lance le cast. Ne pas appeler SessionComplete — le contenu n&#39;est pas terminé.
1. Sur l’appareil **de destination**, appelez SessionStart avec l’indicateur de reprise défini sur `true` et transmettez les mêmes métadonnées de contenu et la même position de la tête de lecture à partir de l’appareil source.

La définition de l’indicateur de reprise entraîne l’incrémentation d’Analytics [Reprises du contenu](/help/reporting/metrics/content-resumes.md) plutôt que [Débuts du média](/help/reporting/metrics/media-starts.md) pour la deuxième étape de la remise.

**Reprise manuelle d’une session précédemment fermée :** si l’application stocke les données utilisateur et peut reprendre une session précédemment fermée, définissez l’indicateur de reprise au début de la session. Voir [Début de session](/help/implementation/events/session/session-start.md#resuming-a-session) pour les détails d’implémentation sur toutes les plateformes.
