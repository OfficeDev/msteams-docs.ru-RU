---
title: Возможности мультимедиа Live Share
author: surbhigupta
description: В этом модуле вы узнаете больше о возможностях мультимедиа Live Share, приостановках и точках ожидания, приглушении звука и синхронизации видео и аудио.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 31b962d747a792b58a9efc9e2c52e42dc841ed18
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552497"
---
# <a name="live-share-media-capabilities"></a>Возможности мультимедиа Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-media-capabilities-docs-feature-1.png" alt-text="Синхронизация мультимедиа Teams Live Share":::

Видео и аудио являются важной частью современного мира и рабочего места. Мы получили множество отзывов о том, что мы можем сделать больше для повышения качества, доступности и лицензионной защиты совместного просмотра видео на собраниях.

Пакет SDK Live Share обеспечивает надежную синхронизацию мультимедиа для любого HTML-кода  `<video>` `<audio>` и элемента с несколькими строками кода. Синхронизация мультимедиа на уровне состояния проигрывателя и элементов управления транспортировкой позволяет по отдельности атрибутировать представления и лицензию, обеспечивая при этом максимально возможное качество, доступное через ваше приложение.

## <a name="install"></a>Установка

Чтобы добавить последнюю версию пакета SDK в приложение с помощью npm:

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-media@next --save
```

ИЛИ

Чтобы добавить последнюю версию пакета SDK в приложение с помощью [Yarn](https://yarnpkg.com/):

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-media@next
```

## <a name="media-sync-overview"></a>Общие сведения о синхронизации мультимедиа

Пакет Live Share SDK имеет два основных класса, связанных с синхронизацией мультимедиа:

| Классы                                                                                        | Описание                                                                                                                                       |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [LiveMediaSession](/javascript/api/@microsoft/live-share-media/livemediasession)     | Пользовательский динамический объект, предназначенный для координации элементов управления транспортировкой мультимедиа и состояния воспроизведения в независимых потоках мультимедиа.                          |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | Синхронизирует любой объект, реализующий интерфейс `IMediaPlayer` , включая HTML5 `<video>` и `<audio>` --using `LiveMediaSession`. |

Пример.

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession } from "@microsoft/live-share-media";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession, IMediaPlayer, MediaPlayerSynchronizer } from "@microsoft/live-share-media";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const mediaSession = container.initialObjects.mediaSession as LiveMediaSession;

// Get the player from your document and create synchronizer
const player: IMediaPlayer = document.getElementById("player") as HTMLVideoElement;
const synchronizer: MediaPlayerSynchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

---

Автоматически `LiveMediaSession` прослушивает изменения состояния воспроизведения группы. `MediaPlayerSynchronizer` прослушивает создаваемые `LiveMediaSession` изменения состояния и применяет `IMediaPlayer` их к указанному объекту, например HTML5 `<video>` или элементу `<audio>` . Чтобы избежать изменений состояния воспроизведения, которые пользователь не инициировал намеренно, таких как событие буфера, необходимо вызывать элементы управления транспортом через синхронизатор, а не напрямую через проигрыватель.

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

> [!NOTE]
> Хотя объект можно использовать для `LiveMediaSession` синхронизации мультимедиа вручную, обычно рекомендуется использовать `MediaPlayerSynchronizer`. В зависимости от проигрывателя, используемго в приложении, может потребоваться создать оболочку делегата, чтобы интерфейс веб-проигрывателя соответствовал [интерфейсу IMediaPlayer](/javascript/api/@microsoft/live-share-media/imediaplayer) .

## <a name="suspensions-and-wait-points"></a>Приостановки и точки ожидания

:::image type="content" source="../assets/images/teams-live-share/live-share-media-out-of-sync.png" alt-text="Снимок экрана: синхронизация приостановки с выступающим.":::

Если вы хотите временно приостановить синхронизацию объекта `LiveMediaSession`, можно использовать приостановку. Объект [MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/livemediasessioncoordinatorsuspension) по умолчанию является локальным, что может быть полезно в тех случаях, когда пользователь может захотеть наверстать упущенное, сделать перерыв и т. д. Если пользователь завершает приостановку, синхронизация возобновляется автоматически.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const suspension: MediaSessionCoordinatorSuspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

---

При запуске приостановки можно также включить необязательный параметр [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint), который позволяет пользователям определять метки времени, в которых должна происходить приостановка для всех пользователей. Синхронизация не будет возобновлена до тех пор, пока все пользователи не прекратят приостановку для этой точки ожидания.

Вот несколько сценариев, в которых точки ожидания особенно полезны:

- Добавление теста или опроса в определенные моменты видео.
- Ожидание загрузки видео перед его запуском или во время буферизации.
- Разрешить выступающим выбирать точки в видео для группового обсуждения.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension, CoordinationWaitPoint } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const waitPoint: CoordinationWaitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);

// End the suspension when the user readies up
document.getElementById("ready-up-button")!.onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

---

## <a name="audio-ducking"></a>Приглушение звука

Пакет SDK Live Share поддерживает интеллектуальное приглушение звука. Эту функцию можно использовать в приложении, добавив в код следующее:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer;
meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer: NodeJS.Timeout | undefined;
meeting.registerSpeakingStateChangeHandler((speakingState: meeting.ISpeakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

---

Кроме того, добавьте следующие [разрешения RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) в манифест приложения:

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

> [!NOTE]
> В `registerSpeakingStateChangeHandler` настоящее время API, используемый для звука, работает только на рабочем столе Microsoft Teams, а также в запланированных собраниях и собраниях.

## <a name="code-samples"></a>Примеры кода

| Название примера          | Описание                                                                                                                               | JavaScript                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Видео React          | Базовый пример, показывающий, как объект LiveMediaSession работает с видео HTML5.                                                        | [View](https://aka.ms/liveshare-reactvideo)    |
| Шаблон мультимедиа React | Разрешите всем подключенным клиентам просматривать видео вместе, создавать общий список воспроизведения, передавать управление и добавлять заметки к видео. | [Просмотр](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Холст Live Share](teams-live-share-canvas.md)

## <a name="see-also"></a>См. также

- [Вопросы и ответы по Live Share SDK](teams-live-share-faq.md)
- [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Справочные документы по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
- [Приложения Teams на собраниях](teams-apps-in-meetings.md)
