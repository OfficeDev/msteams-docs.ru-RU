---
title: Сообщения в беседах с ботами
description: Описывает способы общения с Microsoft Teams ботом. Узнайте о Teams канале, уведомлениях о сообщении, изображениях и адаптивных карточках с помощью примеров кода.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 1b3f5784161295aa31a723e3ca6b0a08f21afb76
ms.sourcegitcommit: f7d0e330c96e00b2031efe6f91a0c67ab0976455
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2022
ms.locfileid: "65611460"
---
# <a name="messages-in-bot-conversations"></a>Сообщения в беседах с ботами

Каждое сообщение в беседе является объектом `Activity` типа `messageType: message`. Когда пользователь отправляет сообщение, Teams отправляет его боту. Teams отправляет объект JSON в конечную точку обмена сообщениями бота. Бот проверяет сообщение, чтобы определить его тип и ответить соответствующим образом.

Основные беседы обрабатываются через соединитель Bot Framework, один REST API. Этот API позволяет боту взаимодействовать с Teams и другими каналами. Пакет SDK Bot Builder предоставляет следующие функции:

* Простой доступ к соединителю Bot Framework.
* Дополнительные функции для управления потоком беседы и состоянием.
* Простые способы внедрения когнитивных служб, таких как обработка естественного языка (NLP).

Бот получает сообщения от Teams с `Text` помощью свойства и отправляет пользователям один или несколько ответов на сообщения.

Дополнительные сведения см[. в описании атрибутов пользователей для сообщений бота](/microsoftteams/platform/messaging-extensions/how-to/action-commands/respond-to-task-module-submit?tabs=dotnet%2Cdotnet-1&branch=pr-en-us-5926#user-attribution-for-bots-messages).

## <a name="receive-a-message"></a>Получение сообщения

Чтобы получить текстовое сообщение, используйте свойство `Text` объекта `Activity`. В обработчике активности бота используйте объект контекста поворота `Activity` для чтения одного запроса сообщения.

В следующем коде показан пример получения сообщения:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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
    "text": "Hello Teams TestBot.Sending bold-italic rich text",
    "attachments": [
      {
            "contentType": "text/html",
            "content": "<div><div>Hello Teams TestBot. Sending <strong>bold</strong>-<em>italic</em> rich text.</div>\n</div>"
      } 
    ],
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

Чтобы отправить текстовое сообщение, укажите строку, которая будет отправляться в качестве действия. В обработчике действий бота используйте `SendActivityAsync` метод объекта контекста шага для отправки одного ответа на сообщение. Используйте метод объекта для `SendActivitiesAsync` отправки нескольких ответов одновременно.

В следующем коде показан пример отправки сообщения при добавлении пользователя в беседу:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

    this.onMembersAddedActivity(async (context, next) => {
        await Promise.all((context.activity.membersAdded || []).map(async (member) => {
            if (member.id !== context.activity.recipient.id) {
                await context.sendActivity(
                    `Welcome to the team ${member.givenName} ${member.surname}`
                );
            }
        }));

        await next();
    });
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
    "type": "message",
    "from": {
        "id": "28:c9e8c047-2a34-40a1-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "conversation": {
        "id": "a:17I0kl8EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-",
        "name": "Convo1"
   },
   "recipient": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB25ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen"
    },
    "text": "My bot's reply",
    "replyToId": "1632474074231"
}

```

---

> [!NOTE]
> Разделение сообщений происходит, когда текстовое сообщение и вложение отправляются в тех же полезных данных действия. Это действие разбивается на отдельные действия по Microsoft Teams, одно с текстовым сообщением, а другое с вложением. При разделении действия идентификатор сообщения в ответе не получается, который используется для упреждающего обновления [](~/bots/how-to/update-and-delete-bot-messages.md) или удаления сообщения. Рекомендуется отправлять отдельные действия, а не в зависимости от разделения сообщений.

Сообщения, отправляемые между пользователями и ботами, включают внутренние данные канала в сообщении. Эти данные позволяют боту правильно обмениваться данными по этому каналу. Пакет SDK Bot Builder позволяет изменять структуру сообщений.

## <a name="teams-channel-data"></a>Данные канала Teams

Объект `channelData` содержит Teams сведениях, связанных с определенными данными, и является окончательным источником идентификаторов команд и каналов. При необходимости можно кэшировать и использовать эти идентификаторы в качестве ключей для локального хранилища. Пакет `TeamsActivityHandler` SDK извлекет важные сведения из `channelData` объекта, чтобы сделать его доступным. Однако вы всегда можете получить доступ к исходным данным из `turnContext` объекта.

Объект `channelData` не включается в сообщения в личных беседах, так как они имеют место за пределами канала.

Типичный `channelData` объект в действии, отправляемом боту, содержит следующие сведения:

* `eventType`: Teams передается только в случае событий [изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `tenant.id`: Microsoft Azure Active Directory (Azure AD) идентификатор клиента, переданный во всех контекстах.
* `team`: передается только в контекстах канала, а не в личном чате.
  * `id`: GUID для канала.
  * `name`: имя команды, переданное только в случае [переименования команды](subscribe-to-conversation-events.md#team-renamed).
* `channel`: передается только в контекстах каналов, когда упоминается бот, или для событий в каналах в командах, в которых был добавлен бот.
  * `id`: GUID для канала.
  * `name`: имя канала передается только в случае [событий изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`: не рекомендуется. Это свойство включено только для обеспечения обратной совместимости.
* `channelData.teamsChannelId`: не рекомендуется. Это свойство включено только для обеспечения обратной совместимости.

### <a name="example-channeldata-object-channelcreated-event"></a>Пример объекта channelData (событие channelCreated)

В следующем коде показан пример объекта channelData:

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

Сообщения, полученные от бота или отправленные в него, могут содержать различные типы содержимого сообщений.

| Формат    | От пользователя к боту | От бота к пользователю | Примечания                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Форматированный текст  | ✔                | ✔                | Бот может отправлять форматированный текст, изображения и карточки. Пользователи могут отправлять боту форматированный текст и изображения.                                                                                        |
| Изображения  | ✔                | ✔                | Максимум 1024×1024 МБ и 1 МБ в формате PNG, JPEG или GIF. Анимированный GIF-файл не поддерживается.  |
| Карточки     | ✖                | ✔                | Сведения о [поддерживаемых Teams](~/task-modules-and-cards/cards/cards-reference.md) см. в справочнике по Teams карточки. |
| Эмодзи    | ✔                | ✔                | Teams в настоящее время поддерживает эмодзи через UTF-16, например U+1F600 для усинхронного распознавания лиц. |

## <a name="notifications-to-your-message"></a>Уведомления в сообщении

Вы также можете добавить уведомления в сообщение с помощью свойства `Notification.Alert` . Уведомления предупреждают пользователей о новых задачах, упоминаниях и комментариях. Эти оповещения связаны с тем, над чем работают пользователи или что они должны просмотреть, вставив уведомление в веб-канал активности. Чтобы уведомления запускались из сообщения бота, задайте `TeamsChannelData` для свойства объектов `Notification.Alert` значение *true*. Независимо от того, создается ли уведомление, зависит от параметров Teams пользователя, и вы не можете переопределить эти параметры. Тип уведомления — это либо баннер, либо баннер и сообщение электронной почты.

> [!NOTE]
> В **поле "Сводка** " в веб-канале отображается любой текст от пользователя в виде уведомления.

В следующем коде показан пример добавления уведомлений в сообщение:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Чтобы улучшить сообщение, в него можно добавить изображения в виде вложений.

## <a name="picture-messages"></a>Сообщения с картинкой

Картинки отправляются путем добавления вложений к сообщению. Дополнительные сведения о вложениях см. в [разделе "Добавление вложений мультимедиа в сообщения"](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).

Изображения могут иметь не более 1024×1024 МБ и 1 МБ в формате PNG, JPEG или GIF. Анимированный GIF-файл не поддерживается.

Укажите высоту и ширину каждого изображения с помощью XML. В markdown размер изображения по умолчанию — 256×256. Например:

* Использование: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.
* Не используйте: `![Duck on a rock](http://aka.ms/Fo983c)`.

Чат-бот может включать адаптивные карточки, упрощающие бизнес-процессы. Адаптивные карточки предлагают форматированный настраиваемый текст, речь, изображения, кнопки и поля ввода.

## <a name="adaptive-cards"></a>Адаптивные карточки

Адаптивные карточки можно создавать в боте и отображать в нескольких приложениях, таких как Teams, веб-сайт и т. д. Дополнительные сведения см. в разделе [Адаптивные карточки](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).

В следующем коде показан пример отправки простой адаптивной карточки:

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

### <a name="form-completion-feedback"></a>Отзывы о завершении формы

Сообщение о завершении формы отображается в адаптивных карточках при отправке ответа боту. Сообщение может иметь два типа: ошибка или успешное выполнение:

* **Ошибка**. Если ответ, отправленный боту, неуспешно, **что-то пошло не так, появится сообщение "Повторить** попытку".

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="Сообщение об ошибке"border="true":::

* **Успешно**. Когда ответ, отправленный боту, будет успешно отправлен, появится ваш ответ **на сообщение** приложения.

:::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="Сообщение об успешном выполнении"border="true":::

Вы можете закрыть **или** переключить чат, чтобы закрыть сообщение.

**Ответ на мобильных устройствах**:

Сообщение об ошибке отображается в нижней части адаптивной карточки.

Дополнительные сведения о карточках и карточках в ботах см. в [документации по карточкам](~/task-modules-and-cards/what-are-cards.md).

## <a name="status-code-responses"></a>Ответы на код состояния

Ниже приведены коды состояния и их код ошибки и значения сообщений:

| Код состояния | Код ошибки и значения сообщений | Описание |
|----------------|-----------------|-----------------|
| 403 | **Код**: `ConversationBlockedByUser` <br/> **Сообщение**: пользователь заблокируют беседу с ботом. | Пользователь заблокирует бота в чате 1:1 или канале с помощью параметров модерации. |
| 403 | **Код**: `BotNotInConversationRoster` <br/> **Сообщение**: бот не входит в список бесед. | Бот не является частью беседы. |
| 403 | **Код**: `BotDisabledByAdmin` <br/> **Сообщение**: администратор клиента отключает этот бот. | Клиент заблокируют бот. |
| 401 | **Код**: `BotNotRegistered` <br/> **Сообщение**: регистрация для этого бота не найдена. | Регистрация этого бота не найдена. |
| 412 | **Код**: `PreconditionFailed` <br/> **Сообщение**: Сбой предварительного условия. Повторите попытку. | Не удалось выполнить предусловие для одной из наших зависимостей из-за нескольких параллельных операций в одной беседе. |
| 404 | **Код**: `ConversationNotFound` <br/> **Сообщение**: беседа не найдена. | Беседа не найдена. |
| 413 | **Код**: `MessageSizeTooBig` <br/> **Сообщение**: слишком большой размер сообщения. | Размер входящего запроса был слишком большим. |
| 429 | **Код**: `Throttled` <br/> **Сообщение**: слишком много запросов. Также возвращает время повторной попытки. | Бот отправил слишком много запросов. Дополнительные сведения см. в [разделе "Ограничение скорости"](~/bots/how-to/rate-limit.md). |

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Бот для беседы в Teams | Обработка сообщений и бесед. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Меню команд бота](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>См. также

* [Отправка упреждающих сообщений](~/bots/how-to/conversations/send-proactive-messages.md)
* [Подписка на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Отправка и получение файлов с помощью ботов](~/bots/how-to/bots-filesv4.md)
* [Отправка идентификатора клиента и идентификатора беседы в заголовки запросов бота](~/bots/how-to/conversations/request-headers-of-the-bot.md)
