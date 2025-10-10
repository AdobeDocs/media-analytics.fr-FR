---
title: Chargement des données de planning pour suivre le contenu en direct
description: Découvrez comment charger des données de planning pour suivre le contenu en direct.
feature: Streaming Media
role: User, Admin, Data Engineer
hide: true
hidefromtoc: true
exl-id: 875c4513-ea4e-4c5f-bfc1-34ea175007ca
source-git-commit: b947a1d64c7fa58e784712397b0167d4186d00c3
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 2%

---

# Chargement des données de planning pour suivre le contenu en direct

Vous pouvez charger les données de planning du contenu multimédia en direct précédent pour suivre plus facilement et plus précisément l’audience du contenu en direct. Vous pouvez effectuer le suivi de l’audience pour des programmes individuels et même des sujets ou des segments de programme spécifiques.

Les éléments suivants sont des exemples de contenu en direct qui sont pris en charge avec le chargement de données de planning :

* Plateformes FAST (Free Ad Supported TV)

* Flux locaux

* Sports en direct

* Programmation d&#39;actualités ou thématiques

## Fonctionnalités

Diverses fonctionnalités sont disponibles lors de l’utilisation de la planification des chargements de données du contenu Streaming Media en direct précédent. Cette section décrit certaines des fonctionnalités clés qui permettent d’analyser les performances du programme.

Ces fonctionnalités sont disponibles quelle que soit la manière dont vous avez mis en œuvre Streaming Media Collection.

* **Suivre précisément les plannings de programme** : Identifiez les heures de début et de fin de chaque programme individuel dans le flux en direct pour la période que vous souhaitez analyser. Avec des heures de début et de fin précises, l’heure d’exécution précise est reflétée avec précision et peut être analysée par rapport à chaque session de visionneuse.

  Par exemple, les heures précises de début et de fin ne sont pas toujours connues pour un événement sportif en direct jusqu’à ce que l’événement soit terminé. Planifier les chargements de données vous permet d’obtenir des rapports précis en mettant à jour les heures de début et de fin une fois le programme terminé.

* **Suivre des sujets individuels ou des segments de programme** : créez des dimensions temporelles pour des sujets spécifiques ou des segments de programme (intervalles de temps) au sein d’un programme donné. Ces dimensions temporelles vous permettent d’analyser l’audience d’un programme à un niveau plus spécifique, ce qui vous aide à recueillir des informations sur les sujets ou les segments de programme qui ont le mieux résonné.

  Par exemple, lors de l’analyse d’un événement sportif en direct, tel qu’un match de football, vous pouvez créer des dimensions distinctes pour la première moitié, la moitié et la seconde moitié. Le suivi de rubriques ou de segments spécifiques au sein d’un programme permet ainsi des répartitions plus détaillées du comportement des visionneuses.

* **Créer des parcours d’utilisateur dans Journey Optimizer** : suivez les programmes qu’une personne a consultés au cours d’une session donnée (ou même les rubriques ou segments de programme qu’elle a consultés), puis utilisez ces données dans Adobe Journey Optimizer pour créer des parcours d’utilisateur pour les clients qui ont visionné un certain programme ou qui se sont montrés intéressés par une rubrique spécifique.

## Comprendre le fonctionnement des données de planning pour Streaming Media

La fonctionnalité de planification des données pour Streaming Media fonctionne de la manière suivante :

1. Lit le jeu de données du programme de planification pour les enregistrements du programme de planification, en filtrant par la date de la planification.

   Ne fonctionne que pour les programmes qui ont eu lieu de 24 à 48 heures dans le passé.

2. Lit les événements de fermeture de média à partir du jeu de données de média, en filtrant par date et par chemin XDM dans les enregistrements de programme de planning.

3. Pour chaque événement de fermeture de média, le même nombre d’événements de début de planning média est généré, car des programmes se chevauchaient avec la session multimédia.

   Chaque événement de début de planning multimédia contient le nom et la durée du planning.

   En outre, une nouvelle mesure de temps appelée **scheduleTimePlayed** contient le nombre de secondes pendant lesquelles la session multimédia a chevauché le programme planifié. L’horodatage de l’événement de début du planning correspond à l’horodatage du début de l’émission.

4. Écrit les nouveaux événements de début de planning dans le jeu de données de médias AEP.

## Conditions préalables

Pour charger les données de planning du contenu actif précédent, votre environnement Streaming Media doit respecter les conditions préalables suivantes :

* La collecte de médias en flux continu doit être activée pour le suivi du contenu pour lequel vous souhaitez charger des données de planning, comme décrit dans la section [Présentation du suivi](/help/use-cases/track-av-playback/track-core-overview.md). <!--specifics??? -->

* Utilisez Streaming Media Collection avec Customer Journey Analytics. Adobe Analytics ne permet pas de charger des données de planning.

## Création d’un jeu de données de planning de programme dans AEP

Avant de pouvoir transmettre les informations de planning, vous devez créer un jeu de données de planning de programme dans Experience Platform :

1. Créez un schéma basé sur la classe XDM **Programme planifié Media Analytics**.

   ![Schéma du programme de planification de Media Analytics](assets/media_schedule_finish_schema_creation.png)

   Il s’agit de la définition XDM de la classe de programme planifié Media Analytics.

   [https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. Créez un jeu de données en fonction du schéma que vous avez créé.

1. Passez à la section suivante, [Informations sur le planning des notifications push](#push-schedule-information).

## Informations sur le planning des notifications push

Après avoir [créé un jeu de données de planning de programme](#create-a-program-schedule-dataset-in-aep), vous pouvez transmettre les informations de planning :

1. Créez un fichier .json avec les informations de planification.

   Le fichier .json doit contenir un tableau d’objets de programme de planification, conformément au schéma XDM.

1. Téléchargez le fichier .json :

   >[!NOTE]
   >
   >Les exemples de cURL de cette section utilisent les variables suivantes :
   >
   >* Pour l’authentification avec Adobe Developer :
   >     * CUSTOMER_API_KEY
   >     * AUTH_TOKEN
   >* identifiant de l’organisation : CUSTOMER_ORG_ID
   >* ID du jeu de données d’enregistrement créé dans la configuration : DATASET_ID
   >* batch_ID créé lors de la première demande utilisée lors du chargement du fichier : BATCH_ID
   >* Nom du fichier utilisé pour les enregistrements push : FILE_NAME

   1. Créez un lot, puis obtenez l’identifiant du lot à partir de la réponse.

      Prenons l’exemple suivant d’utilisation de cURL pour créer un lot AEP :

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. Envoyez le fichier .json contenant les enregistrements de données de planning du programme à l’aide de l’ID de lot.

      Pour transmettre les informations de planification par push, vous devez utiliser les API Batch d’AEP, comme décrit dans la section [Présentation de l’API Batch Ingestion](https://experienceleague.adobe.com/fr/docs/experience-platform/ingestion/batch/overview).

      Prenons l’exemple suivant d’utilisation de cURL pour transmettre un fichier avec les enregistrements de planning :

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. Terminez le lot.

      Examinons l’exemple suivant d’utilisation de cURL pour terminer le lot :

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. Passez à la section suivante, [Enregistrer un ticket d’assistance auprès de l’assistance clientèle d’Adobe](#log-a-support-ticket-with-adobe-customer-care).

## Enregistrez un ticket d’assistance auprès de l’assistance clientèle Adobe

Enregistrez un ticket d’assistance auprès de l’assistance clientèle d’Adobe avec les informations suivantes :

* **Jeu de données multimédia** : spécifiez l’identifiant du jeu de données à partir duquel les données des sessions multimédia sont lues.

* **Jeu de données de planification** : spécifiez l’identifiant du jeu de données vers lequel les enregistrements de planification sont transmis.

* **Jeu de données de média de sortie** : spécifiez l’identifiant du jeu de données dans lequel les événements de début de planning sont enregistrés.

  Cet identifiant de jeu de données peut être le même que celui utilisé pour le jeu de données Media. S’il s’agit d’un identifiant de jeu de données différent, il doit toujours avoir le même schéma XDM que le jeu de données multimédia.

* **Identifiant de l’organisation** : indiquez l’identifiant de votre organisation.

## Exemple de fichier .json de planning avec deux enregistrements

L’exemple suivant illustre un fichier .json planifié avec deux enregistrements. Chaque fichier .json doit contenir tous les programmes planifiés d’une journée.

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### Comprenez les champs de programme de planification dans l’exemple

1. **mediaProgramDetails** : doit contenir les informations minimales requises pour créer l’événement de début de planning :
   * **startTimestamp** : l’heure de début de l’émission.
   * **name** : nom convivial du programme.
   * **length** : nombre de secondes pendant lesquelles l’affichage a duré.

     >[!IMPORTANT]
     >
     >Si vous avez plusieurs demandes de données de planification, les heures de début et de fin ne peuvent pas se chevaucher.

1. **scheduleDate** : date de diffusion de l’émission. Le format doit être AAAA-MM-JJ. Il est utilisé pour filtrer le jeu de données de planification et obtenir toutes les planifications pour lesquelles Adobe crée des démarrages de planification.
1. **scheduleFilter** : utilisé pour filtrer tous les événements de fermeture de session multimédia.
   * **filterPath** : un chemin XDM vers le champ utilisé pour le filtrage.
   * **filterValue** : valeur utilisée pour le filtrage.
1. **customMetadata** : métadonnées personnalisées que vous souhaitez ajouter aux événements de démarrage du planning. Ces métadonnées sont utilisées pour remplacer les métadonnées personnalisées présentes dans les événements de fermeture de session.
1. **defaultMetadata** : liste spécifique des dimensions pouvant ajouter ou remplacer les métadonnées par défaut présentes sur les appels de fermeture du média.

   Examinons les exemples de dimensions suivants que vous pouvez créer et sur lesquels vous pouvez créer des rapports dans Customer Journey Analytics :

   * **[»_Nom de l’épisode_ »](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)** : cette dimension peut vous aider à identifier les épisodes d’une série particulière qui ont les meilleures performances.

   * **[ID de ressource](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. Continuez avec [&#x200B; Analyser les données dans Customer Journey Analytics &#x200B;](#analyze-data-in-customer-journey-analytics).

## Analyse des données dans Customer Journey Analytics

Dans la journée qui suit le chargement de votre fichier de données comme décrit dans [Demande et chargement du fichier de données de planning](#request-and-upload-the-schedule-data-file), vos données sont prêtes à faire l’objet d’un rapport dans Customer Journey Analytics.

Pour créer des rapports sur vos données Streaming Media en direct passées dans Customer Journey Analytics :

1. Créez un projet ou ouvrez un projet existant.

1. Créez le projet en créant les tableaux ou visualisations dont vous avez besoin pour analyser vos données passées de médias en flux continu en direct.

   Lors de la création du projet, utilisez les informations que vous avez incluses dans le fichier de données de planning et envoyées à l’assistance clientèle d’Adobe. Cela inclut la clé correspondante, les dimensions et toute métadonnée supplémentaire. Pour plus d’informations, voir [Demander et charger le fichier de données de planning](#request-and-upload-the-schedule-data-file).




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->
