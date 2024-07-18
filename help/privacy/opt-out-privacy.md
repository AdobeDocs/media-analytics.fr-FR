---
title: Explication de l’exclusion et de la confidentialité
description: Découvrez comment gérer lʼinscription, la désinscription et la confidentialité.
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c00c9850d5ea924cef6b4842ecb770df1e78eb21
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 94%

---

# Exclusion et confidentialité {#opt-out-and-privacy}

## Exclusion/Inclusion {#opt-out-opt-in}

Vous pouvez décider d’autoriser ou non l’activité de suivi sur un appareil spécifique :

* **Applications mobiles –** Les extensions Media respectent les paramètres de confidentialité de la collecte de données. Pour exclure le suivi, vous devez configurer la confidentialité sur [Exclusion dans les balises](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/#create-a-mobile-property) ou [Mise à jour du statut de confidentialité dans le SDK Mobile](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#getprivacystatus).
* **Applications JavaScript/de navigateur -** La bibliothèque VA respecte les paramètres de confidentialité et d’exclusion de `VisitorAPI`. Pour exclure le suivi, assurez-vous de procéder à l’exclusion depuis le service Visitor API. Pour plus d’informations sur l’exclusion et la confidentialité, voir [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).
* **Applications OTT (Chromecast, Roku) -** Les SDK OTT fournissent des API conformes au Règlement général sur la protection des données (RGPD) qui vous permettent de définir des indicateurs d’état `opt` pour la collecte et la transmission de données, ainsi que de récupérer des identités stockées localement.

  >[!NOTE]
  >
  >Les appels de suivi de la pulsation multimédia sont également désactivés si l’état de confidentialité est défini sur exclusion.

  Vous pouvez déterminer si les données Analytics sont envoyées ou non sur un appareil spécifique à l’aide des paramètres suivants :

   * Paramètre `privacyDefault` du fichier de configuration `ADBMobile.json`. Cela contrôle le paramètre initial qui persiste jusqu’à ce qu’il soit modifié dans le code.

   * La méthode `ADBMobile().setPrivacyStatus()`.

      * **Exclusion :**

         * **Chromecast :**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
           ```

         * **Roku :**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
           ```

        >[!IMPORTANT]
        >
        >Lorsqu’un utilisateur exclut le suivi, tous les identifiants et données d’appareil conservés sont purgés jusqu’à ce que l’utilisateur procède à nouveau à l’inclusion.

      * **Inclusion :**

         * **Chromecast :**

           ```
           ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
           ```

         * **Roku :**

           ```
           ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
           ```

      * **Renvoyer le paramètre actuel :**

         * **Chromecast :**

           ```
           ADBMobile.config.getPrivacyStatus()
           ```

         * **Roku :**

           ```
           ADBMobile().getPrivacyStatus()
           ```

  Une fois le paramètre de confidentialité modifié à l’aide de `setPrivacyStatus`, le changement est permanent jusqu’à ce qu’il soit modifié à nouveau en utilisant cette méthode, ou jusqu’à la désinstallation et la réinstallation de l’application.

## Récupération des identifiants stockés (applications OTT) {#retrieving-stored-identifiers-ott-apps}

Ces informations vous aident à récupérer les identités d’utilisateurs stockées localement depuis votre application Roku.

>[!IMPORTANT]
>
>La méthode de récupération de tous les identifiants permet d’obtenir toutes les identités d’utilisateurs connues et conservées par le kit SDK. Vous devez l’invoquer **avant** que l’utilisateur ne se désinscrive.

Les identités stockées localement sont renvoyées dans une chaîne JSON, qui peut contenir :

* Contexte de l’entreprise - ID d’organisation IMS
* Identifiants d’utilisateurs
* Experience Cloud ID (MCID)
* ID de source de données (DPID, DPUUID)
* Analytics ID (AVID, AID, VID et RSID associés)
* Audience Manager ID (UUID)

Par exemple :

* **Chromecast :**

  ```
  ADBMobile.config.getAllIdentifiersAsync(callback)
  ```

* **Roku :**

  ```
  vids = ADBMobile().getAllIdentifiers()
  ```
