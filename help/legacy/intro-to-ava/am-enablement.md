---
title: Qu’est-ce que l’activation d’Adobe Audience Manager ?
description: Apprenez à lier les actions d’application aux données de suivi multimédia sans avoir besoin de règles de traitement supplémentaires ni de variables personnalisées.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# Activation d’Audience Manager{#audience-manager-enablement}

Adobe Audience Manager (AAM), une plateforme de gestion des données (DMP), vous permet de rassembler vos ressources de données d’audience, et ainsi de collecter facilement des informations commercialement pertinentes sur les visiteurs du site, de créer des segments pouvant faire l’objet d’un marketing et de diffuser des publicités et du contenu ciblés auprès de la bonne audience.

Avec AAM, vous n’êtes pas lié à une plateforme de vendeur de données, d’échange ou côté demande. De plus, AAM est entièrement indépendant par rapport aux ressources de données de vos partenaires. Grâce à l’accès à plusieurs sources de données, AAM offre aux éditeurs numériques la possibilité d’utiliser une grande variété de données tierces : Pour en savoir plus sur AAM, consultez la documentation AAM [Documentation du produit Audience Manager](https://docs.adobe.com/content/help/fr-FR/experience-cloud/user-guides/home.html).

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
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  Envoie à la gestion de l’audience par un signal avec des caractéristiques.

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
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
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```
