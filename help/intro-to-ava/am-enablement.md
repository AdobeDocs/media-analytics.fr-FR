---
title: Qu’est-ce que l’activation d’Adobe Audience Manager ?
description: Apprenez à lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
translation-type: ht
source-git-commit: 7ad0c85108e6d3800dce0fcf91175fd5eb4526e7
workflow-type: ht
source-wordcount: '409'
ht-degree: 100%

---

# Activation d’Audience Manager {#audience-manager-enablement}

Adobe Audience Manager (AAM), une plateforme de gestion des données (DMP), vous permet de rassembler vos ressources de données d’audience, et ainsi de collecter facilement des informations commercialement pertinentes sur les visiteurs du site, de créer des segments pouvant faire l’objet d’un marketing et de diffuser des publicités et du contenu ciblés auprès de la bonne audience.

Avec AAM, vous n’êtes pas lié à une plateforme de vendeur de données, d’échange ou côté demande. De plus, AAM est entièrement indépendant par rapport aux ressources de données de vos partenaires. Grâce à l’accès à plusieurs sources de données, AAM offre aux éditeurs numériques la possibilité d’utiliser une grande variété de données tierces et notre Co-op de données privées. Pour en savoir plus sur AAM, consultez la documentation AAM [Documentation du produit Audience Manager.](https://docs.adobe.com/content/help/fr-FR/audience-manager/user-guide/aam-home.html)

**Transfert de données de VA vers AAM** - Pour les publicités vidéo et le contenu vidéo, les mesures et les métadonnées collectées à l’aide de variables de solution (réservées) peuvent être envoyées automatiquement à AAM. Le transfert de données est disponible sur toutes les plateformes, y compris les plateformes de bureau, mobiles et OTT. Pour activer ce transfert de données côté serveur, vous devez contacter le service clientèle d’Adobe et demander l’activation de ce flux.

>[!IMPORTANT]
>
>Pour assurer le transfert harmonieux des données vers AAM, vous devez utiliser les dernières versions des bibliothèques SDK Media.

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

   Définit les DPID et DPUUID. Si les DPID et DPUUID sont définis, ils seront envoyés avec chaque signal.

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

   Renvoie le dernier profil du visiteur obtenu. Renvoie un objet vide à si aucun signal n’a encore été envoyé.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   Renvoie le DPUUID en cours.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   Définit les DPID et DPUUID. Si les DPID et DPUUID sont définis, ils seront envoyés avec chaque signal.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   Envoie à la gestion de l’audience par un signal avec des caractéristiques.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```
