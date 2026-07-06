---
title: Paramètres d’opt-out et de confidentialité
description: Découvrez comment gérer lʼinscription, la désinscription et la confidentialité.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: e760701d832fbb4336e9d40d183f6b514f3bf02a
workflow-type: tm+mt
source-wordcount: 798
ht-degree: 3%

---

# Paramètres d’opt-out et de confidentialité

Lorsqu’un utilisateur se désinscrit du suivi, la bibliothèque de médias en flux continu arrête immédiatement toute activité de collecte de données. Aucun appel de démarrage de session, aucun ping de pulsation et aucune donnée de suivi d’événement n’est envoyée aux serveurs de collecte de données Adobe pour cet utilisateur.

## Exclusion/Inclusion

Les contrôles d’opt-out fonctionnent par appareil ou navigateur. Le respect du consentement de l’utilisateur est de la responsabilité de l’organisme chargé de la mise en œuvre. Pour obtenir un aperçu des pratiques de confidentialité d’Adobe, consultez le [Centre de traitement des données personnelles d’Adobe](https://www.adobe.com/fr/privacy.html).

## Types d’implémentation recommandés

>[!BEGINTABS]

>[!TAB SDK Web]

Le SDK Web respecte les préférences de consentement définies à l’aide de la commande `setConsent`. Lorsque le consentement est défini sur `"out"`, Web SDK cesse de transférer tous les événements, y compris les appels de suivi des médias en flux continu, vers Edge Network. L’état de consentement persiste dans l’espace de stockage du navigateur entre les sessions.

Avant d’implémenter la désinscription, assurez-vous que votre SDK web est configurée avec le composant Streaming Media . Pour plus d’informations, voir [Configuration de Web SDK](../implementation/edge/web-sdk.md).

Définissez le consentement sur opt-out à l’aide de la norme de consentement Adobe 2.0 :

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

Valeurs de consentement :

* `"y"` : a accepté (collecte de données autorisée)
* `"n"` : désinscrit (collecte de données supprimée)
* `"p"` : en attente (en attente de la décision de l’utilisateur ; aucune donnée collectée jusqu’à résolution)

Pour restaurer le suivi, appelez de nouveau `setConsent` avec `"y"` comme valeur `collect.val`.

Voir la [commande setConsent](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/setconsent) dans la documentation de Web SDK pour d’autres formats, y compris IAB TCF 2.0.

>[!TAB iOS]

Le SDK mobile Adobe Experience Platform respecte le statut de confidentialité défini à l’aide de `MobileCore.setPrivacyStatus()`. Définir le statut sur `.optedOut` supprime toute collecte de données sur toutes les extensions d’AEP, y compris les médias en flux continu. Le statut persiste entre les sessions d’application.

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

Pour restaurer le suivi, redéfinissez le statut de confidentialité sur `.optedIn` :

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

Pour plus d’informations, voir [Confidentialité et RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) dans la documentation d’AEP Mobile SDK.

>[!TAB Android]

Le SDK mobile Adobe Experience Platform respecte le statut de confidentialité défini à l’aide de `MobileCore.setPrivacyStatus()`. Définir le statut sur `MobilePrivacyStatus.OPT_OUT` supprime toute collecte de données sur toutes les extensions d’AEP, y compris les médias en flux continu. Le statut persiste entre les sessions d’application.

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

Pour restaurer le suivi, redéfinissez le statut de confidentialité sur `MobilePrivacyStatus.OPT_IN` :

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

Pour plus d’informations, voir [Confidentialité et RGPD](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus) dans la documentation d’AEP Mobile SDK.

>[!TAB Roku Edge]

Le SDK Roku Edge utilise `setConsent()` avec la norme de consentement Adobe 2.0. La définition de `collect.val` sur `"n"` arrête immédiatement toute collecte de données, y compris les événements de médias en flux continu.

Valeurs de consentement :

* `"y"` : a accepté (collecte de données autorisée)
* `"n"` : désinscrit (collecte de données supprimée)
* `"p"` : en attente (en attente de la décision de l’utilisateur ; aucune donnée collectée jusqu’à résolution)

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

Pour restaurer le suivi, définissez `collect.val` sur `"y"`, puis appelez à nouveau `setConsent()`.

Vous pouvez également définir une valeur de consentement par défaut lors de l’initialisation de SDK à l’aide de `updateConfiguration()` avec la clé `ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT`. Pour plus d’informations, voir la [documentation de Roku Edge SDK](https://github.com/adobe/aepsdk-roku).

>[!TAB  API Media Edge ]

L’API Media Edge est une mise en œuvre côté serveur. Aucune couche SDK n’applique automatiquement le consentement : votre application doit vérifier le statut de consentement de l’utilisateur avant d’effectuer des appels API et supprimer les requêtes des utilisateurs désinscrits.

Pour l’opt-out complet, ne PUBLIEZ pas sur le point d’entrée `/va/v2/sessions` (ou tout point d’entrée d’événement suivant) pour les utilisateurs qui se sont désinscrits :

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

Pour plus d’informations, voir [Référence de l’API Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

>[!ENDTABS]

## Types d’implémentation hérités (Analytics uniquement)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

La bibliothèque Media SDK JS 3.x fait référence à l’état d’opt-out de l’API visiteur Adobe (Service d’identités). Lorsqu’un utilisateur se désinscrit à l’aide de l’API visiteur, Media SDK supprime automatiquement tous les appels de suivi.

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

Remplacez `YOUR_ORG_ID@AdobeOrg` par l’ID d’organisation de Adobe Admin Console.

Pour restaurer le suivi, transmettez les `false` à `setOptOut()`.

Pour plus d’informations, voir [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).

>[!TAB  Chromecast ]

Chromecast Media SDK 3.x respecte le statut de confidentialité défini à l’aide de `ADBMobile.config.setPrivacyStatus()`. Définir le statut sur `PRIVACY_STATUS_OPT_OUT` supprime toute la collecte de données.

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

Pour restaurer le suivi, redéfinissez le statut sur opt-in :

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

Vous pouvez également définir le statut de confidentialité par défaut à l’initialisation de SDK dans votre objet `ADBMobileConfig` :

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB Roku 2.x]

Le SDK Roku 2.x respecte le statut de confidentialité défini à l’aide de `setPrivacyStatus`. Définir le statut sur `PRIVACY_STATUS_OPT_OUT` supprime toute la collecte de données.

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_OUT)
```

Pour restaurer le suivi, redéfinissez le statut sur opt-in :

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_IN)
```

Vous pouvez également définir le statut de confidentialité par défaut à l’initialisation de SDK dans votre fichier `ADBMobileConfig.json` :

```json
"analytics": {
  "privacyDefault": "optedout"
}
```

>[!TAB  API Media Collection ]

L’API Media Collection est une implémentation côté serveur. Votre application doit vérifier le statut de consentement de l’utilisateur avant d’effectuer des appels API et supprimer les requêtes des utilisateurs désinscrits.

Pour l’opt-out complet, ne PUBLIEZ pas sur le point d’entrée des sessions pour les utilisateurs qui se sont désinscrits.

Pour les opt-outs partiels dans le cadre du CCPA, incluez des indicateurs d&#39;opt-out dans l&#39;objet `params` de votre demande d&#39;`sessionStart` :

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding` : définissez cette valeur sur `true` pour exclure les données partagées entre Adobe Analytics et d’autres solutions Experience Cloud (telles qu’Audience Manager).
* `analytics.optOutShare` : définissez cette valeur sur `true` pour vous exclure du partage de données fédérées avec d’autres clients Adobe Analytics.

Pour obtenir la liste complète des paramètres disponibles, reportez-vous à la référence des paramètres de requête de l’API [Media Collection](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md).

>[!ENDTABS]

