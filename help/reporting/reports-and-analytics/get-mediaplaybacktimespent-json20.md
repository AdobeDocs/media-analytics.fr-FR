---
title: Obtention des données de rapport JSON sur le temps de lecture de média avec les API Analytics 2.0
description: Découvrez comment obtenir des données de rapport sur le temps de lecture de média à l’aide des API Analytics 2.0. Affichez un exemple de requête et de réponse.
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: 65e5b67a-26fc-433e-b99b-0ebbc24428ac
source-git-commit: 67f1fa8194fa58b2c513e3136d2bc7880f9cb06b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 100%

---

# Obtention des données de rapport JSON sur le temps de lecture de média avec les API Analytics 2.0{#get-media-playback-time-spent-json-report-data}

Vous pouvez obtenir des données de rapport sur le temps de lecture de média à l’aide des [_*API Analytics 2.0*_](https://www.adobe.io/apis/experiencecloud/analytics/docs.html).

1. Filtrez les données à l’aide de n’importe quel segment généré par l’interface utilisateur. Pour filtrer selon un identifiant de contenu spécifique, créez un segment.
1. Définissez la balise `elements` -> `id` du corps de la requête sur `metrics/playback_time_spent_seconds` ou `metrics/playback_time_spent_minutes` selon la sortie que vous souhaitez obtenir (en secondes ou en minutes).
1. Demandez une quantité suffisante de données.

   * La plage de données que vous spécifiez dans le rapport rassemble toutes les données d’observateurs simultanés _au moment de la fin de la session vidéo._
Vous devez donc tenir compte des sessions qui commencent un jour et se terminent après minuit, c’est-à-dire le lendemain.

   * Demandez un jour de données supplémentaire à la période prévue dans votre requête, mais dans votre analyse _*utilisez uniquement les données prévues.*_

Un exemple de payload de requête pour un jour de données ressemble à l’exemple suivant. La requête est faite pour 2 jours consécutifs mais dans le rapports vous n’utilisez que le premier jour.

## Exemple de requête

```json
{
    "rsid": "[YOUR_RSID]",
    "locale": "en_US",
    "dimension": "variables/daterangeminute",
    "globalFilters": [
        {
            "dateRange": "2021-09-02T00:00/2021-09-03T00:00",
            "type": "dateRange"
        }
    ],
    "metricContainer": {
        "metrics": [
            {
                "columnId": "column1",
                "id": "metrics/playback_time_spent_minutes"
            }
        ]
    },
    "settings": {
        "dimensionSort": "asc",
        "limit": "2000",
        "page": 0
  }
}
```

## Exemple de réponse

```JSON
{
   "totalPages":1,
   "firstPage":true,
   "lastPage":true,
   "numberOfElements":1440,
   "number":0,
   "totalElements":1440,
   "columns":{
      "dimension":{
         "id":"variables/daterangeminute",
         "type":"time"
      },
      "columnIds":[
         "column1"
      ]
   },
   "rows":[
      {
         "itemId":"12008020000",
         "value":"00:00 2021-09-02",
         "data":[
            123.0
         ]
      },
      {
         "itemId":"12008020001",
         "value":"00:01 2021-09-02",
         "data":[
            143.0
         ]
      },
      {
         "itemId":"12008020002",
         "value":"00:02 2021-09-02",
         "data":[
            167.0
         ]
      },

      ...
      {
         "itemId":"12008022359",
         "value":"23:59 2021-09-02",
         "data":[
            768.0
         ]
      }
   ],
   "summaryData":{
      "filteredTotals":[
         17124.0
      ],
      "totals":[
         18453.0
      ]
   }
}
```


<!--
You can extract the Media Playback Time Spent report data using the Experience Cloud API Explorer as follows.

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html)

        * `dateTo` - End date of the report.         

          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`

        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }

      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The Media Playback Time Spent report data, in JSON format, is presented in the Response field.

   For example:

   ![](assets/api_helper_2.png)

   ![](assets/api_helper_1.png)

-->
