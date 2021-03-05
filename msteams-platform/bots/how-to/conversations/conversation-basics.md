---
title: Основы разговора
description: описывает способы беседы с ботом Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 4eba22e9b29f5378dc03480ba5f6ba421f816eb3
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449509"
---
# <a name="conversation-basics"></a>Основы разговора

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Беседа — это серия сообщений, отправленных между ботом и одним или более пользователями. Существует три типа бесед, которые также называются области в Teams:

| Тип беседы | Описание |
| ------- | ----------- |
|  `teams` | Также называются телефонные беседы, видимые всем участникам канала. |
| `personal` | Беседы между ботами и одним пользователем. |
| `groupChat` | Чат между ботом и двумя или более пользователями. Также включает бота в чаты собраний. |

Бот ведет себя немного по-другому в зависимости от того, в какой беседе он участвует:

* Боты в беседах с каналами и групповыми чатами требуют от пользователя @ упоминания бота, чтобы вызвать его в канале.
* Боты в беседе один к одному не требуют упоминания @. Все сообщения, отправленные пользователем по маршрутам к боту.

Чтобы включить бот в определенной области, добавьте эту область в [манифест приложения.](~/resources/schema/manifest-schema.md)

## <a name="activities"></a>Действия

Каждое сообщение — `Activity` это объект типа `messageType: message` . Когда пользователь отправляет сообщение, Teams отправляет сообщение вашему боту; В частности, он отправляет объект JSON в конечную точку обмена сообщениями вашего бота. Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.

Основные беседы обрабатываются с помощью соединиттеля Bot Framework, единого API REST. Этот API позволяет боту взаимодействовать с Teams и другими каналами. SDK Bot Builder предоставляет простой доступ к этому API, дополнительные функции для управления потоком беседы и состоянием, а также простые способы включения когнитивных служб, таких как обработка естественного языка (NLP).

## <a name="receive-a-message"></a>Получение сообщения

Чтобы получить текстовое сообщение, используйте `Text` свойство `Activity` объекта. В обработнике действий бота используйте объект контекста поворота для чтения `Activity` одного запроса сообщения.

Ниже приводится пример кода.

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

Чтобы отправить текстовое сообщение, укажите строку, которая будет отправляться в качестве действия. В обработнике действий бота используйте метод объекта контекста поворота для `SendActivityAsync` отправки единого ответа сообщения. Используйте метод объекта `SendActivitiesAsync` для отправки сразу нескольких ответов. В следующем коде показан пример отправки сообщения при добавлении в беседу.

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

> [!NOTE]
> Разделение сообщений происходит, когда текстовое сообщение и вложение отправляются в той же полезной нагрузке. Это действие разделено на отдельные действия Microsoft Teams, одно действие с только текстовым сообщением, а другое с вложением. При разделении действия в ответ не получается ID сообщения, [](~/bots/how-to/update-and-delete-bot-messages.md) который используется для обновления или удаления сообщения. Рекомендуется отправлять отдельные действия, а не в зависимости от разделения сообщений.

## <a name="teams-channel-data"></a>Данные канала teams

Объект содержит сведения, определенные для Teams, и является окончательным источником для кодов `channelData` групп и каналов. Может потребоваться кэширования и использования этих ID-данных в качестве ключей для локального хранения. В SDK обычно извлекаются важные сведения из объекта, чтобы сделать `TeamsActivityHandler` `channelData` его доступным. Однако вы всегда можете получить доступ к исходным данным `turnContext` объекта.

Объект не входит в сообщения в личных беседах, так как они проходят `channelData` за пределами любого канала.

Типичный объект channelData в действии, отправленный боту, содержит следующие сведения:

* `eventType`Тип событий Teams; передается только в случаях [событий изменения канала.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `tenant.id` ID клиента Azure Active Directory, переданный во всех контекстах.
* `team` Передается только в контекстах каналов, а не в личном чате.
  * `id` GUID для канала.
  * `name`Имя команды; передается только в случаях [переименования событий команды.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel` Передается только в контекстах каналов, когда бот упоминается или для событий в каналах в командах, где был добавлен бот.
  * `id` GUID для канала.
  * `name`Имя канала; передается только в случаях [событий изменения канала.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channelData.teamsTeamId` Обесценилось. Это свойство включено только для обратной совместимости.
* `channelData.teamsChannelId` Обесценилось. Это свойство включено только для обратной совместимости.

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

Бот может отправлять богатый текст, изображения и карточки. Пользователи могут отправлять богатый текст и изображения в бот.

| Format    | От пользователя к боту | От бота к пользователю | Примечания                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Форматированный текст  | ✔                | ✔                |                                                                                         |
| Изображения  | ✔                | ✔                | Максимальный размер 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF не поддерживается  |
| Карточки     | ✖                | ✔                | См. [ссылку на карточки Teams для](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемых карт |
| Emojis    | ✖                | ✔                | Teams currently supports emojis through UTF-16 (such as U+1F600 for grinning face)          |

## <a name="adding-notifications-to-your-message"></a>Добавление уведомлений в сообщение

Уведомления оповещают пользователей о новых задачах, упоминаниях и комментариях, связанных с тем, над чем они работают или на которые необходимо смотреть, вставив уведомление в канал активности. Вы можете настроить уведомления для запуска бот-сообщения, установив свойство `TeamsChannelData` `Notification.Alert` объектов до true. В конечном счете, вопрос о том, будет ли поднято уведомление, зависит от параметров teams отдельного пользователя, и программным образом переопреять эти параметры невозможно. Тип уведомления — это баннер или баннер и электронная почта.

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

## <a name="picture-messages"></a>Сообщения изображений

Изображения отправляются путем добавления вложений в сообщение. Дополнительные сведения о вложениях можно найти в документации [Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)

Изображения могут быть не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF. Анимированный GIF не поддерживается.

Всегда укажите высоту и ширину каждого изображения с помощью XML. В Markdown размер изображения по умолчанию составляет 256×256. Например:

* Использование - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте - `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="adaptive-cards"></a>Адаптивные карты

Для отправки простой адаптивной карты используйте следующий код:

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

Дополнительные информацию о картах и картах в ботах см. в [документации по картам.](~/task-modules-and-cards/what-are-cards.md)

## <a name="code-sample"></a>Пример кода

|**Пример имени** | **Описание** | **. NETCore** | **JavaScript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| Командный бот беседы | Обработка событий обмена сообщениями и бесед. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a>Дальнейшие действия

* [Отправка упреждающих сообщений](~/bots/how-to/conversations/send-proactive-messages.md)
* [Подписка на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
