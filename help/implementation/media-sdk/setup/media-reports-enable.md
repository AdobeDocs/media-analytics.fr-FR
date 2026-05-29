---
title: Activation des rapports multimédia
description: Découvrez la suite de rapports multimédia qui collecte les mesures multimédia.  Pour configurer les rapports multimédia avant l’envoi des données multimédia, procédez comme suit.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 20%

---

# Activation des rapports multimédia

Chaque suite de rapports qui collecte des mesures multimédia doit être configurée avant que les données multimédia ne soient envoyées.

1. Dans [](https://experience.adobe.com/analytics), accédez à **[!UICONTROL Admin]** → **[!UICONTROL Suites de rapports]**.
1. Sélectionnez la ou les suites de rapports qui collectent les données multimédia. Sélectionnez **[!UICONTROL Modifier les paramètres]** → **[!UICONTROL Gestion des médias]** → **[!UICONTROL Rapports multimédia]**.

   ![ Capture d’écran du menu Gestionnaire de suites de rapports ](assets/media-reporting.png)

1. Sur la page **[!UICONTROL Création de rapports multimédia]**, activez les composants de médias en flux continu souhaités (voir ci-dessous).

1. Sélectionnez **[!UICONTROL Enregistrer].**

   Si cette suite de rapports est déjà configurée pour collecter les données multimédia, une fois que vous avez cliqué sur **[!UICONTROL Enregistrer]**, une page de configuration supplémentaire s’affiche. Si la page **[!UICONTROL Mesure Noyau multimédia]** s’affiche, passez à l’étape suivante.

## Modules de médias en flux continu disponibles

La mesure multimédia inclut les modules suivants :

* **[!UICONTROL Media Core]** : requis pour tout suivi des médias en flux continu. Il réserve les variables de solution pour la lecture du contenu et les données de session.
   * **Dimensions :**
      * [[!UICONTROL Contenu]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL  Canal de contenu ]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL Longueur du contenu (variable)]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL Nom du contenu (variable)]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL  Nom du lecteur de contenu ]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL  Segment de contenu ]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL  Type de contenu ]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL Chemin du média]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL ID de session multimédia]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL Type de flux]](/help/reporting/dimensions/stream-type.md)
   * **Mesures :**
      * [[!UICONTROL Audience moyenne par minute]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL Fin du contenu]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL Reprise du contenu]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL Vues de segment de contenu]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL Le contenu démarre]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL  Temps passé sur le contenu ]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL Démarrage des médias]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL Événements Pause]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL  Flux impactés en pause ]](/help/reporting/metrics/paused-impacted-streams.md)
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
      * [[!UICONTROL  Nom du chapitre ]](/help/reporting/dimensions/chapter-name.md)
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
      * [[!UICONTROL  Flux impactés par la mise en mémoire tampon ]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL  Flux impactés par l’image perdue ]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL Images perdues]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL Pertes avant le démarrage]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL Événements d’erreur]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL  Flux impactés par l’erreur ]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL Heure de commencer]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL Durée totale du tampon]](/help/reporting/metrics/total-buffer-duration.md)
* **[!UICONTROL Métadonnées vidéo]** : permet le suivi des attributs de contenu vidéo standard tels que l’émission, la saison et le genre.
   * **Dimensions :**
      * [!UICONTROL Chargements d’annonces]
      * [[!UICONTROL Jour]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL Épisode]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL Genre]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL Type de flux multimédia]](/help/reporting/dimensions/media-feed-type.md)
      * [](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL Réseau]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL  Saison ]](/help/reporting/dimensions/season.md)
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
