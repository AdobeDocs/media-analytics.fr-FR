---
seo-title: Configuration d’Adobe Debug
title: Configuration d’Adobe Debug
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# Configuration d’Adobe Debug{#configure-adobe-debug}

## Accès à Adobe Debug {#section_AF81E7AD331E41FFA371AB9DA924BFBB}

Pour accéder à Adobe Debug :

1. Go to [Experience Cloud](https://www.marketing.adobe.com) and create a new Adobe Experience Cloud user.

   >[!TIP]
   >
   >Cette connexion n’est pas le même nom d’utilisateur/mot de passe que celui utilisé pour vous connecter à Adobe Analytics.

1. Une fois votre compte Experience Cloud créé, contactez votre représentant Adobe pour demander l’accès à Adobe Debug.
1. After access has been granted, go to [https://debug.adobe.com](https://debug.adobe.com) and use your Experience Cloud credentials to log in.

   ![](assets/adobe-debug-login.png)

   Les navigateurs pris en charge pour cet outil sont les suivants :
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer versions 9 à 11

Les navigateurs recommandés sont les dernières versions de Chrome et Firefox.

## Debug Proxy {#section_8D3493B8426B46DEB9CD7E2ABD785D66}

Téléchargez et configurez le proxy de débogage :

1. Téléchargez l’application Debug Proxy sur la page de [téléchargement des applications.](https://debug.adobe.com/#/downloads)

   Les systèmes d’exploitation pris en charge sont les suivants :
   * OS X 10.7 64 bits ou version supérieure
   * Windows 7.1 64 bits ou version supérieure
   ![](assets/debug-proxy-app.png)

1. Le serveur Debug Proxy s’exécute sur votre ordinateur local sur le port 33284 et est défini comme proxy système.

   Vous devrez peut-être régler le paramètre de votre navigateur en fonction du système d’exploitation et du navigateur.

## Téléchargement et installation du certificat SSL sur le bureau ou les applications {#section_2F9547E301CB413299A67BD59AFBEE0D}

La première fois que vous exécutez Adobe Debug, un certificat SSL unique est généré. Si vous prenez en charge le trafic HTTPS sur les ordinateurs de bureau et/ou les applications, vous devez télécharger et installer notre certificat SSL.

Téléchargez et installez le certificat SSL:

1. After Adobe Debug has been installed and started, go to [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) and download the certification.
1. Importez le certificat

   **Mac OS**
   1. Cliquez deux fois sur le certificat d’autorité de certification racine pour l’ouvrir dans Keychain Access.
   1. Le certificat d’autorité de certification racine apparaît à la connexion.
   1. Déplacez (faites glisser) le certificat d’autorité de certification racine vers Système.
   1. Vous devez copier le certificat vers Système pour vous assurer qu’il est approuvé par tous les utilisateurs et les processus système locaux.
   1. Ouvrez le certificat d’autorité de certification racine, développez Approbation, sélectionnez Toujours approuver et enregistrez vos modifications.
   **Windows**
   1. Procédez de l’une des manières suivantes :

      * [Ajout de certificats au magasin d’autorités de certification racine approuvées pour un ordinateur local](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Pour Firefox, suivez la procédure décrite dans [Installation du certificat racine dans Mozilla Firefox.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    Vous devrez peut-être quitter et rouvrir Firefox pour voir le changement.
    
    **Périphériques iOS**
    1. Définissez votre périphérique iOS pour utiliser Adobe Debug comme proxy HTTP en cliquant sur **[!UICONTROL Settings app]** **&gt;** **[!UICONTROL Wifi settings]**.
    
    1. Dans Safari, accédez à [Débogage].](https://proxy.debug.adobe.com/ssl)
    
    Safari vous invite à installer le certificat SSL.

## Installation du certificat SSL pour votre appareil mobile {#section_F2A3336F482C43E2ABEA742AD5CCACCA}

S’il vous manque les appels HTTPS dans Adobe Debug, vous devez installer le certificat SSL pour Adobe Debug sur l’appareil mobile.

### iOS

Pour installer le certificat SSL sur un appareil iOS :

1. Sur votre ordinateur portable, activez le débogage proxy et accédez à [Adobe Debug.](https://debug.adobe.com)
1. Effectuez les étapes suivantes sur votre appareil iOS :
   1. Mettez votre appareil en mode avion.
   1. Sélectionnez le signal Wi-Fi utilisé par votre ordinateur portable.
   1. Sur votre ordinateur portable, définissez manuellement l’adresse IP et le port affichés dans l’application Debug Proxy.
   1. Ouvrez une fenêtre de navigateur Apple Safari.
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Téléchargez et installez le certificat SSL.

1. Sur votre ordinateur portable, démarrez votre session Adobe Debug.
1. Commencez le test sur votre appareil iOS.

### Android

Pour installer le certificat SSL sur un appareil Android :

1. Sur votre ordinateur portable, activez le proxy de débogage et accédez à [Adobe Debug.](https://debug.adobe.com)
1. Effectuez les étapes suivantes sur votre appareil Android :
   1. Mettez votre appareil en mode avion.
   1. Sélectionnez le signal Wi-Fi utilisé par votre ordinateur portable.
   1. Sur votre ordinateur portable, définissez manuellement l’adresse IP et le port affichés dans l’application Debug Proxy.
   1. Ouvrez une fenêtre de navigateur.
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. Téléchargez et installez le certificat SSL.

1. Sur votre ordinateur portable, démarrez votre session Adobe Debug.
1. Commencez le test sur votre appareil Android.

