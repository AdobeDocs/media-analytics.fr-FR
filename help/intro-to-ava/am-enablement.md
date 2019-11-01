---
title: Activation d’Audience Manager
description: null
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Activation d’Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), une plate-forme de gestion des données (DMP), vous permet de rassembler vos ressources de données d’audience, et ainsi de collecter facilement des informations commercialement pertinentes sur les visiteurs du site, de créer des segments pouvant faire l’objet d’un marketing et de diffuser des publicités et du contenu ciblés auprès de la bonne audience.

Avec AAM, vous n’êtes pas lié à une plate-forme de vendeur de données, d’échange ou côté demande. De plus, AAM est entièrement indépendant par rapport aux ressources de données de vos partenaires. Grâce à l’accès à plusieurs sources de données, AAM offre aux éditeurs numériques la possibilité d’utiliser une grande variété de données tierces et notre Co-op de données privées. Pour en savoir plus sur AAM, consultez la documentation AAM [Documentation du produit Audience Manager.](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**Transfert de données de VA vers AAM :** Pour les publicités vidéo et le contenu vidéo, les mesures et les métadonnées collectées à l’aide de variables de solution (réservées) peuvent être envoyées automatiquement à AAM. Le transfert de données est disponible sur toutes les plates-formes, y compris les plates-formes de bureau, mobiles et OTT. Pour activer ce transfert de données côté serveur, vous devez contacter le service clientèle d’Adobe et demander l’activation de ce flux.

>[!IMPORTANT]
>
>Pour assurer un transfert sans heurt des données vers AAM, vous devez vous trouver sur les dernières versions des bibliothèques du SDK multimédia.

Federated Data prend entièrement en charge le partage de données vers AAM. Demandez à votre équipe Adobe de vous confirmer les paramètres Federated Data.

## Méthodes OTT/AAM {#ott-aam-methods}

Vous pouvez utiliser ces méthodes pour envoyer des signaux et récupérer des segments de visiteurs auprès d’Audience Manager :

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   Renvoie le dernier profil du visiteur obtenu. Renvoie un objet vide si aucun signal n’a encore été envoyé.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   Renvoie le dernier profil du visiteur obtenu. Renvoie un objet vide si aucun signal n’a encore été envoyé.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   Renvoie le DPUUID en cours.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   Définit les DPID et DPUUID. Si les DPID et DPUUID sont définis, ils sont envoyés avec chaque signal.

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   Envoie à la gestion de l’audience par un signal avec des caractéristiques.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   Renvoie le dernier profil du visiteur obtenu. Renvoie un objet vide si aucun signal n’a encore été envoyé.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   Renvoie le dernier profil du visiteur obtenu. Renvoie un objet vide si aucun signal n’a encore été envoyé.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Renvoie le DPUUID en cours.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Définit les DPID et DPUUID. Si les DPID et DPUUID sont définis, ils sont envoyés avec chaque signal.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Envoie à la gestion de l’audience par un signal avec des caractéristiques.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```

