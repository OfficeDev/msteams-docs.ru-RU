---
title: 'Live Share: начало работы'
author: surbhigupta
description: В этом модуле вы узнаете больше о возможностях пакета SDK для live share, разрешениях RSC и динамических структурах данных.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 6d2e1dc9d49ab1ec551fd814ba8baa330e9ace3f
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552551"
---
# <a name="live-share-core-capabilities"></a>Основные возможности Live Share

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-core-capabilities-hero.png" alt-text="Teams Live Share":::

Пакет Live Share SDK можно добавить в расширения `sidePanel` и `meetingStage` контексты ваших собраний с минимальными усилиями. В этой статье рассматривается интеграция пакета Live Share SDK в ваше приложение, а также основные возможности пакета SDK.

## <a name="install-the-javascript-sdk"></a>Установка пакета SDK для JavaScript

Пакет [Live Share SDK](https://github.com/microsoft/live-share-sdk) — это пакет JavaScript, опубликованный на[npm](https://www.npmjs.com/package/@microsoft/live-share), который можно скачать через npm или Yarn.

### <a name="npm"></a>npm

```bash
npm install @microsoft/live-share@next --save
```

### <a name="yarn"></a>Пряжи

```bash
yarn add @microsoft/live-share@next
```

## <a name="register-rsc-permissions"></a>Регистрация разрешений RSC

Чтобы включить Live Share SDK для расширения вашего собрания, необходимо сначала добавить следующие разрешения RSC в манифест вашего приложения:

```json
{
  // ...rest of your manifest here
  "configurableTabs": [
    {
        "configurationUrl": "<<YOUR_CONFIGURATION_URL>>",
        "canUpdateConfiguration": true,
        "scopes": [
            "groupchat"
        ],
        "context": [
            "meetingSidePanel",
            "meetingStage"
        ]
    }
  ],
  "validDomains": [
    "<<BASE_URI_ORIGIN>>"
  ],
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "LiveShareSession.ReadWrite.Chat",
          "type": "Delegated"
        },
        {
          "name": "LiveShareSession.ReadWrite.Group",
          "type": "Delegated"
        },
        {
          "name": "MeetingStage.Write.Chat",
          "type": "Delegated"
        },
        {
          "name": "ChannelMeetingStage.Write.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

## <a name="join-a-meeting-session"></a>Присоединение к собранию

Выполните действия, чтобы присоединиться к сеансу, связанному с собранием пользователя:

1. [Инициализация LiveShareClient](/javascript/api/@microsoft/live-share/liveshareclient).
2. Определение структур данных для синхронизации. Например, `SharedMap`.
3. Присоединение к контейнеру.

Пример.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

Это все, что требуется для настройки контейнера и присоединения к сеансу собрания. Теперь давайте рассмотрим различные типы _распределенных структур данных_, которые можно использовать с Live Share SDK.

> [!TIP]
> Прежде чем использовать API Live Share, убедитесь, что клиентский пакет SDK Teams инициализирован.

## <a name="fluid-distributed-data-structures"></a>Гибко распределенные структуры данных

Пакет Live Share SDK поддерживает любую [распределенную структуру данных](https://fluidframework.com/docs/data-structures/overview/), включенную в Fluid Framework. Ниже приведен краткий обзор нескольких доступных типов объектов:

| Общий объект                                                                       | Описание                                                                                                                             |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [SharedMap](https://fluidframework.com/docs/data-structures/map/)                   | Распределенное хранилище пары \"ключ -значение\". Задайте любой сериализуемый объект JSON для заданного ключа, чтобы синхронизировать этот объект для всех пользователей, находящихся в сеансе. |
| [SharedSegmentSequence](https://fluidframework.com/docs/data-structures/sequences/) | Структура данных, подобная списку, для хранения набора элементов (называемых сегментами) в заданных позициях.                                               |
| [SharedString](https://fluidframework.com/docs/data-structures/string/)             | Последовательность распределенных строк, оптимизированная для редактирования текста документа.                                                                |

Давайте рассмотрим принцип работы `SharedMap`. В этом примере мы использовали `SharedMap` для создания функции списка воспроизведения.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed, local) => {
  const video = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap, IValueChanged } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await liveShare.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Declare interface for object being stored in map
interface IVideo {
  id: string;
  url: string;
}

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed: IValueChanged, local: boolean) => {
  const video: IVideo | undefined = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video: IVideo) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

---

> [!NOTE]
> Основные объекты Fluid Framework DDS не поддерживают проверку роли собрания. Все участники собрания могут изменять данные, хранящиеся в этих объектах.

## <a name="live-share-data-structures"></a>Структуры данных Live Share

Пакет SDK Live Share включает набор новых классов Live Share `SharedObject` , которые предоставляют объекты с отслеживанием состояния и без отслеживания состояния, которые не хранятся в контейнере Fluid. Например, если вы хотите создать в приложении функцию лазерной указки, такую как популярную интеграцию с PowerPoint Live, вы можете использовать наши объекты `LiveEvent` или `LiveState`.

| Динамический объект                                                        | Описание                                                                                                                             |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| [LivePresence](/javascript/api/@microsoft/live-share/livepresence) | Узнайте, какие пользователи находятся в сети, задайте настраиваемые свойства для каждого пользователя и транслируйте изменения, связанные с их присутствием.                               |
| [LiveEvent](/javascript/api/@microsoft/live-share/liveevent)       | Трансляция отдельных событий с помощью любых настраиваемых атрибутов данных в полезных данных.                                                             |
| [LiveState](/javascript/api/@microsoft/live-share/livestate)       | Аналогично SharedMap, распределенное хранилище пары "ключ-значение" позволяет изменить ограниченное состояние на основе роли, например, докладчика. |
| [LiveTimer](/javascript/api/@microsoft/live-share/livetimer)       | Синхронизация таймера обратного отсчета для заданного интервала.                                                                                     |

### <a name="livepresence-example"></a>Пример LivePresence

:::image type="content" source="../assets/images/teams-live-share/live-share-presence.png" alt-text="Присутствие Teams Live Share":::

Этот `LivePresence` класс упрощает отслеживание пользователей в сеансе. При вызове метода `.initialize()` или метода `.updatePresence()` можно назначить пользовательские метаданные для этого пользователя, такие как имя или изображение профиля. Прослушивая события `presenceChanged` , каждый `LivePresenceUser` клиент получает последний объект, сворачивая все обновления присутствия в одну запись для каждого уникального `userId`объекта.

> [!NOTE]
> По умолчанию `userId` каждому из них `LivePresenceUser` назначается случайный UUID, который не привязан напрямую к удостоверению AAD. Это можно переопределить, заключив `userId` пользовательский ключ в качестве первичного ключа, как показано в примере ниже.

Пример.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  LiveShareClient,
  LivePresence,
  PresenceState,
} from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    presence: LivePresence,
  },
};
const { container } = await liveShare.joinContainer(schema);
const presence = container.initialObjects.presence;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence, local) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName, profilePicture) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  LiveShareClient,
  LivePresence,
  PresenceState,
  LivePresenceUser,
} from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomUserData {
  name: string;
  picture: string;
}

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    presence: LivePresence<ICustomUserData>,
  },
};
const { container } = await liveShare.joinContainer(schema);
const presence = container.initialObjects.presence as LivePresence<ICustomUserData>;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence: LivePresenceUser<ICustomUserData>, local: boolean) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName: string, profilePicture: string) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

---

### <a name="liveevent-example"></a>Пример LiveEvent

:::image type="content" source="../assets/images/teams-live-share/live-share-event.png" alt-text="Событие Teams Live Share для отображения уведомлений":::

`LiveEvent` — это отличный способ отправки простых событий другим клиентам на собрании. Это полезно для таких сценариев, как отправка уведомлений о сеансе.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveEvent, LiveShareClient } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { notifications: LiveEvent },
};
const { container } = await liveShare.joinContainer(schema);
const { notifications } = container.initialObjects;

// Register listener for incoming notifications
notifications.on("received", (event, local) => {
  let notificationToDisplay;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LiveEvent, ILiveEvent } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomEvent extends ILiveEvent {
  senderName: string;
  text: string;
}

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    notifications: LiveEvent<ICustomEvent>,
  },
};
const { container } = await liveShare.joinContainer(schema);
const notifications = container.initialObjects.notifications as LiveEvent<ICustomEvent>;

// Register listener for incoming notifications
notifications.on("received", (event: ICustomEvent, local: boolean) => {
  let notificationToDisplay: string;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

---

### <a name="livetimer-example"></a>Пример LiveTimer

:::image type="content" source="../assets/images/teams-live-share/live-share-timer.png" alt-text="Таймер обратного отсчета Live Share в Teams":::

`LiveTimer` включает сценарии с ограничением по времени, например таймер группировки или круговой таймер для игры.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LiveTimer } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { timer: LiveTimer },
};
const { container } = await liveShare.joinContainer(schema);
const { timer } = container.initialObjects;

// Register listener for when the timer starts its countdown
timer.on("started", (config, local) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on("played", (config, local) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on("paused", (config, local) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on("finished", (config) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on("onTick", (milliRemaining) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events for users in session
await timer.initialize();

// Start a 60 second timer
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  LiveShareClient,
  LiveTimer,
  LiveTimerEvents,
  ITimerConfig,
} from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { timer: LiveTimer },
};
const { container } = await liveShare.joinContainer(schema);
const timer = container.initialObjects.timer as LiveTimer;

// Register listener for when the timer starts its countdown
timer.on(LiveTimerEvents.started, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on(LiveTimerEvents.played, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on(LiveTimerEvents.paused, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on(LiveTimerEvents.finished, (config: ITimerConfig) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on(LiveTimerEvents.onTick, (milliRemaining: number) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events
await timer.initialize();

// Start a 60 second timer for users in session
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

---

## <a name="role-verification-for-live-data-structures"></a>Проверка роли для динамических структур данных

Собрания в Teams могут варьироваться от приватных звонков до собраний всех сотрудников компании и могут включать участников в разных организациях. Динамические объекты предназначены для поддержки проверки роли, позволяя определить роли, которым разрешено отправлять сообщения для каждого отдельного динамического объекта. Например, можно выбрать, что только выступающие и организаторы собраний могут управлять воспроизведением видео, но при этом разрешить гостям и участникам запрашивать следующее видео для просмотра.

> [!NOTE]
> Класс `LivePresence` не поддерживает проверку роли. Объект `LivePresenceUser` имеет метод `getRoles` , который возвращает роли собрания для заданного пользователя.

Пример использования `LiveState`:

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LiveState, UserMeetingRole } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { appState: LiveState },
};
const { container } = await liveShare.joinContainer(schema);
const { appState } = container.initialObjects;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state, data, local) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LiveState, UserMeetingRole } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomState {
  documentId: string;
  presentingUserId?: string;
}

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: {
    appState: LiveState<ICustomState>,
  },
};
const { container } = await liveShare.joinContainer(schema);
const appState = container.initialObjects.appState as LiveState<ICustomState>;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state: string, data: ICustomState | undefined, local: boolean) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId: string) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId: string) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

---

Перед реализацией проверки роли в приложении, особенно роли **организатора**, выслушайте своих клиентов, чтобы понять их сценарии. Нет никакой гарантии, что организатор собрания будет присутствовать на собрании. Как правило, при совместной работе в организации все пользователи будут либо **организаторами**, либо **выступающими**. Если пользователь является **участником**, то обычно это осознанное решение, принятое организатором собрания.

> [!NOTE]
> В настоящее время Live Share не поддерживает собрания каналов.

## <a name="code-samples"></a>Примеры кода

| Название примера | Описание                                                     | JavaScript                                  |
| ----------- | --------------------------------------------------------------- | ------------------------------------------- |
| Dice Roller | Включение во всех подключенных клиентах возможности прокрутки игральной кости и просмотра результата. | [View](https://aka.ms/liveshare-diceroller) |
| Игра в покер по гибкой методике | Включите все подключенные клиенты для игры в покер по гибкой методике..               | [View](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Динамический общий доступ к мультимедиа](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>См. также

- [Репозиторий GitHub](https://github.com/microsoft/live-share-sdk)
- [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Справочные документы по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
- [Вопросы и ответы о Live Share](teams-live-share-faq.md)
- [Приложения Teams на собраниях](teams-apps-in-meetings.md)
