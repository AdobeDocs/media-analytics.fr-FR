---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics pour la diffusion de médias
breadcrumb-title: Guide de Media Analytics
user-guide-description: Implémentation d’Adobe Analytics for Streaming Media. Inclut le SDK Media et l’API Media Collection.
sub-product: media analytics
source-git-commit: 5465631bf29e746d7d5dc07603f57fd7033935c4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Adobe Analytics pour la diffusion de médias {#using}

+ [Mesurer des médias en flux continu dans Adobe Analytics](media-overview.md)
+ [Périphériques et plateformes pris en charge](measurement-options/supported-devices.md)
+ Présentation de Streaming Media Analytics {#intro-to-ava}
   + [Conditions préalables](intro-to-ava/prereqs.md)
   + Chemins de mise en œuvre {#implementation-paths}
      + [Aperçu](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Côté client](intro-to-ava/implementation-paths/client-side-path.md)
      + Autres chemins de mise en œuvre {#other-paths}
         + Suivi des jalons du module média {#mm-milestone-tracking}
            + [Aperçu de Milestone](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [Migrer le jalon vers Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [Migration de Milestone vers les liens personnalisés](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Lien personnalisé dans Analytics {#cl-in-aa}
            + [Guide de mise en œuvre d’un lien personnalisé](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Activation d’Audience Manager](intro-to-ava/am-enablement.md)
+ SDK Media Analytics {#sdk-implement}
   + [FAQ sur l’abandon de la prise en charge du SDK Media Analytics](sdk-implement/end-of-support-faqs.md)
   + [Téléchargement des SDK](sdk-implement/download-sdks.md)
   + Installation et configuration {#setup}
      + [Aperçu](sdk-implement/setup/setup-overview.md)
      + [Configuration d’Android](sdk-implement/setup/set-up-android.md)
      + [Configuration d’iOS](sdk-implement/setup/set-up-ios.md)
      + Configuration de JavaScript {#setup-javascript}
         + [Configuration de JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [Configuration de JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Configuration de Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Configuration de Roku](sdk-implement/setup/set-up-roku.md)
   + Suivi de la lecture des médias en flux continu {#track-av-playback}
      + [Aperçu](sdk-implement/track-av-playback/track-core-overview.md)
      + Suivi de la lecture principale des médias en flux continu {#track-core}
         + [Suivi de la lecture principale sur Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Suivi de la lecture principale sur iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + Suivi de la lecture principale sur JavaScript {#track-core-javascript}
            + [Suivi de la lecture principale sur JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [Suivi de la lecture principale sur JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Suivi de la lecture principale sur Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Suivi de la lecture principale sur Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Suivi de la mise en mémoire tampon {#track-buffering}
         + [Suivi de la mise en mémoire tampon sur Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Suivi de la mise en mémoire tampon sur iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + Suivi de la mise en mémoire tampon sur JavaScript {#track-buffering-js}
            + [Suivi de la mise en mémoire tampon sur JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [Suivi de la mise en mémoire tampon sur JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Suivi de la mise en mémoire tampon sur Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Suivi de la mise en mémoire tampon sur Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Suivi de la recherche {#track-seeking}
         + [Suivi de la recherche sur Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Suivi de la recherche sur iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + Suivi de la recherche sur JavaScript {#track-seeking-js}
            + [Suivi de la recherche sur JavaScript 2.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [Suivi de la recherche sur JavaScript 3.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Suivi de la recherche sur Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Suivi de la recherche sur Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Mise en œuvre de métadonnées standard {#impl-std-metadata}
         + [Mise en œuvre de métadonnées standard sur Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Mise en œuvre de métadonnées standard sur iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Clés de métadonnées iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Mise en œuvre de métadonnées standard sur JavaScript {#impl-std-md-js}
            + [Mise en œuvre de métadonnées standard sur JavaScript 2.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [Mise en œuvre de métadonnées standard sur JavaScript 3.x](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Mise en œuvre de métadonnées standard sur Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Paramètres des métadonnées standard - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Mise en œuvre de métadonnées standard sur Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Paramètres des métadonnées standard - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Suivi des publicités {#track-ads}
      + [Aperçu](sdk-implement/track-ads/track-ads-overview.md)
      + [Suivi des publicités sur Android](sdk-implement/track-ads/track-ads-android.md)
      + [Suivi des publicités sur iOS](sdk-implement/track-ads/track-ads-ios.md)
      + Suivi des publicités sur JavaScript {#track-ads-js}
         + [Suivi des publicités sur JavaScript 2.x](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [Suivi des publicités sur JavaScript 3.x](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Suivi des publicités sur Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Suivi des publicités sur Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Mise en œuvre de métadonnées de publicité standard {#impl-std-ad-metadata}
         + [Mise en œuvre de métadonnées de publicité standard sur Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Mise en œuvre de métadonnées de publicité standard sur iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Mise en œuvre de métadonnées de publicité standard sur JavaScript {#impl-std-ad-md-js}
            + [Mise en œuvre de métadonnées de publicité standard sur JavaScript 2.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Mise en œuvre de métadonnées de publicité standard sur JavaScript 3.x](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Mise en œuvre de métadonnées de publicité standard sur Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Suivi des chapitres et des segments {#track-chapters}
      + [Aperçu](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Suivi des chapitres et des segments sur Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Suivi des chapitres et des segments sur iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + Suivi des chapitres et des segments sur JavaScript {#track-chapters-js}
         + [Suivi des chapitres et des segments sur JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Suivi des chapitres et des segments sur JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Suivi des chapitres et des segments sur Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Suivi des chapitres et des segments sur Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Suivi de la qualité de l’expérience {#track-qos}
      + [Aperçu](sdk-implement/track-qos/track-qos-overview.md)
      + [Suivi de la qualité de l’expérience sur Android](sdk-implement/track-qos/track-qos-android.md)
      + [Suivi de la qualité de l’expérience sur iOS](sdk-implement/track-qos/track-qos-ios.md)
      + Suivi de la qualité de l’expérience sur JavaScript {#track-qos-js}
         + [Suivi de la qualité de l’expérience sur JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [Suivi de la qualité de l’expérience sur JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Suivi de la qualité de l’expérience sur Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Suivi de la qualité de l’expérience sur Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Erreurs de suivi {#track-errors}
      + [Aperçu](sdk-implement/track-errors/track-errors-overview.md)
      + [Erreurs de suivi sur Android](sdk-implement/track-errors/track-errors-android.md)
      + [Erreurs de suivi sur iOS](sdk-implement/track-errors/track-errors-ios.md)
      + Erreurs de suivi sur JavaScript {#track-errors-js}
         + [Erreurs de suivi sur JavaScript 2.x](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [Erreurs de suivi sur JavaScript 3.x](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Erreurs de suivi sur Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Erreurs de suivi sur Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Exclusion et confidentialité](sdk-implement/opt-out-privacy.md)
   + Scénarios de suivi {#tracking-scenarios}
      + [Lecture VOD sans publicité](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Lecture VOD avec publicités preroll](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Lecture VOD avec publicités ignorées](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
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
      + [Test 1 - Lecture standard](sdk-implement/validation/test1-standard-playback.md)
      + [Test 2 - Interruption du média](sdk-implement/validation/test2-media-interrupt.md)
      + [Détails des appels de test](sdk-implement/validation/test-call-details.md)
      + [Descriptions des paramètres Heartbeat](sdk-implement/validation/heartbeat-params.md)
      + Débogage {#debugging}
         + [Débogage du SDK](sdk-implement/validation/debugging/sdk-debugging.md)
   + Analytics dans les applications OTT {#analytics-with-ott}
      + [Suivi des états de l’application](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Suivi des actions de l’application](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Configuration d’identifiants utilisateur](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT et Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT et Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Guide pas à pas {#cookbook}
      + [Guide pas à pas SDK](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [Gestion des interruptions de l’application lors de la lecture](sdk-implement/cookbook/app-interrupts.md)
      + [Résolution des appels main:play apparaissant entre les publicités](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Reprise des sessions inactives](sdk-implement/cookbook/resuming-inactive.md)
      + [Suivi dans SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migration de Media Analytics 1.x vers 2.x {#va-1x-to-2x}
      + [Présentation de la migration](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Comparaison de code : 1.x vers 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversion de l’API 1.x vers 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + Migration du SDK Media Analytics vers Launch {#sdk-to-launch}
      + [Migration du SDK vers Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + Guides de plateforme pour la migration du SDK vers Launch {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ API Media Collection (RESTful) {#media-collection-api}
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
   + Chronologies du suivi multimédia {#mc-api-timelines}
      + [Chronologie 1 : Regarder jusqu’à la fin du contenu](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Chronologie 2 : L’utilisateur abandonne la session](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Chronologie 3 : Chapitres](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Guide pas à pas {#media-analytics-cookbook}
   + [Guide pas à pas](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Attribution des diffusions multimédia](media-analytics-cookbook/media-dimensions.md)
+ Mesures et métadonnées {#metrics-and-metadata}
   + [Paramètres des médias en flux continu](metrics-and-metadata/audio-video-parameters.md)
   + [Paramètres de publicité](metrics-and-metadata/ad-parameters.md)
   + [Paramètres de chapitre](metrics-and-metadata/chapter-parameters.md)
   + [Paramètres d’état du lecteur](metrics-and-metadata/player-state-parameters.md)
   + [Paramètres de qualité](metrics-and-metadata/quality-parameters.md)
   + [Segments](metrics-and-metadata/segments.md)
   + [Mesures calculées](metrics-and-metadata/calculated-metrics.md)
+ Rapports et analyses {#media-reports}
   + [Activation des rapports multimédia](media-reports/media-reports-enable.md)
   + Rapports multimédia par défaut {#media-default-reports}
      + [Aperçu des rapports par défaut](media-reports/media-default-reports/default-reports-overview.md)
      + [Présentation du média](media-reports/media-default-reports/media-reports-overview.md)
      + [Détails du média](media-reports/media-default-reports/media-reports-detail.md)
      + [Rapport sur les tranches horaires des médias](media-reports/media-default-reports/media-reports-daypart.md)
      + [Rapport sur les observateurs simultanés de médias](media-reports/media-default-reports/media-concurrent-viewers.md)
   + Panneaux Workspace multimédia {#media-workspace-panels}
   + [Panneau Audience moyenne par minute du média](media-reports/media-workspace-panels/average-minute-audience.md)
   + [Panneau des visionneuses simultanées de médias](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Panneau Temps de lecture de média](media-reports/media-workspace-panels/media-playback-time-spent.md)
   + [Modèles Workspace multimédia](media-reports/media-workspace-templates.md)
   + [Obtenir des données d’observateurs simultanés via l’API](media-reports/media-default-reports/get-concurrent-json20.md)
   + [Obtention des données de temps de lecture de média via l’API](media-reports/media-default-reports/get-mediaplaybacktimespent-json20.md)
+ [Suivi du contenu téléchargé](media-collection-api/track-downloaded-content.md)
+ Suivi de l’état du lecteur {#player-state-tracking}
   + [Aperçu](sdk-implement/player-state-tracking/player-state-overview.md)
   + [États standard et personnalisés](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [Mise en œuvre et création de rapports](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [Exemples de suivi de l’état du lecteur](sdk-implement/player-state-tracking/player-state-examples.md)
+ [Federated Analytics](federated-analytics.md)
+ Ressources supplémentaires {#additional-resources}
   + [Notes de mise à jour](additional-resources/doc-updates.md)

<!-- + Player State Tracking {#player-state-tracking}
    + [Overview](sdk-implement/player-state-tracking/player-state-overview.md)
    + [Standard and custom states](sdk-implement/player-state-tracking/standard-and-custom-states.md)
    + [Implementation and reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
    + [Player state tracking examples](sdk-implement/player-state-tracking/player-state-examples.md)
-->
