---
title: Configuration d’Adobe Debug
description: « Découvrez commet configurer Adobe Debug, que vous pouvez utiliser pour résoudre les problèmes de mise en œuvre du SDK Media. »
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
exl-id: 48ad3f23-f36d-44f3-b8d9-b0b3a2ee06bc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 41023be25308092a1b3e7c40bad2d8085429a0bc
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 100%

---

# Configuration d’Adobe Debug{#configure-adobe-debug}

## Accès à Adobe Debug {#accessing-adobe-debug}

Pour accéder à Adobe Debug :

1. Accédez à [Experience Cloud](https://www.marketing.adobe.com/) et créez un nouvel utilisateur Adobe Experience Cloud.

   >[!TIP]
   >
   >Cette connexion est différente du nom d’utilisateur/mot de passe que vous utilisez pour vous connecter à Adobe Analytics.

1. Une fois votre compte Experience Cloud créé, contactez votre représentant Adobe pour demander l’accès à Adobe Debug.
1. Une fois l’accès accordé, accédez à [https://debug.adobe.com](https://debug.adobe.com) et utilisez les informations d’identification d’Experience Cloud pour vous connecter.

   ![](assets/adobe-debug-login.png)

   Les navigateurs pris en charge pour cet outil sont les suivants :
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versions 9 à 11

Les navigateurs recommandés sont les dernières versions de Chrome et Firefox.

## Debug Proxy {#debug-proxy}

Télécharger et configurer Debug Proxy :

1. Téléchargez l’application Debug Proxy sur la page de [téléchargement des applications](https://debug.adobe.com/#/downloads).

   Les systèmes d’exploitation pris en charge sont les suivants :
   * OS X 10.7 64 bits ou version ultérieure
   * Windows 7.1 64 bits ou version ultérieure

   ![](assets/debug-proxy-app.png)

1. Le serveur Debug Proxy s’exécute sur votre ordinateur local sur le port 33284 et est défini comme proxy système.

   Vous devrez peut-être régler le paramètre de votre navigateur en fonction du système d’exploitation et du navigateur.

## Téléchargement et installation du certificat SSL sur le bureau ou les applications {#download-and-install-sSL-desktop}

La première fois que vous exécutez Adobe Debug, un certificat SSL unique est généré. Si vous prenez en charge le trafic HTTPS sur les ordinateurs de bureau et/ou les applications, vous devez télécharger et installer notre certificat SSL.

Téléchargez et installez le certificat SSL :

1. Après avoir installé et démarré Adobe Debug, accédez à [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) et téléchargez la certification.
1. Importez le certificat

   **Mac OS**
   1. Double-cliquez sur le certificat d’autorité de certification racine pour l’ouvrir dans Keychain Access.
   1. Le certificat d’autorité de certification racine apparaît à la connexion.
   1. Déplacez (faites glisser) le certificat d’autorité de certification racine vers Système.
   1. Vous devez copier le certificat dans le système pour vous assurer qu’il est approuvé par tous les utilisateurs et par les processus système locaux.
   1. Ouvrez le certificat d’autorité de certification racine, développez Approbation, sélectionnez Toujours approuver et enregistrez vos modifications.

   **Windows**
   1. Procédez de l’une des manières suivantes :

      * [Ajout de certificats au magasin des autorités de certification racine approuvées pour un ordinateur local](https://technet.microsoft.com/fr-fr/library/cc754841.aspx#BKMK_addlocal)
   1. Pour Firefox, exécutez la procédure décrite dans [Installation d’un certificat racine dans Mozilla Firefox](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox).

      Vous devrez peut-être fermer et rouvrir Firefox pour voir la modification.
   **Appareils iOS**
   1. Configurez votre appareil iOS pour qu’il utilise Adobe Debug comme proxy HTTP en cliquant sur **[!UICONTROL Paramètres d’application]** **>** **[!UICONTROL Paramètres Wi-Fi]**.

   1. Dans Safari, accédez à [Débogage](https://proxy.debug.adobe.com/ssl).

      Safari vous invite à installer le certificat SSL.




## Installation du certificat SSL pour votre appareil mobile {#install-sSL-for-mobile-device}

S’il vous manque les appels HTTPS dans Adobe Debug, vous devez installer le certificat SSL pour Adobe Debug sur l’appareil mobile.

### iOS

Pour installer le certificat SSL sur un appareil iOS :

1. Sur votre ordinateur portable, activez le débogage proxy et accédez à [Adobe Debug](https://debug.adobe.com).
1. Effectuez les étapes suivantes sur votre appareil iOS :
   1. Mettez votre appareil en mode avion.
   1. Sélectionnez le signal Wi-Fi utilisé par votre ordinateur portable.
   1. Sur votre ordinateur portable, définissez manuellement l’adresse IP et le port affichés sur l’application Debug Proxy.
   1. Ouvrez une fenêtre de navigateur Apple Safari.
   1. Accédez à [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl).
   1. Téléchargez et installez le certificat SSL.

1. Sur votre ordinateur portable, démarrez votre session Adobe Debug.
1. Commencez le test sur votre appareil iOS.

### Android

Pour installer le certificat SSL sur un appareil Android :

1. Sur votre ordinateur portable, activez le proxy de débogage et accédez à [Adobe Debug](https://debug.adobe.com).
1. Effectuez les étapes suivantes sur votre appareil Android :
   1. Mettez votre appareil en mode avion.
   1. Sélectionnez le signal Wi-Fi utilisé par votre ordinateur portable.
   1. Sur votre ordinateur portable, définissez manuellement l’adresse IP et le port affichés sur l’application Debug Proxy.
   1. Ouvrez une fenêtre du navigateur.
   1. Accédez à [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl).
   1. Téléchargez et installez le certificat SSL.

1. Sur votre ordinateur portable, démarrez votre session Adobe Debug.
1. Commencez le test sur votre appareil Android.
