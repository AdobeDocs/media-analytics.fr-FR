---
title: Configurer des rapports pour les implémentations Analytics uniquement
description: Activez les modules de suite de rapports multimédia dans Adobe Analytics afin que les données de médias en flux continu puissent être collectées et rapportées.
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 9%

---

# Configurer des rapports pour les implémentations Analytics uniquement

Pour qu’une implémentation Analytics uniquement puisse collecter des données de médias en flux continu, chaque suite de rapports qui reçoit ces données doit être configurée pour activer les modules de médias appropriés. Cette page décrit comment activer ces modules et où trouver les rapports résultants.

* **Conditions préalables** : une implémentation d’Adobe Analytics. Consultez la [présentation de l’implémentation pour Analytics uniquement](/help/implementation/analytics-only/overview.md) et la méthode d’implémentation de votre choix.

## Activation de la création de rapports multimédia sur une suite de rapports

Chaque suite de rapports qui collecte des mesures multimédia doit être configurée avant que les données multimédia ne soient envoyées.

1. Dans [&#128279;](https://experience.adobe.com/analytics), accédez à **[!UICONTROL Admin]** → **[!UICONTROL Suites de rapports]**.
1. Sélectionnez la ou les suites de rapports qui collectent les données multimédia. Sélectionnez **[!UICONTROL Modifier les paramètres]** → **[!UICONTROL Gestion des médias]** → **[!UICONTROL Rapports multimédia]**.

   ![&#x200B; Capture d’écran du menu Gestionnaire de suites de rapports &#x200B;](assets/media-reporting.png)

1. Sur la page **[!UICONTROL Rapports multimédia]**, activez les modules de médias en flux continu souhaités (voir ci-dessous).

1. Sélectionnez **[!UICONTROL Enregistrer].**

   Si cette suite de rapports est déjà configurée pour collecter des données multimédia, une page de configuration supplémentaire s’affiche après avoir sélectionné **[!UICONTROL Enregistrer]**. Si la page **[!UICONTROL Mesure Noyau multimédia]** s’affiche, passez à l’étape suivante.

## Modules de médias en flux continu disponibles

La mesure multimédia inclut les modules suivants :

* **[!UICONTROL Media Core]** : requis pour tout suivi des médias en flux continu. Il réserve les variables de solution pour la lecture du contenu et les données de session.
   * **Dimensions :**
      * [[!UICONTROL Contenu]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL &#x200B; Canal de contenu &#x200B;]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL Longueur du contenu (variable)]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL Nom du contenu (variable)]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL &#x200B; Nom du lecteur de contenu &#x200B;]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL &#x200B; Segment de contenu &#x200B;]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL &#x200B; Type de contenu &#x200B;]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL Chemin du média]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL ID de session multimédia]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL Type de flux]](/help/reporting/dimensions/stream-type.md)
   * **Mesures :**
      * [[!UICONTROL Audience moyenne par minute]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL Fin du contenu]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL Reprise du contenu]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL Vues de segment de contenu]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL Le contenu démarre]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL &#x200B; Temps passé sur le contenu &#x200B;]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL Démarrage des médias]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL Événements Pause]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL &#x200B; Flux impactés en pause &#x200B;]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL Marqueurs de progression]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL Durée totale de la pause]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL Temps de lecture unique]](/help/reporting/metrics/unique-time-played.md)
* **[!UICONTROL Publicités multimédia]** : permet le suivi des publicités dans le contenu multimédia.
   * **Dimensions :**
      * [[!UICONTROL Annonce]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL Annonce publicitaire dans la capsule]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL Longueur de l’annonce (variable)]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL Nom de l’annonce (variable)]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL Nom du lecteur publicitaire]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL capsule publicitaire]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL Publicitaire]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL ID de campagne]](/help/reporting/dimensions/campaign-id.md)
   * **Dimensions de classification :**
      * [[!UICONTROL ID de ressource]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL Évaluation du contenu]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL Date de première diffusion]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL Première date numérique]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL Nom de la capsule]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Position de la capsule]](/help/reporting/dimensions/pod-position.md)
   * **Mesures :**
      * [[!UICONTROL Fin de la publicité]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL La publicité commence]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL Temps passé sur la publicité]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL Temps passé sur le média]](/help/reporting/metrics/media-time-spent.md)
* **[!UICONTROL Chapitres multimédia]** : permet le suivi des chapitres dans le contenu multimédia.
   * **Dimension:**
      * [[!UICONTROL Chapitre]](/help/reporting/dimensions/chapter.md)
   * **Dimensions de classification :**
      * [[!UICONTROL Longueur du chapitre]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL &#x200B; Nom du chapitre &#x200B;]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL Décalage de chapitre]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL Position du chapitre]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL Originator]](/help/reporting/dimensions/originator.md)
   * **Mesures :**
      * [[!UICONTROL Fin du chapitre]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL Démarrage du chapitre]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL Durée du chapitre]](/help/reporting/metrics/chapter-time-spent.md)
* **[!UICONTROL Qualité du média]** : permet le suivi des données de qualité de lecture, y compris les événements de mise en mémoire tampon, de débit et d’erreur.
   * **Dimensions :**
      * [[!UICONTROL Débit moyen]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL Modifications de débit]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL Événements de mémoire tampon]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL Images perdues]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL Erreurs]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL ID d’erreur externe]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL ID d’erreur du SDK du lecteur]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL Heure de commencer]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL Durée totale du tampon]](/help/reporting/dimensions/total-buffer-duration.md)
   * **Mesures :**
      * [[!UICONTROL Débit moyen]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL Flux affectés par le changement de débit]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL Modifications de débit]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL Événements de mémoire tampon]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL &#x200B; Flux impactés par la mise en mémoire tampon &#x200B;]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL &#x200B; Flux impactés par l’image perdue &#x200B;]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL Images perdues]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL Pertes avant le démarrage]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL Événements d’erreur]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL &#x200B; Flux impactés par l’erreur &#x200B;]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL Heure de commencer]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL Durée totale du tampon]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL Métadonnées vidéo]** : permet le suivi des attributs de contenu vidéo standard tels que l’émission, la saison et le genre.
   * **Dimensions :**
      * [[!UICONTROL Chargements d’annonces]](/help/reporting/dimensions/ad-load-type.md)
      * [[!UICONTROL Jour]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL Épisode]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL Genre]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL Type de flux multimédia]](/help/reporting/dimensions/media-feed-type.md)
      * [&#128279;](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL Réseau]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL &#x200B; Saison &#x200B;]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL Afficher]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL Afficher le type]](/help/reporting/dimensions/show-type.md)
   * **Mesure :**
      * [[!UICONTROL Autorisé]](/help/reporting/metrics/authorized.md)
* **[!UICONTROL Métadonnées audio]** : permet le suivi des attributs de contenu audio standard tels que l’artiste, l’album et la station.
   * **Dimensions :**
      * [[!UICONTROL album]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL Artiste]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL Auteur]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Libellé]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL Éditeur]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL Station]](/help/reporting/dimensions/station.md)
* **[!UICONTROL Suivi de l’état du lecteur]** : permet de mesurer les états standard de l’interface utilisateur du lecteur, tels que le plein écran, le sous-titrage et l’image dans l’image.
   * **Mesures :**
      * [[!UICONTROL Nombre de légendes]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL Durée totale du sous-titrage]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL Nombre de pages plein écran]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL Durée totale en plein écran]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL Nombre de focus]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL Durée totale du focus]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL Nombre de mises en sourdine]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL Durée totale du son muet]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL Image dans le nombre d’images]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL Durée totale de l&#39;image dans l&#39;image]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL Flux affectés par le sous-titrage]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL Flux affectés par le plein écran]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL Flux affectés par dans le focus]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL Flux affectés par le mode muet]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL Flux affectés par l’image dans l’image]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)

>[!MORELIKETHIS]
>
>* [Rapports multimédia dans Workspace](/help/reporting/workspace/media-workspace-templates.md)
>* [Présentation des dimensions](/help/reporting/dimensions/overview.md)
>* [Présentation des mesures](/help/reporting/metrics/overview.md)
