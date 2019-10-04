---
product: Media Analytics
audience: utilisateur final
user-guide-title: Adobe Analytics pour l’audio et la vidéo
translation-type: tm+mt
source-git-commit: b0aae4555f2193f5aa03e647adeac6c322b6b389

---


# Adobe Analytics for Audio and Video {#using}

+ [Mesure de l’audio et de la vidéo dans Adobe Analytics](media-overview.md)
+ Measurement Options {#measurement-options}
   + Media Module Milestone Tracking {#mm-milestone-tracking}
      + [Aperçu de Milestone](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrer l’jalon vers Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migration de Milestone vers les liens personnalisés](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Lien personnalisé dans Analytics {#cl-in-aa}
      + [Custom Link Implementation Guide](measurement-options/cl-in-aa/cl-impl-guide.md)
+ Présentation des analyses audio et vidéo {#intro-to-ava}
   + [Conditions préalables](intro-to-ava/prereqs.md)
   + Chemins de mise en œuvre {#implementation-paths}
      + [Aperçu](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Côté client](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Activation d’Audience Manager](intro-to-ava/am-enablement.md)
+ SDK Media Analytics {#sdk-implement}
   + [Téléchargement des SDK](sdk-implement/download-sdks.md)
   + Installation et configuration {#setup}
      + [Aperçu](sdk-implement/setup/setup-overview.md)
      + [Configuration d’Android](sdk-implement/setup/set-up-android.md)
      + [Configuration d’iOS](sdk-implement/setup/set-up-ios.md)
      + [Configuration de JavaScript](sdk-implement/setup/set-up-js.md)
      + [Configuration de Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Configuration de Roku](sdk-implement/setup/set-up-roku.md)
   + Suivi de la lecture audio et vidéo {#track-av-playback}
      + [Aperçu](sdk-implement/track-av-playback/track-core-overview.md)
      + Track Core Audio and Video Playback {#track-core}
         + [Suivi de la lecture principale sur Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Track Core Playback on iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [Track Core Playback on JavaScript](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Track Core Playback on Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Suivi de la lecture principale sur Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Track Buffering {#track-buffering}
         + [Mise en mémoire tampon du suivi sur Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Track Buffering on iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [Track Buffering on JavaScript](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Track Buffering on Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Track Buffering on Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Track Seeking {#track-seeking}
         + [Track Seeking on Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Track Seeking on iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [Track Seeking on JavaScript](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Recherche de pistes sur Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Recherche de pistes sur Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Mise en œuvre de métadonnées standard {#impl-std-metadata}
         + [Mise en œuvre de métadonnées standard sur Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Mise en œuvre de métadonnées standard sur iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Clés de métadonnées iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [Mise en œuvre de métadonnées standard sur JavaScript](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Mise en œuvre de métadonnées standard sur Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Standard Metadata Parameters - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Mise en œuvre de métadonnées standard sur Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Standard Metadata Parameters - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Suivi des publicités {#track-ads}
      + [Aperçu](sdk-implement/track-ads/track-ads-overview.md)
      + [Track Ads on Android](sdk-implement/track-ads/track-ads-android.md)
      + [Suivi des publicités sur iOS](sdk-implement/track-ads/track-ads-ios.md)
      + [Suivi des publicités sur JavaScript](sdk-implement/track-ads/track-ads-js.md)
      + [Suivi des publicités sur Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Track Ads on Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Mise en œuvre de métadonnées de publicité standard {#impl-std-ad-metadata}
         + [Mise en œuvre de métadonnées de publicité standard sur Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Mise en œuvre de métadonnées de publicité standard sur iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [Mise en œuvre de métadonnées de publicité standard sur JavaScript](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Mise en œuvre de métadonnées de publicité standard sur Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Suivi des chapitres et des segments {#track-chapters}
      + [Aperçu](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Track Chapters and Segments on Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Suivi des chapitres et des segments sur iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + [Suivi des chapitres et des segments sur JavaScript](sdk-implement/track-chapters/track-chapters-js.md)
      + [Suivi des chapitres et des segments sur Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Track Chapters and Segments on Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Suivi de la qualité de l’expérience {#track-qos}
      + [Aperçu](sdk-implement/track-qos/track-qos-overview.md)
      + [Track Quality of Experience on Android](sdk-implement/track-qos/track-qos-android.md)
      + [Suivi de la qualité de l’expérience sur iOS](sdk-implement/track-qos/track-qos-ios.md)
      + [Track Quality of Experience on JavaScript](sdk-implement/track-qos/track-qos-js.md)
      + [Track Quality of Experience on Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Track Quality of Experience on Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Track Errors {#track-errors}
      + [Aperçu](sdk-implement/track-errors/track-errors-overview.md)
      + [Suivi des erreurs sur Android](sdk-implement/track-errors/track-errors-android.md)
      + [Suivi des erreurs sur iOS](sdk-implement/track-errors/track-errors-ios.md)
      + [Suivi des erreurs sur JavaScript](sdk-implement/track-errors/track-errors-js.md)
      + [Suivi des erreurs sur Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Suivi des erreurs sur Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Exclusion et confidentialité](sdk-implement/opt-out-privacy.md)
   + Tracking Scenarios {#tracking-scenarios}
      + [Lecture VOD sans publicité](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Lecture VOD avec publicités preroll](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Lecture VOD avec saut de publicité](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [Lecture VOD avec un chapitre](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [Lecture VOD avec saut de chapitre](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [Lecture VOD avec recherche dans le contenu principal](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [Lecture VOD avec mise en mémoire tampon](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Plusieurs dispositifs de suivi VOD en parallèle](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [Un dispositif de suivi VOD pour plusieurs sessions](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Contenu principal en direct](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Contenu principal en direct avec suivi séquentiel](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validation {#validation}
      + [Aperçu de la validation](sdk-implement/validation/validation-overview.md)
      + [Test 1 : Lecture standard](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2 : Interruption des médias](sdk-implement/validation/test2-media-interrupt.md)
      + [Détails de l'appel de test](sdk-implement/validation/test-call-details.md)
      + [Descriptions des paramètres Heartbeat](sdk-implement/validation/heartbeat-params.md)
      + Débogage {#debugging}
         + [Débogage du SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Configuration d’Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Création d’un nouveau rapport de débogage](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Tableaux de bord et rapports de débogage](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT Apps {#analytics-with-ott}
      + [Suivi des états de l’application](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Suivi des actions de l’application](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Set User IDs](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT et Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT et Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Guide pas à pas {#cookbook}
      + [Gestion des interruptions de l’application lors de la lecture](sdk-implement/cookbook/app-interrupts.md)
      + [Résolution des appels main:play apparaissant entre les publicités](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Resuming Inactive Sessions](sdk-implement/cookbook/resuming-inactive.md)
      + [Suivi dans SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
      + [Différences entre le SDK et le lancement](sdk-implement/cookbook/sdk-vs-launch-qoe.md)
   + Media Analytics 1.x to 2.x Migration {#va-1x-to-2x}
      + [Présentation de la migration](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Comparaison de code  : 1.x vers 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversion de l’API 1.x vers 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
+ API de collection de médias (RESTful) {#media-collection-api}
   + [Aperçu](media-collection-api/mc-api-overview.md)
   + Référence d’API {#mc-api-ref}
      + [Requête Sessions](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Requête events](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Paramètres de requête](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Types et descriptions d’événement](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [Schémas de validation JSON](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Mise en œuvre de l’API {#mc-api-impl}
      + [Démarrage rapide](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Définition du type de requête HTTP dans votre lecteur](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Obtention d’un ID de session](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Mise en œuvre d’une requête events](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Validation des requêtes d’événement](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Envoi d’événements ping](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Envoi de données QoE](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Prise en charge des métadonnées personnalisées](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Conditions d’expiration](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Contrôle de l’ordre des événements](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Événements de mise en file d’attente lorsque la réponse des sessions est lente](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Media Tracking Timelines {#mc-api-timelines}
      + [Chronologie 1 : Regarder jusqu’à la fin du contenu](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Chronologie 2 : L’utilisateur abandonne la session](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Chronologie 3 : Chapitres](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [Track Downloaded Content](media-collection-api/track-downloaded-content.md)
+ Mesures et métadonnées {#metrics-and-metadata}
   + [Paramètres audio et vidéo](metrics-and-metadata/audio-video-parameters.md)
   + [Paramètres de publicité](metrics-and-metadata/ad-parameters.md)
   + [Paramètres de chapitre](metrics-and-metadata/chapter-parameters.md)
   + [Paramètres de qualité](metrics-and-metadata/quality-parameters.md)
   + [Segments](metrics-and-metadata/segments.md)
   + [Mesures calculées](metrics-and-metadata/calculated-metrics.md)
+ Reporting and Analysis {#media-reports}
   + [Activation des rapports sur les médias](media-reports/media-reports-enable.md)
   + Media Default Reports {#media-default-reports}
      + [Présentation des rapports par défaut](media-reports/media-default-reports/default-reports-overview.md)
      + [Présentation du média](media-reports/media-default-reports/media-reports-overview.md)
      + [Détails du média](media-reports/media-default-reports/media-reports-detail.md)
      + [Tranche horaire du média](media-reports/media-default-reports/media-reports-daypart.md)
      + [Visionneuses simultanées de médias](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [Obtention des données du rapport JSON sur les visionneuses simultanées](media-reports/media-default-reports/get-concurrent-json.md)
   + [Modèles Media Workspace](media-reports/media-workspace-templates.md)
+ [Federated Analytics](data-sharing/federated-analytics.md)
+ Ressources supplémentaires {#additional-resources}
   + [Mises à jour de la documentation](additional-resources/doc-updates.md)

