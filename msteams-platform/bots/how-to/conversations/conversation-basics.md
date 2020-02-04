---
title: Общие сведения о беседах
author: clearab
description: Как создать беседу с роботом Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2d241ad04509c596e97647138bab2a749fa0f74c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675311"
---
# <a name="conversation-basics"></a>Общие сведения о беседах

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Беседа — это серия сообщений, отправляемых между Bot и одним или несколькими пользователями. В Teams существует три вида бесед (также называемых областями):

* `teams`Также называется каналы каналов, видимых всем участникам канала.
* `personal`Беседы между Боты и одним пользователем.
* `groupChat`Чат между Bot и двумя или несколькими пользователями. Кроме того, в конференциях можно включить робота.

В зависимости от типа беседы, в которой она участвует, программа-робота немного ведет себя по-разному.

* Для боты в беседах в канале и группе необходимо, чтобы пользователь "@" привызывал его в канале.
* Для боты в беседе "один к одному" не требуется указать @ упоминание. Все сообщения, отправленные пользователем, будут перенаправляться в робот.

Чтобы включить Bot в определенной области, добавьте эту область в [манифест приложения](~/resources/schema/manifest-schema.md).

## <a name="activities"></a>Действия

Каждое сообщение является `Activity` объектом типа `messageType: message`. Когда пользователь отправляет сообщение, Teams отправляет сообщение на сервер почтовых роботов; в частности, он отправляет объект JSON в конечную точку обмена сообщениями ленты. Ваш почтовый робот просматривает сообщение, чтобы определить его тип и ответить соответствующим образом.

Основная беседа обрабатывается через соединитель Bot Framework, один REST API, позволяющий роботам общаться с Teams и другими каналами. Пакет SDK построителя позволяет легко получить доступ к этому API, дополнительные функции для управления движением и состоянием беседы, а также простые способы внедрения таких служб, как естественный язык (НЛП).

## <a name="receive-a-message"></a>Получение сообщения

Для получения текстового сообщения используйте `Text` свойство `Activity` объекта. В обработчике действий Bot используйте объект "переключить контекст" `Activity` , чтобы считать один запрос сообщения.

Ниже приведен пример кода.

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/Node. js](#tab/typescript)

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

# <a name="pythontabpython"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

Чтобы отправить текстовое сообщение, укажите строку, которую необходимо отправить как действие. В обработчиках действий Bot используйте `SendActivityAsync` метод "переключить контекстный объект" для отправки одного ответа на сообщение. Кроме того, можно использовать `SendActivitiesAsync` метод объекта для отправки нескольких ответов одновременно. В приведенном ниже коде показан пример отправки сообщения, когда кто-то добавляется в беседу.  

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/Node. js](#tab/typescript)

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

# <a name="pythontabpython"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

`channelData` Объект содержит сведения, зависящие от команды, и является основным источником для идентификаторов команд и каналов. Возможно, вам потребуется кэшировать и использовать эти идентификаторы в качестве ключей для локального хранилища. `TeamsActivityHandler` В пакете SDK обычно запрашиваются важные сведения из `channelData` объекта, чтобы сделать его более легко доступным, но вы всегда можете получить доступ к исходным данным из `turnContext` объекта.

Этот `channelData` объект не включается в сообщения в личных беседах, так как они выполняются вне какого-либо канала.

Типичный объект Чаннелдата в действии, отправляемом на почтовый робот, содержит следующие сведения:

* `eventType`Тип события Teams; передается только в случае [событий изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `tenant.id`Идентификатор клиента Azure Active Directory; передается во всех контекстах
* `team`Передается только в контекстах канала, а не в личном сеансе чата.
  * `id`GUID для канала
  * `name`Имя команды; передается только в случае [событий переименования команды](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* `channel`Передается только в контекстах канала при упоминании Bot или для событий в каналах в Microsoft Teams, где добавлен Bot
  * `id`GUID для канала
  * `name`Имя канала; передается только в случае [событий изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`Устаревшие. Это свойство включено только для обеспечения обратной совместимости.
* `channelData.teamsChannelId`Устаревшие. Это свойство включено только для обеспечения обратной совместимости.

### <a name="example-channeldata-object-channelcreated-event"></a>Пример объекта Чаннелдата (событие Чаннелкреатед)

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

Ваш робот может отправлять форматированный текст, изображения и карточки. Пользователи могут отправлять форматированный текст и изображения в Bot.

| Format    | От пользователя к Bot | От Bot к пользователю | Примечания                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Форматированный текст  | ✔                | ✔                |                                                                                         |
| Изображения  | ✔                | ✔                | Не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается  |
| Карточки     | ✖                | ✔                | Поддерживаемые карточки представлены в [справочнике по карточке Teams](~/task-modules-and-cards/cards/cards-reference.md) |
| Эмодзи    | ✖                | ✔                | В настоящее время Teams поддерживает эмодзи, используя кодировку UTF-16 (например, U + 1F600 для гриннинг Face)          |

## <a name="adding-notifications-to-your-message"></a>Добавление уведомлений в сообщение

Уведомления уведомляют пользователей о новых задачах, упоминании и комментариях, связанных с тем, над чем они работают, или необходимо просмотреть, вставив уведомление в свой канал активности. Вы можете настроить уведомления для запуска из сообщения Bot, задав для свойства `TeamsChannelData` Objects `Notification.Alert` значение true. Если уведомление не будет вызвано, в конечном итоге зависит от параметров Teams отдельного пользователя, и вы не сможете программно переопределить эти параметры. Типом уведомления будет либо баннер, либо баннер и электронная почта.

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/Node. js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

## <a name="picture-messages"></a>Графические сообщения

Изображения отправляются путем добавления вложений к сообщению. Дополнительные сведения о вложениях можно найти в [документации по среде Bot](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).

Рисунки могут иметь не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается.

Рекомендуем указать высоту и ширину каждого изображения с помощью XML. Если вы используете Markdown, размер изображения по умолчанию равен 256 × 256. Пример:

* Используйте`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте —`![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="next-steps"></a>Дальнейшие действия

* [Отправка упреждающих сообщений](~/bots/how-to/conversations/send-proactive-messages.md)
* [Подписаться на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
