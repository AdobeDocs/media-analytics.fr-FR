---
title: Obtention des données du rapport JSON sur les visionneuses simultanées
description: null
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Obtention des données du rapport JSON sur les visionneuses simultanées {#get-concurrent-viewers-json-report-data}

Vous pouvez obtenir des données de rapport des visionneuses simultanées à l’aide de la _*version 1.4*_ des API Analytics :
* [Interfaces API Analytics](https://github.com/AdobeDocs/analytics-1.4-apis)
* [Swagger](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. Filtrez les données à l’aide de n’importe quel segment généré par l’interface utilisateur. Pour filtrer selon un identifiant de contenu spécifique, créez un segment.
1. Définissez le `elements` -> `id` dans le corps de requête sur `videoconcurrentviewers`.
1. Demandez une quantité suffisante de données. Adobe recommande 3 200 points de données pour s’assurer qu’il n’y a pas d’écart entre les données.

   * La plage de données que vous spécifiez dans le rapport rassemble toutes les données de visionneuse simultanées _au moment de la fin de la session vidéo._
Vous devez donc tenir compte des sessions qui commencent un jour et se terminent après minuit (c.-à-d. le lendemain).

   * Demandez plusieurs jours de données, mais dans votre analyse, _*utilisez uniquement le premier jour des données.*_

Voici un exemple de charge utile de requête pour ce scénario :

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
  }
}
```

<!--
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows. 

1. Navigate to: [https://www.adobe.io.](https://www.adobe.io)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/report-suites-admin.html)
        
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

   The concurrent viewers report data, in JSON format, is presented in the Response field.
   
   For example:
   
   ![](assets/api_helper_2.png) 

   ![](assets/api_helper_1.png)

-->
