---
title: Возможности мультимедиа Live Share
description: В этом модуле вы узнаете больше о возможностях мультимедиа Live Share, приостановках и точках ожидания, приглушении звука и синхронизации видео и аудио.
ms.topic: concept
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 662a0204793eaf2ef4702a447a4a61c79964112c
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142481"
---
---

# <a name="live-share-media-capabilities"></a>Возможности мультимедиа Live Share

Видео и аудио являются важной частью современного мира и рабочего места. Мы получили множество отзывов о том, что мы можем сделать больше для повышения качества, доступности и лицензионной защиты совместного просмотра видео на собраниях.

Пакет SDK Live Share позволяет **синхронизировать мультимедиа** с любым HTML-кодом `<video>` и элементом `<audio>` проще, чем когда-либо. Синхронизация мультимедиа на уровне состояния проигрывателя и элементов управления транспортировкой позволяет по отдельности атрибутировать представления и лицензию, обеспечивая при этом максимально возможное качество, доступное через ваше приложение.

## <a name="install"></a>Установка

Чтобы добавить последнюю версию пакета SDK в приложение с помощью npm:

```bash
npm install @microsoft/live-share --save
npm install @microsoft/live-share-media --save
```

ИЛИ

Чтобы добавить последнюю версию пакета SDK в приложение с помощью [Yarn](https://yarnpkg.com/):

```bash
yarn add @microsoft/live-share
yarn add @microsoft/live-share-media
```

## <a name="media-sync-overview"></a>Общие сведения о синхронизации мультимедиа

Пакет Live Share SDK имеет два основных класса, связанных с синхронизацией мультимедиа:

| Классы                                                                                                                  | Описание                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| [EphemeralMediaSession](/javascript/api/@microsoft/live-share-media/ephemeralmediasession)     | Пользовательский эфемерный объект, предназначенный для координации элементов управления транспортировкой мультимедиа и состояния воспроизведения в независимых потоках мультимедиа. |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | Синхронизирует локальный мультимедийный элемент HTML с группой удаленных элементов мультимедиа HTML для `EphemeralMediaSession`.|

Пример.

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { EphemeralMediaSession } from "@microsoft/live-share-media";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Setup the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { mediaSession: EphemeralMediaSession },
};
const { container } = await client.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = ["Organizer", "Presenter"];
await mediaSession.start(allowedRoles);
```

`EphemeralMediaSession` автоматически прослушивает изменения состояния воспроизведения группы и применяет изменения через `MediaPlayerSynchronizer`. Чтобы избежать изменений состояния воспроизведения, которые пользователь не инициировал намеренно, таких как событие буфера, необходимо вызывать элементы управления транспортом через синхронизатор, а не напрямую через проигрыватель.

Пример.

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
  <div class="player-controls">
    <button id="play-button">Play</button>
    <button id="pause-button">Pause</button>
    <button id="restart-button">Restart</button>
    <button id="change-track-button">Change track</button>
  </div>
</body>
```

```javascript
// ...

document.getElementById("play-button").onclick = () => {
  synchronizer.play();
};

document.getElementById("pause-button").onclick = () => {
  synchronizer.pause();
};

document.getElementById("restart-button").onclick = () => {
  synchronizer.seekTo(0);
};

document.getElementById("change-track-button").onclick = () => {
  synchronizer.setTrack({
    trackIdentifier: "SOME_OTHER_VIDEO_SRC",
  });
};
```

 > [!Note]
 > Хотя объект `EphemeralMediaSession` можно использовать для прямой синхронизации мультимедиа с помощью `MediaPlayerSynchronizer`, если вы не хотите более точного управления логикой синхронизации. В зависимости от проигрывателя, используемого в приложении, можно создать тестовый модификатор делегата, чтобы интерфейс веб-проигрывателя соответствовал интерфейсу мультимедиа HTML.

## <a name="suspensions-and-wait-points"></a>Приостановки и точки ожидания

Если вы хотите временно приостановить синхронизацию объекта `EphemeralMediaSession`, можно использовать приостановку. Объект [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/ephemeralmediasessioncoordinatorsuspension) по умолчанию является локальным, что может быть полезно в тех случаях, когда пользователь может захотеть наверстать упущенное, сделать перерыв и т. д. Если пользователь завершает приостановку, синхронизация возобновляется автоматически.

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

При запуске приостановки можно также включить необязательный параметр [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint), который позволяет пользователям определять метки времени, в которых должна происходить приостановка для всех пользователей. Синхронизация не будет возобновлена до тех пор, пока все пользователи не прекратят приостановку для этой точки ожидания. Это полезно для таких действий, как добавление теста или опроса в определенные моменты видео.

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension();
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

## <a name="audio-ducking"></a>Приглушение звука

Пакет SDK Live Share поддерживает интеллектуальное приглушение звука. Вы можете использовать _экспериментальную_ функцию в приложении, добавьте в код следующее:

```javascript
import * as microsoftTeams from "@microsoft/teams-js";

// ...

let volumeTimer;
microsoftTeams.meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

Чтобы включить приглушение звука, добавьте в манифест приложения следующие разрешения [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent):

```json
{
  // ...rest of your manifest here
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Chat",
          "type": "Delegated"
        },
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

> [!Note]
> API `registerSpeakingStateChangeHandler`, используемый для приглушения звука, в настоящее время работает только для нелокальных пользователей, которые говорят.

## <a name="code-samples"></a>Примеры кода

| Название примера   | Описание | JavaScript |
| -------------------- | ----------------------------| -----------------|
| Видео React          | Базовый пример, показывающий, как объект EphemeralMediaSession работает с видео HTML5.                                                        | [View](https://aka.ms/liveshare-reactvideo)    |
| Шаблон мультимедиа React | Разрешите всем подключенным клиентам просматривать видео вместе, создавать общий список воспроизведения, передавать управление и добавлять заметки к видео. | [Просмотр](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Руководство для разработки игры в покер по гибкой методике](../sbs-teams-live-share.yml)

## <a name="see-also"></a>См. также

* [Вопросы и ответы по Live Share SDK](teams-live-share-faq.md)
* [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Справочная документация по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
* [Справочные документы](https://aka.ms/livesharedocs)
* [Приложения Teams на собраниях](teams-apps-in-meetings.md)
