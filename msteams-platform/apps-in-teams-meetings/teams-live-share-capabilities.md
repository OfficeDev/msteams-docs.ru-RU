---
title: 'Live Share: начало работы'
description: В этом модуле вы узнаете больше о возможностях пакета SDK для Live Share, разрешениях RSC и структурах зашифрованных данных.
ms.topic: concept
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 35d5228ac39dd1a9d58d699d8c989aeeceaf765d
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503349"
---
---

# <a name="live-share-core-capabilities"></a>Основные возможности Live Share

Пакет Live Share SDK можно добавить в расширения `sidePanel` и `meetingStage` контексты ваших собраний с минимальными усилиями. В этой статье рассматривается интеграция пакета Live Share SDK в ваше приложение, а также основные возможности пакета SDK.

> [!Note]
> В настоящее время поддерживаются только запланированные собрания, и все участники должны быть в календаре собрания. Такие типы собраний, как приватные звонки, групповые звонки и незапланированные собрания, в настоящее время не поддерживаются.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-dashboard.png" alt-text="Teams Live Share":::

## <a name="install-the-javascript-sdk"></a>Установка пакета SDK для JavaScript

Пакет [Live Share SDK](https://github.com/microsoft/live-share-sdk) — это пакет JavaScript, опубликованный на[npm](https://www.npmjs.com/package/@microsoft/live-share), который можно скачать через npm или Yarn.

**npm**

```bash
npm install @microsoft/live-share --save
```

**Yarn**

```bash
yarn add @microsoft/live-share
```

## <a name="register-rsc-permissions"></a>Регистрация разрешений RSC

Чтобы включить Live Share SDK для расширения вашего собрания, необходимо сначала добавить следующие разрешения RSC в манифест вашего приложения:

```json
{
  // ...rest of your manifest here
  "configurableTabs": [
    {
        "configurationUrl": "https://<<BASE_URI_ORIGIN>>/config",
        "canUpdateConfiguration": false,
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

1. Инициализация клиентского пакета SDK для Teams.
2. Инициализация [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient).
3. Определение структур данных для синхронизации. Например, `SharedMap`.
4. Присоединение к контейнеру.

Пример.

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Setup the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

Это все, что требуется для настройки контейнера и присоединения к сеансу собрания. Теперь давайте рассмотрим различные типы _распределенных структур данных_, которые можно использовать с Live Share SDK.

## <a name="fluid-distributed-data-structures"></a>Гибко распределенные структуры данных

Пакет Live Share SDK поддерживает любую [распределенную структуру данных](https://fluidframework.com/docs/data-structures/overview/), включенную в Fluid Framework. Ниже приведен краткий обзор нескольких доступных типов объектов:

| Общий объект                                                                       | Описание                                                                                                                                  |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [SharedMap](https://fluidframework.com/docs/data-structures/map/)                   | Распределенное хранилище пары \"ключ -значение\". Задайте любой сериализуемый объект JSON для заданного ключа, чтобы синхронизировать этот объект для всех пользователей, находящихся в сеансе. |
| [SharedSegmentSequence](https://fluidframework.com/docs/data-structures/sequences/) | Структура данных, подобная списку, для хранения набора элементов (называемых сегментами) в заданных позициях.                                                    |
| [SharedString](https://fluidframework.com/docs/data-structures/string/)             | Последовательность распределенных строк, оптимизированная для редактирования текста документа.                                                                     |

Давайте рассмотрим принцип работы `SharedMap`. В этом примере мы использовали `SharedMap` для создания функции списка воспроизведения.

```javascript
import { SharedMap } from "fluid-framework";
// ...
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const { playlistMap } = container.initialObjects;

// Listen for changes to values in the map
playlistMap.on("valueChanged", (changed, local) => {
  const video = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video) {
  // Add video to map
  playlistMap.set(video.id, video);
}
// ...
```

> [!Note]
> Основные объекты Fluid Framework DDS не поддерживают проверку роли собрания. Все участники собрания могут изменять данные, хранящиеся в этих объектах.

## <a name="live-share-ephemeral-data-structures"></a>Временные структуры данных Live Share

Пакет Live Share SDK содержит набор новых временных классов `SharedObject`, предоставляющих объекты с отслеживанием состояния и без отслеживания состояния, которые не хранятся в контейнере Fluid. Например, если вы хотите создать в приложении функцию лазерной указки, такую как популярную интеграцию с PowerPoint Live, вы можете использовать наши объекты `EphemeralEvent` или `EphemeralState`.

| Временный объект                                                                                                       | Описание                                                                                                                     |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralPresence](/javascript/api/@microsoft/live-share/ephemeralpresence) | Узнайте, какие пользователи находятся в сети, задайте настраиваемые свойства для каждого пользователя и транслируйте изменения, связанные с их присутствием.                       |
| [EphemeralEvent](/javascript/api/@microsoft/live-share/ephemeralevent)       | Трансляция отдельных событий с помощью любых настраиваемых атрибутов данных в полезных данных.                                                     |
| [EphemeralState](/javascript/api/@microsoft/live-share/ephemeralstate)       | Аналогично SharedMap, распределенное хранилище пары "ключ-значение" позволяет изменить ограниченное состояние на основе роли, например, докладчика.|

### <a name="ephemeralpresence-example"></a>Пример EphemeralPresence

Этот `EphemeralPresence` класс упрощает отслеживание участников собрания. При вызове метода `.start()` или `.updatePresence()` можно назначить пользовательские метаданные для этого пользователя, например, уникальный идентификатор или имя.

Пример.

```javascript
import { EphemeralPresence, PresenceState } from "@microsoft/live-share";
// ...
const schema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);
const { presence } = container.initialObjects;

// Listen for changes to presence
presence.on("presenceChanged", (userPresence, local) => {
  // Update UI with presence
});

// Start tracking presence
presence.start("YOUR_CUSTOM_USER_ID", {
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

### <a name="ephemeralevent-example"></a>Пример EphemeralEvent

`EphemeralEvent` — это отличный способ отправки простых событий другим клиентам на собрании. Это полезно для таких сценариев, как отправка уведомлений о сеансе.

```javascript
import { EphemeralEvent } from "@microsoft/live-share";
// ...
const schema = {
  initialObjects: { notifications: EphemeralEvent },
};
const { container } = await client.joinContainer(schema);
const { notifications } = container.initialObjects;

// Listen for incoming notifications
notifications.on("received", (event, local) => {
  let notificationToDisplay;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start tracking notifications
await notifications.start();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

## <a name="role-verification-for-ephemeral-data-structures"></a>Проверка роли для временных структур данных

Собрания в Teams могут варьироваться от приватных звонков до собраний всех сотрудников компании и могут включать участников в разных организациях. Временные объекты предназначены для поддержки проверки роли, что позволяет определить роли, которым разрешено отправлять сообщения для каждого отдельного временного объекта. Например, можно выбрать, что только выступающие и организаторы собраний могут управлять воспроизведением видео, но при этом разрешить гостям и участникам запрашивать следующее видео для просмотра.

Пример.

```javascript
import { EphemeralState, UserMeetingRole } from "@microsoft/live-share";
// ...
const schema = {
  initialObjects: { appState: EphemeralState },
};
const { container } = await client.joinContainer(schema);
const { appState } = container.initialObjects;

// Listen for changes to values in the map
appState.on("stateChanged", (state, value, local) => {
  // Update local app state
});

// Set roles who can change state and start
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.start(allowedRoles);

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

Перед реализацией проверки роли в приложении, особенно роли **организатора**, выслушайте своих клиентов, чтобы понять их сценарии. Нет никакой гарантии, что организатор собрания будет присутствовать на собрании. Как правило, при совместной работе в организации все пользователи будут либо **организаторами**, либо **выступающими**. Если пользователь является **участником**, то обычно это осознанное решение, принятое организатором собрания.

## <a name="code-samples"></a>Примеры кода

| Название примера | Описание  | JavaScript  |
| ----------- | ---------------------------------------------- | -------------- |
| Dice Roller | Включение во всех подключенных клиентах возможности прокрутки игральной кости и просмотра результата. | [View](https://aka.ms/liveshare-diceroller) |
| Игра в покер по гибкой методике | Включите все подключенные клиенты для игры в покер по гибкой методике..| [View](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Возможности мультимедиа Live Share](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>См. также

* [Репозиторий GitHub](https://github.com/microsoft/live-share-sdk)
* [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Справочные документы по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
* [Вопросы и ответы о Live Share](teams-live-share-faq.md)
* [Приложения Teams на собраниях](teams-apps-in-meetings.md)
