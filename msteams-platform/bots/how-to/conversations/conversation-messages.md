---
title: Сообщения в беседах с ботами
description: Узнайте, как отправлять сообщения, рекомендуемые действия, уведомления, вложения, изображения, адаптивную карточку и ответы об ошибках состояния.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 16849a9e8ed97854e91934aef9de463eb355fec5
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833207"
---
# <a name="messages-in-bot-conversations"></a>Сообщения в беседах с ботами

Каждое сообщение в беседе `Activity` является объектом типа `messageType: message`. Когда пользователь отправляет сообщение, Microsoft Teams публикует его боту. Teams отправляет объект JSON в конечную точку обмена сообщениями бота, а Teams разрешает только одну конечную точку для обмена сообщениями. Бот проверяет сообщение, чтобы определить его тип и ответить соответствующим образом.

Основные беседы обрабатываются через соединитель Bot Framework, один REST API. Этот API позволяет боту взаимодействовать с Teams и другими каналами. Пакет SDK Bot Builder предоставляет следующие возможности:

* Простой доступ к соединителю Bot Framework.
* Функциональные возможности для управления потоком и состоянием беседы.
* Простые способы внедрения когнитивных служб, такие как обработка естественного языка (NLP).

Бот получает сообщения из Teams с помощью `Text` свойства и отправляет пользователям один или несколько ответов на сообщения.

Дополнительные сведения см. [в разделе атрибуция пользователей для сообщений бота](/microsoftteams/platform/messaging-extensions/how-to/action-commands/respond-to-task-module-submit?tabs=dotnet%2Cdotnet-1&branch=pr-en-us-5926#user-attribution-for-bots-messages).

## <a name="receive-a-message"></a>Получение сообщения

Чтобы получить текстовое `Text` сообщение, используйте свойство `Activity` объекта . В обработчике активности бота используйте объект контекста поворота `Activity` для чтения одного запроса сообщения.

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

Чтобы отправить текстовое сообщение, укажите строку, которую нужно отправить в качестве действия. В обработчике действий бота используйте метод объекта контекста поворота `SendActivityAsync` для отправки одного ответа сообщения. Используйте метод объекта для отправки `SendActivitiesAsync` нескольких ответов.

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
>
>* Разделение сообщений происходит, когда текстовое сообщение и вложение отправляются в одной и той же полезной нагрузке действия. Teams разделяет это действие на два отдельных действия: одно с текстовым сообщением, а другое с вложением. Так как действие разделено, вы не получаете в ответ идентификатор сообщения, который используется для упреждающего [обновления или удаления](~/bots/how-to/update-and-delete-bot-messages.md) сообщения. Вместо разбиения сообщений рекомендуется отправлять отдельные действия.
>* Отправленные сообщения можно локализовать для обеспечения персонализации. Дополнительные сведения см. в статье [Локализация приложения](../../../concepts/build-and-test/apps-localization.md).

Сообщения, отправляемые между пользователями и ботами, включают в себя данные внутреннего канала в сообщении. Эти данные позволяют боту правильно взаимодействовать по этому каналу. Пакет SDK Bot Builder позволяет изменять структуру сообщений.

## <a name="send-suggested-actions"></a>Отправка предлагаемых действий

Предлагаемые действия позволяют боту предоставлять кнопки, которые пользователь может выбрать для ввода данных. Предлагаемые действия улучшают взаимодействие с пользователем, позволяя пользователю отвечать на вопрос или делать выбор с помощью кнопки, а не вводить ответ с помощью клавиатуры.
Когда пользователь нажимает кнопку, она остается видимой и доступной в расширенных карточках, но не для предлагаемых действий. Это не позволяет пользователю выбирать устаревшие кнопки в беседе.

Чтобы добавить предлагаемые действия в сообщение, задайте `suggestedActions` свойство объекта [действия](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) , чтобы указать список объектов [действия с карточками](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference) , которые представляют кнопки, которые будут представлены пользователю. Дополнительную информацию см. в статье [`sugestedActions`](/dotnet/api/microsoft.bot.builder.messagefactory.suggestedactions).

Ниже приведен пример реализации и опыта предлагаемых действий.

``` json
"suggestedActions": {
    "actions": [
      {
        "type": "imBack",
        "title": "Action 1",
        "value": "Action 1"
      },
      {
        "type": "imBack",
        "title": "Action 2",
        "value": "Action 2"
      }
    ],
    "to": [<list of recepientIds>]
  }
```

Ниже показан пример предлагаемых действий.

:::image type="content" source="~/assets/images/Cards/suggested-actions.png" alt-text="Действия, предлагаемые ботом" border="true":::

> [!NOTE]
>
> * `SuggestedActions` поддерживаются только для чат-ботов и текстовых сообщений, но не для адаптивных карточек или вложений.
> * `imBack` — это единственный поддерживаемый тип действия, и Teams отображает до трех предлагаемых действий.

## <a name="teams-channel-data"></a>Данные канала Teams

Объект `channelData` содержит сведения, относящиеся к Teams, и является окончательным источником идентификаторов команд и каналов. При необходимости эти идентификаторы можно кэшировать и использовать в качестве ключей для локального хранилища. В `TeamsActivityHandler` пакете SDK извлекает из `channelData` объекта важную информацию, чтобы сделать его доступным. Однако вы всегда можете получить доступ к исходным данным из `turnContext` объекта .

Объект `channelData` не включается в сообщения в личных беседах, так как они происходят за пределами канала.

Типичный `channelData` объект в действии, отправляемом боту, содержит следующие сведения:

* `eventType`: тип события Teams передается только в случаях [изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `tenant.id`: Microsoft Azure Active Directory (Azure AD) идентификатор клиента передается во всех контекстах.
* `team`: передается только в контекстах канала, а не в личном чате.
  * `id`: GUID для канала.
  * `name`: имя команды, переданное только в случаях [переименования команды](subscribe-to-conversation-events.md#team-renamed).
* `channel`: передается только в контекстах каналов, когда упоминается бот, или для событий в каналах в командах, где бот был добавлен.
  * `id`: GUID для канала.
  * `name`: имя канала передается только в случаях [изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`:Устаревшие. Это свойство включается только для обеспечения обратной совместимости.
* `channelData.teamsChannelId`:Устаревшие. Это свойство включается только для обеспечения обратной совместимости.

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

Сообщения, полученные ботом или отправляемые ей, могут содержать различные типы содержимого сообщений.

| Формат    | От пользователя к боту | От бота к пользователю | Примечания                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Форматированный текст  | ✔️                | ✔️                | Бот может отправлять форматированный текст, изображения и карточки. Пользователи могут отправлять боту форматированный текст и изображения.                                                                                        |
| Изображения  | ✔️                | ✔️                | Максимум 1024 × 1024 пикселя и 1 МБ в формате PNG, JPEG или GIF. Не поддерживает анимированный GIF-файл. |
| Карточки     | ❌                | ✔️                | Сведения о поддерживаемых карточках см. [в статье Справочник по карточкам Teams](~/task-modules-and-cards/cards/cards-reference.md) . |
| Эмодзи    | ✔️                | ✔️                | В настоящее время Teams поддерживает эмодзи через UTF-16, например U+1F600 для улыбки лица. |

### <a name="picture-messages"></a>Сообщения с картинкой

Чтобы улучшить сообщение, можно добавить изображения в виде вложений в это сообщение. Дополнительные сведения о вложениях см. в статье [Добавление мультимедийных вложений в сообщения](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).

Изображения могут иметь не более 1024 × 1024 пикселей и 1 МБ в формате PNG, JPEG или GIF. GIF с анимацией не поддерживается.

Укажите высоту и ширину каждого изображения с помощью XML. В Markdown размер изображения по умолчанию — 256×256. Например:

* Используйте: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.
* Не используйте: `![Duck on a rock](http://aka.ms/Fo983c)`.

Бот беседы может включать адаптивные карточки, которые упрощают бизнес-процессы. Адаптивные карточки предоставляют расширенные настраиваемые текст, речь, изображения, кнопки и поля ввода.

### <a name="adaptive-cards"></a>Адаптивные карточки

Адаптивные карточки можно создать в боте и отображать в нескольких приложениях, таких как Teams, ваш веб-сайт и т. д. Дополнительные сведения см. в разделе [Адаптивные карточки](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).

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

#### <a name="form-completion-feedback"></a>Отзывы о завершении формы

Вы можете создать отзыв о заполнении формы с помощью адаптивной карточки. Сообщение о завершении формы отображается в адаптивных карточках при отправке ответа боту. Сообщение может быть двух типов: ошибка или успешное выполнение:

* **Ошибка**. Если ответ, отправленный боту, неуспешен, **что-то пошло не так, появится сообщение Повторите попытку** .

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="Сообщение об ошибке"border="true":::

* **Успешно**. При успешном выполнении ответа, отправленного боту, **появится сообщение о том, что ваш ответ отправлен в приложение** .

     :::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="Сообщение об успешном выполнении"border="true":::

     Вы можете **выбрать Закрыть** или переключить чат, чтобы закрыть сообщение.

     Если вы не хотите отображать сообщение об успешном выполнении, задайте атрибуту `hide` значение `true` в свойстве `msTeams` `feedback` . Ниже приведен пример:

     ```json
        "content": {
            "type": "AdaptiveCard",
            "title": "Card with hidden footer messages",
            "version": "1.0",
            "actions": [
            {
                "type": "Action.Submit",
                "title": "Submit",
                "msTeams": {
                    "feedback": {
                    "hide": true
                    }
                }
            }
            ]
        } 
     ```

Дополнительные сведения о карточках и карточках в ботах см. в [документации по карточкам](~/task-modules-and-cards/what-are-cards.md).

## <a name="add-notifications-to-your-message"></a>Добавление уведомлений в сообщение

Отправить уведомление из приложения можно двумя способами:

* Задав свойство в `Notification.Alert` сообщении бота.
* Отправляя уведомление веб-канала действий с помощью API Graph.

Вы можете добавить уведомления в сообщение с помощью `Notification.Alert` свойства . Уведомления оповещают пользователей о событии в приложении, например о новых задачах, упоминаниях или комментариях. Эти оповещения связаны с тем, над чем работают пользователи или что они должны смотреть, вставляя уведомление в веб-канал действий. Чтобы уведомления активируются из сообщения бота `TeamsChannelData` , задайте для свойства objects `Notification.Alert` *значение true*. Если возникает уведомление, это зависит от параметров Teams отдельного пользователя, и вы не можете переопределить эти параметры.

Если вы хотите создать произвольное уведомление, не отправляя пользователю сообщение, можно использовать API Graph. Дополнительные сведения см. в статье [Отправка уведомлений веб-канала действий с помощью API Graph](/graph/teams-send-activityfeednotifications), а также [рекомендации](/graph/teams-activity-feed-notifications-best-practices).

> [!NOTE]
> В поле **Сводка** отображается любой текст от пользователя в виде уведомления в веб-канале.

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

## <a name="status-codes-from-bot-conversational-apis"></a>Коды состояния из интерфейсов API бесед бота

Обеспечьте соответствующую обработку этих ошибок в приложении Teams. В следующей таблице перечислены коды ошибок и описания, по которым создаются ошибки.

| Код состояния | Код ошибки и значения сообщений | Описание | Повторный запрос | Действие разработчика |
|----------------|-----------------|-----------------|----------------|----------------|
| 400 | **Код**: `Bad Argument` <br/> **Сообщение**: *сценарий | Недопустимые полезные данные запроса, предоставляемые ботом. Дополнительные сведения см. в сообщении об ошибке. | Нет | Повторно оцените полезные данные запроса на наличие ошибок. Проверьте возвращенное сообщение об ошибке для получения дополнительных сведений. |
| 401 | **Код**: `BotNotRegistered` <br/> **Сообщение**. Регистрация для этого бота не найдена. | Регистрация этого бота не найдена. | Нет | Проверьте идентификатор и пароль бота. Убедитесь, что идентификатор бота (идентификатор AAD) зарегистрирован на портале разработчика Teams или через регистрацию канала бота Azure в Azure с включенным каналом Teams.|
| 403 | **Код**: `BotDisabledByAdmin` <br/> **Сообщение**. Администратор клиента отключил этот бот | Администратор клиента заблокировал взаимодействие между пользователем и приложением бота. Администратор клиента должен разрешить использование приложения для пользователя в политиках приложений. Дополнительные сведения см. в разделе [Политики приложений](/microsoftteams/app-policies). | Нет | Остановите публикацию в беседе, пока пользователь явно не инициирует взаимодействие с ботом, указывая, что бот больше не заблокирован. |
| 403 | **Код**: `BotNotInConversationRoster` <br/> **Сообщение**. Бот не входит в список бесед. | Бот не является частью беседы. Приложение необходимо переустановить в беседе. | Нет | Перед отправкой другого запроса на беседу [`installationUpdate`](~/bots/how-to/conversations/subscribe-to-conversation-events.md#install-update-event) подождите событие, указывающее на то, что бот был добавлен повторно.|
| 403 | **Код**: `ConversationBlockedByUser` <br/> **Сообщение**. Пользователь заблокировал беседу с ботом. | Пользователь заблокировал бот в личном чате или канале с помощью параметров модерации. | Нет | Удалите беседу из кэша. Остановите попытки публикации в беседах, пока пользователь явно не инициирует взаимодействие с ботом, указывая, что бот больше не заблокирован. |
| 403 |**Код**: `InvalidBotApiHost` <br/> **Сообщение**: Недопустимый узел API бота. Для клиентов GCC позвоните по телефону `https://smba.infra.gcc.teams.microsoft.com`.|Бот назвал общедоступную конечную точку API для беседы, которая принадлежит клиенту GCC.| Нет | Обновите URL-адрес службы для беседы `https://smba.infra.gcc.teams.microsoft.com` и повторите запрос.|
| 403 | **Код**: `NotEnoughPermissions` <br/> **Сообщение**: *сценарий | У бота нет необходимых разрешений для выполнения запрошенного действия. | Нет | Определите требуемое действие из сообщения об ошибке. |
| 404 | **Код**: `ActivityNotFoundInConversation` <br/> **Сообщение**: беседа не найдена. | Указанный идентификатор сообщения не найден в беседе. Сообщение не существует или оно удалено. | Нет | Проверьте, является ли идентификатор отправленного сообщения ожидаемым значением. Удалите идентификатор, если он был кэширован. |
| 404 | **Код**: `ConversationNotFound` <br/> **Сообщение**: беседа не найдена. | Беседа не найдена, так как она не существует или была удалена. | Нет | Проверьте, является ли отправленный идентификатор беседы ожидаемым значением. Удалите идентификатор, если он был кэширован. |
| 412 | **Код**: `PreconditionFailed` <br/> **Сообщение**. Сбой предварительного условия, повторите попытку. | Сбой предварительного условия для одной из зависимостей из-за нескольких одновременных операций в одном диалоге. | Да | Повторите попытку с экспоненциальной задержкой. |
| 413 | **Код**: `MessageSizeTooBig` <br/> **Сообщение**: слишком большой размер сообщения. | Размер входящего запроса был слишком велик. Дополнительные сведения см. в разделе [Форматирование сообщений бота](/microsoftteams/platform/bots/how-to/format-your-bot-messages). | Нет | Уменьшите размер полезных данных. |
| 429 | **Код**: `Throttled` <br/> **Сообщение**: Слишком много запросов. Также возвращает время повторной попытки после. | Бот отправил слишком много запросов. Дополнительные сведения см. в разделе [Ограничение скорости](/microsoftteams/platform/bots/how-to/rate-limit). | Да | Повторите попытку с помощью `Retry-After` заголовка для определения времени отката. |
| 500 | **Код**: `ServiceError` <br/> **Сообщение**: *различные | Внутренняя ошибка сервера. | Нет | Сообщите о проблеме в [сообществе разработчиков](~/feedback.md#developer-community-help). |
| 502 | **Код**: `ServiceError` <br/> **Сообщение**: *различные | Проблема с зависимостью службы. | Да | Повторите попытку с экспоненциальной задержкой. Если проблема не исчезнет, сообщите о ней в [сообществе разработчиков](~/feedback.md#developer-community-help). |
| 503 | | Служба недоступна. | Да | Повторите попытку с экспоненциальной задержкой. Если проблема не исчезнет, сообщите о ней в [сообществе разработчиков](~/feedback.md#developer-community-help). |
| 504 | | Время ожидания шлюза. | Да | Повторите попытку с экспоненциальной задержкой. Если проблема не исчезнет, сообщите о ней в [сообществе разработчиков](~/feedback.md#developer-community-help). |

### <a name="status-codes-retry-guidance"></a>Руководство по повторным попыткам кодов состояния

Общие рекомендации по повторным попыткам для каждого кода состояния перечислены в следующей таблице. Бот должен избегать повторных попыток кодов состояния, которые не указаны:

|Код состояния | Стратегия повторных попыток |
|----------------|-----------------|
| 403 | Повторите попытку, вызвав API `https://smba.infra.gcc.teams.microsoft.com` GCC для `InvalidBotApiHost`.|
| 412 | Повторите попытку с экспоненциальной задержкой. |
| 429 | Повторите попытку с помощью `Retry-After` заголовка для определения времени ожидания в секундах и между запросами, если они доступны. В противном случае повторите попытку с экспоненциальной задержкой с идентификатором потока, если это возможно. |
| 502 | Повторите попытку с экспоненциальной задержкой. |
| 503 | Повторите попытку с экспоненциальной задержкой. |
| 504 | Повторите попытку с экспоненциальной задержкой. |

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | Node.js | .NETCore | Python | .NET |
|----------------|-----------------|--------------|----------------|-----------|-----|
| Бот для беседы в Teams | Обработка сообщений и бесед. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) | Н/Д |
| Локализация приложений Teams | Локализация приложений Teams с помощью бота и вкладки. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) | Недоступно | Недоступно | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Меню команд бота](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>См. также

* [Отправка упреждающих сообщений](~/bots/how-to/conversations/send-proactive-messages.md)
* [Подписка на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Отправка и получение файлов с помощью ботов](~/bots/how-to/bots-filesv4.md)
* [Отправка идентификатора клиента и идентификатора беседы в заголовки запросов бота](~/bots/how-to/conversations/request-headers-of-the-bot.md)
* [Локализация приложения](../../../concepts/build-and-test/apps-localization.md)
