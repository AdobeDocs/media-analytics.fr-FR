---
seo-title: Exclusion et confidentialité
title: Exclusion et confidentialité
uuid: 7 e 60 c 7 bd -8 dba -4 c 7 a -9 c 3 c -0 c 634 b 815397
translation-type: tm+mt
source-git-commit: 80208f1c4773857f7907be0b8566c55a03e6106c

---


# Exclusion et confidentialité{#opt-out-and-privacy}

## Exclusion/Inclusion {#section_zfb_syq_v2b}

Vous pouvez décider d’autoriser ou non l’activité de suivi sur un appareil spécifique :

* **Applications mobiles -** La bibliothèque VA respecte les paramètres de confidentialité et d’exclusion de la bibliothèque `AdobeMobile`. Pour exclure le suivi, vous devez utiliser la bibliothèque `AdobeMobile`. Pour en savoir plus sur les paramètres d’exclusion et de confidentialité de la bibliothèque `AdobeMobile`, consultez la rubrique [Paramètres d’exclusion et de confidentialité](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html).
* **Applications JavaScript/de navigateur -** La bibliothèque VA respecte les paramètres de confidentialité et d’exclusion de `VisitorAPI`. Pour exclure le suivi, assurez-vous de procéder à l’exclusion depuis le service Visitor API. For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **Applications OTT (Chromecast, Roku) :** les SDK OTT fournissent des API GDPR (General Data Protection Regulation) qui permettent de définir des indicateurs `opt` d'état pour la collecte et la transmission des données et pour récupérer les identités stockées localement.

   >[!NOTE]
   >
   >Les appels de suivi de pulsation multimédia sont également désactivés si l'état de confidentialité est défini pour s'exclure.

   Vous pouvez déterminer si les données Analytics sont envoyées ou non sur un appareil spécifique à l’aide des paramètres suivants :

   * `privacyDefault` Paramètre du fichier `ADBMobile.json` de configuration. Cela contrôle le paramètre initial qui persiste jusqu’à ce qu’il soit modifié dans le code.

   * `ADBMobile().setPrivacyStatus()` Méthode.

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
         >Lorsqu'un utilisateur choisit de ne pas effectuer le suivi, toutes les données et tous les ID persistants sont purgés jusqu'à ce que l'utilisateur y retourne.

      * **Inclusion :**

         * **Chromecast :**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku :**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **Renvoi du paramètre actuel :**

         * **Chromecast :**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku :**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   Une fois le paramètre de confidentialité modifié à l’aide de `setPrivacyStatus`, le changement est permanent jusqu’à ce qu’il soit modifié à nouveau en utilisant cette méthode, ou jusqu’à la désinstallation et la réinstallation de l’application.

## Récupération des identifiants stockés (applications OTT) {#section_mky_2yq_v2b}

Ces informations vous aident à récupérer les identités d’utilisateurs stockées localement depuis votre application Roku.

>[!IMPORTANT]
>
>La méthode de récupération de tous les identifiants obtient toutes les identités utilisateur connues et conservées par le SDK. Vous devez l’invoquer **avant** que l’utilisateur ne se désinscrive.

Les identités stockées localement sont renvoyées dans une chaîne JSON, qui peut contenir :

* Contexte de la société – ID d’organisation IMS
* Identifiants d’utilisateurs
* Experience Cloud ID (MCID)
* ID de sources de données (DPID, DPUUID)
* Analytics ID (AVID, AID, VID et RSID associés)
* Audience Manager ID (UUID)

Par exemple :

* **Chromecast :**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku :**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

