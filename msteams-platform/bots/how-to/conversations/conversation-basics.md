---
title: Основы разговора
author: clearab
description: Беседа с ботом Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075695"
---
# <a name="conversation-basics"></a>Основы разговора

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Беседа — это серия сообщений, отправленных между ботом и одним или более пользователями. Существует три типа бесед (также называемых областью) в Teams:

* `teams` Также называется беседами канала, которые видны всем участникам канала.
* `personal` Беседы между ботами и одним пользователем.
* `groupChat` Чат между ботом и двумя или более пользователями. Также включает бота в чатах собраний.

Бот ведет себя немного по-разному в зависимости от типа беседы, в которых он участвует:

* Боты в беседах в канале и групповом чате требуют от пользователя @упоминания бота, чтобы вызвать его в канале.
* Боты в беседе "один к одному" не требуют @упоминания. Все сообщения, отправленные пользователем, будут направлены вашему боту.

Чтобы включить бота в определенной области, добавьте эту область в манифест [приложения.](~/resources/schema/manifest-schema.md)

## <a name="activities"></a>Действия

Каждое сообщение является `Activity` объектом типа `messageType: message` . Когда пользователь отправляет сообщение, Teams отправляет его вашему боту; В частности, он отправляет объект JSON в конечную точку обмена сообщениями бота. Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.

Базовая беседа обрабатывается через соединители Bot Framework, один API REST, позволяющий боту взаимодействовать с Teams и другими каналами. SDK построитель ботов предоставляет простой доступ к этому API, дополнительные функции для управления потоком беседы и состоянием, а также простые способы включения функций распознавания, таких как обработка естественного языка (NLP).

## <a name="receive-a-message"></a>Получение сообщения

Чтобы получить текстовое сообщение, используйте `Text` свойство `Activity` объекта. В обработнике действий бота используйте объект контекста turn для чтения `Activity` одного запроса сообщения.

Ниже приведен пример кода.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a>Отправка сообщения

Чтобы отправить текстовое сообщение, укажите строку, отправляемую в качестве действия. В обработчике действий бота используйте метод объекта контекста turn для отправки `SendActivityAsync` одного ответа на сообщение. Вы также можете использовать метод объекта `SendActivitiesAsync` для отправки нескольких ответов одновременно. В приведенном ниже коде показан пример отправки сообщения при добавлении кого-либо в беседу  

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="teams-channel-data"></a>Данные канала Teams

Объект `channelData` содержит сведения, специфичная для Teams, и является окончательным источником для кодов команды и канала. Возможно, потребуется кэширования и использовать эти ids в качестве ключей для локального хранилища. Как правило, SDK извлекет важные сведения из объекта, чтобы сделать его более доступным, однако вы всегда можете получить доступ к исходной информации `TeamsActivityHandler` `channelData` из `turnContext` объекта.

Объект не включается в сообщения в личных беседах, так как они проходят `channelData` за пределами любого канала.

Типичный объект channelData в действии, отправленный вашему боту, содержит следующие сведения:

* `eventType` Тип события Teams; передается только в случае событий [изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `tenant.id` ИД клиента Azure Active Directory; передается во всех контекстах
* `team` Передается только в контекстах канала, а не в личном чате.
  * `id` GUID для канала
  * `name` Имя команды; передается только в случае [переименования команд](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel` Передается только в контекстах канала, когда упоминается бот, или для событий в каналах в командах, в которые был добавлен бот
  * `id` GUID для канала
  * `name`Имя канала; передается только в случае событий [изменения канала.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channelData.teamsTeamId` Неподготовлено. Это свойство включено только для обратной совместимости.
* `channelData.teamsChannelId` Неподготовлено. Это свойство включено только для обратной совместимости.

### <a name="example-channeldata-object-channelcreated-event"></a>Пример объекта channelData (событие channelCreated)

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## <a name="message-content"></a>Содержимое сообщения

Бот может отправлять текст, изображения и карточки. Пользователи могут отправлять вашему боту текст и изображения.

| Format    | От пользователя к боту | От бота к пользователю | Примечания                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Форматированный текст  | ✔                | ✔                |                                                                                         |
| Изображения  | ✔                | ✔                | Не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается  |
| Карточки     | ✖                | ✔                | См. справочник [по карточкам Teams для](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемых карточек |
| Emojis    | ✖                | ✔                | В настоящее время Teams поддерживает эмодзи через UTF-16 (например, U+1F600 для ухмылки)          |

## <a name="adding-notifications-to-your-message"></a>Добавление уведомлений в сообщение

Уведомления оповещают пользователей о новых задачах, упоминаниях и примечаниях, связанных с тем, над чем они работают, или о том, что им нужно посмотреть, вставив уведомление в веб-канал активности. Вы можете настроить уведомления для запуска из сообщения бота, установив для свойства `TeamsChannelData` `Notification.Alert` объектов true. В конечном счете, будет зависеть от параметров Teams отдельного пользователя, и вы не сможете программным образом переопределять эти параметры. Тип уведомления будет баннером или баннером и сообщением электронной почты.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a>Сообщения с рисунками

Изображения отправляются путем добавления вложений в сообщение. Дополнительные сведения о вложениях можно найти в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)

Изображения могут иметь не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается.

Рекомендуется указать высоту и ширину каждого изображения с помощью XML. Если вы используете Markdown, размер изображения по умолчанию составляет 256×256. Например:

* Использование — `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте — `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="code-sample"></a>Пример кода
|**Имя примера** | **Описание** | **. NETCore** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| Бот беседы Teams | Обработка событий обмена сообщениями и бесед. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a>Дальнейшие действия

* [Отправка упреждающих сообщений](~/bots/how-to/conversations/send-proactive-messages.md)
* [Подписка на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
