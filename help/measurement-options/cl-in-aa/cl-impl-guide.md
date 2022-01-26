---
title: Présentation de l’implémentation d’un lien personnalisé
description: Découvrez comment implémenter le suivi des liens personnalisés dans Streaming Media Analytics.
uuid: 83315e73-20ca-4db5-9d43-33daade45a13
exl-id: ee6f931a-ef80-4ebe-8ccb-cdbf970516e6
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---

# Guide de mise en œuvre d’un lien personnalisé{#custom-link-implementation-guide}

Le suivi vidéo personnalisé utilise le suivi manuel des liens à l’aide du code de lien personnalisé dans le code `appMeasurement` d’Analytics.
Le plus souvent, il est utilisé sur les plateformes et les appareils nécessitant peu de mesures vidéo.

* Dans JavaScript : la fonction `s.tl()`
* Dans les applications mobiles : [trackAction() Android](https://experienceleague.adobe.com/docs/mobile-services/android/analytics-android/actions.html?lang=fr), [trackAction() iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/analytics-ios/actions.html?lang=fr), [trackAction() OTT](/help/sdk-implement/analytics-with-ott/track-app-actions.md)
* Dans l’API Data Insertion : [balise linktype](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/reference/r_supported_tags.md)

## Conditions

* Accès aux événements et aux données de l’API du lecteur vidéo
* Possibilité d’ajouter des scripts en cas d’utilisation du SDK Analytics
* Possibilité d’ajouter des balises de suivi (script personnalisé ou code en dur) en cas d’utilisation de l’API Data Insertion

## Métadonnées

* Des métadonnées peuvent être ajoutées aux données de lien de n’importe quel appel de suivi.
* N’oubliez pas de mettre à jour `linkTrackVars` et `linkTrackEvents`.

```javascript
/* Call on video complete */

if (e.type == "ended") {  
    s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
    s.linkTrackEvents = 'event3';
    s.prop10 = mediaName;
    s.eVar10 = mediaName;
    s.eVar12 = "video";
    s.eVar13 = document.title;
    s.eVar15 = mediaPlayerName;
    s.events = 'event3';
    s.tl(this,'o','Video Complete');
};
```

## Pourquoi utiliser un lien personnalisé

* Peu de conditions requises
* Fonctionne sur n’importe quelle plateforme, y compris NoScript
* Tout calcul, tel que le temps passé ou les quartiles, doit être effectué dans un script personnalisé.
* Très simple sans bibliothèque ni script masqué
* Contrôle total sur tous les aspects des données vidéo

## Exemple de lecteur JavaScript pour HTML5

```javascript
<script type="text/javascript">
  myvideo = document.getElementById('movie');
  myvideo.addEventListener('play',myHandler,false);
  myvideo.addEventListener('seeked',myHandler,false);
  myvideo.addEventListener('seeking',myHandler,false);
  myvideo.addEventListener('pause',myHandler,false);
  myvideo.addEventListener('ended',myHandler,false);

  function myHandler(e) {
      var video = document.getElementsByTagName('video')[0];
      var mediaName="13502979:Sailing";
      var mediaLength = video.duration;
      var mediaPlayerName = "HTML5 Player";
      /*Define video offset*/
      if (video.currentTime > 0) {
          mediaOffset = Math.floor(video.currentTime);
      } else {
          mediaOffset = 0;
      };
      /*Call on video start*/
      if (e.type == "play") {
          if (mediaOffset == 0) {
              console.log(mediaPlayerName +
                ' -> start -> playhead: ' +  
                Math.floor(video.currentTime));
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event2';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event2';
              s.tl(this,'o','Video Start');
          }
      };

      /*Call on video pause*/
      if (e.type == "pause") {
          console.log(mediaPlayerName +' -> pause -> playhead: ' + Math.floor(video.currentTime));
          if (video.currentTime != video.duration) {
              s.linkTrackVars='events,prop10,eVar10,eVar12,eVar13,eVar15';
              s.linkTrackEvents='event7';
              s.prop10=mediaName;
              s.eVar10=mediaName;
              s.eVar12="video";
              s.eVar13=document.title;
              s.eVar15=mediaPlayerName;
              s.events='event7';
              s.tl(this,'o','Video Pause');
          }
      };

      /*Call on video complete*/
      if (e.type == "ended") {
          console.log(mediaPlayerName +
            ' -> ended -> playhead: ' +
            Math.floor(video.currentTime));
          s.linkTrackVars = 'events, prop10, eVar10, eVar12, eVar13, eVar15';
          s.linkTrackEvents = 'event3';
          s.prop10= m ediaName;
          s.eVar10=mediaName;
          s.eVar12="video";
          s.eVar13=document.title;
          s.eVar15=mediaPlayerName;
          s.events='event3';
          s.tl(this,'o','Video Complete');
      };
  };
</script>
```
