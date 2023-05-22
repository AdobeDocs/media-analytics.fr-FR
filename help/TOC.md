---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics for Streaming Media
breadcrumb-title: Guide de Media Analytics
user-guide-description: Implémentation d’Adobe Analytics for Streaming Media. Inclut le SDK Media et l’API Media Collection.
sub-product: media analytics
source-git-commit: 129818d73bdcc63fcf922d295e3f360ab1375dbe
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 99%

---


# Adobe Analytics for Streaming Media {#using}

+ [Guide d’analyse des médias en flux continu](media-overview.md)
+ Notes de mise à jour {#release-notes}
   + [Notes de mise à jour des médias en flux continu](additional-resources/release-notes.md)
+ Prise en main {#getting-started}
   + [Aperçu](getting-started/getting-started.md)
   + [Conditions préalables](getting-started/prereqs.md)
   + [Périphériques pris en charge](getting-started/supported-devices.md)
   + [Documentation sur les médias en flux continu](getting-started/implementation-documentation.md)
   + [SDK, bibliothèques et extensions](getting-started/download-sdks.md)
   + Fin de la prise en charge {#end-of-support}
      + [Fin de la prise en charge du SDK Media Analytics Mobile](additional-resources/end-of-support-faqs.md)
      + Hérité - Migration du SDK Media autonome vers Launch {#sdk-to-launch}
         + [Aperçu](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - SDK Media vers Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - SDK Media vers Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - SDK Media vers Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Implémentation {#implementation}
   + [Présentation de l’implémentation](implementation/overview.md)
   + SDK Media - Implémentation {#media-sdk}
      + [Présentation des SDK Media](implementation/media-sdk/media-sdk-overview.md)
      + Installation et configuration {#setup}
         + Installer les SDK web {#install-web-sdk}
            + [Installer Analytics à l’aide de JavaScript](implementation/media-sdk/setup/web-implementation.md)
            + [Installer Analytics à l’aide de l’extension Media Analytics](implementation/media-sdk/setup/web-implementation-tags.md)
         + [Installer les SDK mobiles](implementation/media-sdk/setup/mobile-implementation.md)
         + Installation des SDK OTT {#ott-setup}
            + [Installation du SDK Chromecast](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Installation du SDK Roku](implementation/media-sdk/setup/set-up-roku.md)
   + [Installation d’Analytics avec Adobe Experience Platform Edge](implementation/implementation-edge.md)
   + API Media Collection - Implémentation {#streaming-media-apis}
      + [Media Collection](implementation/media-collection-api/mc-api-overview.md)
      + [Démarrage rapide de l’API](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Requête Sessions](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Requête events](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Paramètres de requête](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Types et descriptions d’événement](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
      + Mise en œuvre de l’API {#mc-api-impl}
         + [Définition du type de requête HTTP dans votre lecteur](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
         + [Obtention d’un ID de session](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
         + [Mise en œuvre d’une requête events](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
         + [Schémas de validation JSON](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
         + [Validation des requêtes d’événement](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
         + [Envoi d’événements ping](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
         + [Envoi de données QoE](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
         + [Prise en charge des métadonnées personnalisées](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
         + [Conditions d’expiration](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
         + [Contrôle de l’ordre des événements](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
         + [Événements de mise en file d’attente lorsque la réponse des sessions est lente](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variables {#variables}
      + [Paramètres des médias en flux continu](implementation/variables/audio-video-parameters.md)
      + [Paramètres de publicité](implementation/variables/ad-parameters.md)
      + [Paramètres de chapitre](implementation/variables/chapter-parameters.md)
      + [Paramètres d’état du lecteur](implementation/variables/player-state-parameters.md)
      + [Paramètres de qualité](implementation/variables/quality-parameters.md)
      + [Mesures calculées](implementation/variables/calculated-metrics.md)
+ Création de rapports {#media-reports}
   + [Activation des rapports multimédia](reporting/media-reports-enable.md)
   + [À propos des segments](reporting/segments.md)
   + Rapports multimédia par défaut {#media-default-reports}
      + [Aperçu des rapports par défaut](reporting/reports-and-analytics/default-reports-overview.md)
      + [Présentation du média](reporting/reports-and-analytics/media-reports-overview.md)
      + [Détails du média](reporting/reports-and-analytics/media-reports-detail.md)
      + [Rapport sur les tranches horaires des médias](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Rapport sur les observateurs simultanés de médias](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + Panneaux d’espace de travail multimédia {#media-workspace-panels}
      + [Panneau Audience moyenne par minute de média](reporting/workspace/average-minute-audience.md)
      + [Panneau Observateurs simultanés de médias](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Panneau Temps de lecture de média](reporting/workspace/media-playback-time-spent.md)
   + [Modèles d’espaces de travail multimédia ](reporting/workspace/media-workspace-templates.md)
   + [Obtenir des données d’observateurs simultanés via l’API](reporting/reports-and-analytics/get-concurrent-json20.md)
   + [Obtention des données de temps de lecture de média via l’API](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Cas d’utilisation {#media-use-cases}
   + [Cas d’utilisation du SDK Media](use-cases/cookbook/sdk-cookbook-overview.md)
   + Suivi de l’état du lecteur {#player-state-tracking}
      + [Aperçu](use-cases/player-state-tracking/player-state-overview.md)
      + [États standard et personnalisés](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Mise en œuvre et création de rapports](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Suivi de plusieurs états du lecteur](use-cases/player-state-tracking/multiple-player-states.md)
      + [Exemples de suivi de l’état du lecteur](use-cases/player-state-tracking/player-state-examples.md)
   + [Effectuer le suivi du contenu téléchargé hors ligne](use-cases/track-downloaded-content.md)
   + [Federated Analytics ](use-cases/federated-analytics.md)
   + [Gestion des interruptions de l’application lors de la lecture](use-cases/cookbook/app-interrupts.md)
   + [Attribution des diffusions multimédia](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [Reprise des sessions inactives](use-cases/cookbook/resuming-inactive.md)
   + [Suivi Roku dans SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Gestion des écarts entre les publicités](use-cases/cookbook/fix-ad-play-ad.md)
   + Chronologies {#timelines}
      + [Début et fin du chapitre](use-cases/timelines/chapter-start-end.md)
      + [Affichage à la fin du contenu](use-cases/timelines/view-to-end-of-content.md)
      + [Abandon de session](use-cases/timelines/user-abandons-session.md)
   + Utilisation d’Analytics dans les applications OTT {#analytics-with-ott}
      + [Suivi des états de l’application](use-cases/analytics-with-ott/track-app-states.md)
      + [Suivi des actions de l’application](use-cases/analytics-with-ott/track-app-actions.md)
      + [Configuration d’identifiants utilisateur](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT et Audience Manager](use-cases/analytics-with-ott/ott-am.md)
      + [OTT et Experience Cloud](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Suivi {#tracking}
   + Suivi {#track-av-playback}
      + [Aperçu](use-cases/track-av-playback/track-core-overview.md)
      + Suivi de la lecture principale des médias en flux continu {#track-core}
         + [Suivi de la lecture principale sur JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Suivre la lecture principale sur Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
         + [Suivi de la lecture principale sur Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
      + Suivi de la mise en mémoire tampon {#track-buffering}
         + [Suivi de la mise en mémoire tampon sur JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Effectuer le suivi de la mise en mémoire tampon sur Chromecast](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Effectuer le suivi de la mise en mémoire tampon sur Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
      + Suivi de la recherche {#track-seeking}
         + [Suivi de la recherche sur JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Effectuer le suivi de la recherche sur Chromecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Suivre la recherche sur Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
      + Mise en œuvre de métadonnées standard {#impl-std-metadata}
         + [Mise en œuvre de métadonnées standard sur JavaScript 3.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Mise en œuvre de métadonnées standard sur Chromecast](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Paramètres des métadonnées standard - Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Mise en œuvre de métadonnées standard sur Roku](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Paramètres des métadonnées standard - Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
      + Suivi des publicités {#track-ads}
         + [Aperçu](use-cases/track-ads/track-ads-overview.md)
         + [Suivi des publicités sur JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
         + [Suivre les publicités sur Chromecast](use-cases/track-ads/track-ads-chromecast.md)
         + [Effectuer le suivi des publicités sur Roku](use-cases/track-ads/track-ads-roku.md)
         + Mise en œuvre de métadonnées de publicité standard {#impl-std-ad-metadata}
            + [Mise en œuvre de métadonnées de publicité standard sur JavaScript 3.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
            + [Mise en œuvre de métadonnées de publicité standard sur Roku](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
      + Suivi des chapitres et des segments {#track-chapters}
         + [Aperçu](use-cases/track-chapters/track-chapters-overview.md)
         + [Suivi des chapitres et des segments sur JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
         + [Effectuer le suivi des chapitres et des segments sur Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
         + [Suivi des chapitres et des segments sur Roku](use-cases/track-chapters/track-chapters-roku.md)
      + Suivi de la qualité de l’expérience {#track-qos}
         + [Aperçu](use-cases/track-qos/track-qos-overview.md)
         + [Suivi de la qualité de l’expérience sur JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
         + [Suivre la qualité de l’expérience sur Chromecast](use-cases/track-qos/track-qos-chromecast.md)
         + [Effectuer le suivi de la qualité de l’expérience sur Roku](use-cases/track-qos/track-qos-roku.md)
      + Erreurs de suivi {#track-errors}
         + [Aperçu](use-cases/track-errors/track-errors-overview.md)
         + [Erreurs de suivi sur JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
         + [Erreurs de suivi sur Chromecast](use-cases/track-errors/track-errors-chromecast.md)
         + [Erreurs de suivi sur Roku](use-cases/track-errors/track-errors-roku.md)
+ Confidentialité et sécurité {#streaming-media-privacy}
   + [Paramètres d’opposition et de confidentialité](privacy/opt-out-privacy.md)
   + [Sécurité](privacy/security.md)
+ Mises en œuvre héritées {#legacy-implementations}
   + [Hérité - Aperçu](legacy/setup/legacy-setup-overview.md)
   + [Téléchargement des SDK hérités](legacy/legacy-download-sdks.md)
   + Hérité - SDK Media {#legacy-media-sdks}
      + [Hérité - Présentation des SDK Media](legacy/media-sdk/setup/setup-overview.md)
      + [Configuration d’Android](legacy/media-sdk/setup/set-up-android.md)
      + [Configuration d’iOS](legacy/media-sdk/setup/set-up-ios.md)
      + Configuration de JavaScript {#setup-javascript}
         + [Configurer JavaScript 3.x](legacy/media-sdk/setup/setup-javascript/set-up-js-3.md)
   + [À propos de la mesure de pulsation](legacy/heartbeat-measurement.md)
   + [Adobe Primetime et l’analyse des médias en flux continu](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Activation de Adobe Audience Management](legacy/intro-to-ava/am-enablement.md)
   + [Mise en œuvre d’un lien personnalisé](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + Suivi du jalon hérité {#legacy-milestone-tracking}
      + [Suivi du jalon hérité](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migration de jalon vers VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migration de jalon vers CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Validation {#validation}
      + [Aperçu de la validation](legacy/validation/validation-overview.md)
      + [Test 1 - Lecture standard](legacy/validation/test1-standard-playback.md)
      + [Test 2 - Interruption des médias](legacy/validation/test2-media-interrupt.md)
      + [Détails des appels de test](legacy/validation/test-call-details.md)
      + [Descriptions des paramètres Heartbeat](legacy/validation/heartbeat-params.md)
      + Débogage {#debugging}
         + [Débogage du SDK](legacy/validation/debugging/sdk-debugging.md)
   + [Migration héritée : VHL 1.x vers VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Configuration de JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Comparaison de code v1.x vers v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [API de suivi 1x à 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Hérité - Introduction à AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Chemin côté client](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + Suivi hérité {#track-av-playback}
      + [Effectuer le suivi de la lecture principale sur Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Suivre la lecture principale sur iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Suivi de la lecture principale sur JavaScript {#track-core-javascript}
         + [Suivi de la lecture principale sur JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Effectuer le suivi de la mise en mémoire tampon sur Android](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [Effectuer le suivi de la mise en mémoire tampon sur iOS](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + Suivi de la mise en mémoire tampon sur JavaScript {#track-buffering-js}
            + [Suivi de la mise en mémoire tampon sur JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Effectuer le suivi de la recherche sur Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [Suivre la recherche sur iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + Suivi de la recherche sur JavaScript {#track-seeking-js}
            + [Suivi de la recherche sur JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Mise en œuvre de métadonnées standard sur Android](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Mise en œuvre de métadonnées standard sur iOS](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Clés de métadonnées iOS](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Mise en œuvre de métadonnées standard sur JavaScript {#impl-std-md-js}
            + [Mise en œuvre de métadonnées standard sur JavaScript 2.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + Suivi des publicités {#track-ads}
         + [Effectuer le suivi des publicités sur Android](use-cases/track-ads/track-ads-android.md)
         + [Effectuer le suivi des publicités sur iOS](use-cases/track-ads/track-ads-ios.md)
         + Suivi des publicités sur JavaScript {#track-ads-js}
            + [Suivi des publicités sur JavaScript 2.x](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Mise en œuvre de métadonnées de publicité standard sur Android](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Mise en œuvre de métadonnées de publicité standard sur iOS](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Mise en œuvre de métadonnées de publicité standard sur JavaScript {#impl-std-ad-md-js}
               + [Mise en œuvre de métadonnées de publicité standard sur JavaScript 2.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + Suivi des chapitres et des segments {#track-chapters}
         + [Suivre les chapitres et les segments sur Android](use-cases/track-chapters/track-chapters-android.md)
         + [Effectuer le suivi des chapitres et des segments sur iOS](use-cases/track-chapters/track-chapters-ios.md)
         + Suivi des chapitres et des segments sur JavaScript {#track-chapters-js}
            + [Suivi des chapitres et des segments sur JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Suivre la qualité de l’expérience sur Android](use-cases/track-qos/track-qos-android.md)
         + [Effectuer le suivi de la qualité de l’expérience sur iOS](use-cases/track-qos/track-qos-ios.md)
         + Suivi de la qualité de l’expérience sur JavaScript {#track-qos-js}
            + [Suivi de la qualité de l’expérience sur JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + Erreurs de suivi {#track-errors}
         + [Erreurs de suivi sur Android](use-cases/track-errors/track-errors-android.md)
         + [Erreurs de suivi sur iOS](use-cases/track-errors/track-errors-ios.md)
         + Erreurs de suivi sur JavaScript {#track-errors-js}
            + [Erreurs de suivi sur JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + Scénarios de suivi {#tracking-scenarios}
         + [Lecture VOD sans publicité](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [Lecture VOD avec publicités preroll](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [Lecture VOD avec publicités ignorées](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [Lecture VOD avec un chapitre](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [Lecture VOD avec saut de chapitre](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [Lecture VOD avec recherche dans le contenu principal](use-cases/tracking-scenarios/vod-seeking.md)
         + [Lecture VOD avec mise en mémoire tampon](use-cases/tracking-scenarios/vod-buffering.md)
         + [Plusieurs dispositifs de suivi VOD en parallèle](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [Un dispositif de suivi VOD pour plusieurs sessions](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [Contenu principal en direct ](use-cases/tracking-scenarios/live-main-content.md)
         + [Contenu principal en direct avec suivi séquentiel](use-cases/tracking-scenarios/live-sequential.md)
