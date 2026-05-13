---
title: API Streaming Media Collection - Démarrage rapide
description: Prise en main de l’API Streaming Media. Découvrez comment vérifier rapidement vos données de requête.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/F7NHDQkJVwVc-Th-blxBP8gifT7V55xLqlI1YT-pswc
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 294
ht-degree: 90%

---

# Démarrage rapide{#quick-start}

>[!TIP]
>
>Rassemblez les données de demande nécessaires pour terminer une [requête sessions](../mc-api-ref/mc-api-sessions-req.md) sur le serveur principal de l’API Collection de Media Analytics (MA). Vous pouvez vérifier rapidement vos données de requête en envoyant les requêtes manuellement (avec `curl`, Postman, etc.). Vous obtenez ainsi un feedback immédiat indiquant l’existence ou non de problèmes de types de données incorrects ou d’informations incorrectes dans votre requête. Utilisez les [schémas de validation JSON](../mc-api-ref/mc-api-json-validation.md) pour vérifier que vous fournissez des données de requêtes correctes.

1. Rassemblez les données Adobe Analytics et de visiteur standard que vous devez fournir pour exécuter l’une des applications Experience Cloud :

   * Identifiant d’entreprise Experience Cloud du visiteur
   * Identifiant utilisateur Experience Cloud du visiteur
   * Identifiant de suite de rapports Analytics
   * URL du serveur de suivi Analytics

1. Créez un objet JSON pour le corps de votre requête `sessions`, contenant les données minimales requises pour un appel réussi. Par exemple :

   ```json
   {
       "playerTime": {
           "playhead": 0,
           "ts": 1234560890123
       },
       "eventType": "sessionStart",
       "params": {
           "media.playerName": "sample-html5-api-player",
           "analytics.trackingServer": "[YOUR_TS]",
           "analytics.reportSuite": "[YOUR_RSID]",
           "media.contentType": "VOD",
           "media.length": 60.39333333333333,
           "media.id": "MA Collection API Sample Player",
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]",
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe",
           "media.channel": "sample-channel",
           "media.sdkVersion": "va-api-0.0.0",
           "analytics.enableSSL": false
       }
   }
   ```

   >[!NOTE]
   >
   >Vous devez utiliser les types de données corrects dans le corps de la requête JSON. Par exemple, `analytics.enableSSL` nécessite une valeur booléenne, `media.length` est numérique, etc. Vous pouvez vérifier les types de paramètre et les exigences obligatoires ou facultatives en cochant la case [Schémas de validation JSON.](mc-api-validate-reqs.md)

1. Envoyez des requêtes sessions au point d’entrée d’API MA Collection. Si la charge utile de votre requête n’est pas valide, identifiez le problème et réessayez jusqu’à obtention d’une réponse `201 Created`. Dans cet exemple `curl`, le corps de la requête JSON se trouve dans un fichier nommé `sample_data_session` :

   ```sh
   $ curl -i -d \
     @sample_data_session https://{uri}/api/v1/sessions \
     > curl.sessions.out
   
   $ cat curl.sessions.out
   HTTP/1.1 201 Created
   Server: nginx/1.13.5
   Date: Mon, 18 Dec 2017 22:34:12 GMT
   Content-Type: application/octet-stream
   Content-Length: 0
   Connection: keep-alive
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: *
   Access-Control-Allow-Methods: OPTIONS,POST,PUT
   Access-Control-Allow-Headers: Content-Type
   Access-Control-Expose-Headers: Location
   ```

Si la [requête sessions](../mc-api-ref/mc-api-sessions-req.md) réussit, vous recevez une réponse `201 Created` similaire à la réponse ci-dessus. La réponse comprend un ID de session dans l’en-tête Emplacement. L’ID de session est la donnée essentielle de la réponse, car il est nécessaire pour tous les appels de suivi suivants. Après un retour réussi d’une [requête sessions](../mc-api-ref/mc-api-sessions-req.md), vous pouvez passer en toute confiance à la mise en œuvre du suivi vidéo en utilisant l’API MA dans votre lecteur vidéo.
