---
title: Создать и отправить модуль задачи
author: clearab
description: Обработка действия первоначального вызова и реагирование с помощью модуля задачи из команды расширения сообщения о действии
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072877"
---
# <a name="create-and-send-the-task-module"></a>Создать и отправить модуль задачи

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Если вы не заполняете модуль задачи параметрами, определенными в манифесте приложения, необходимо создать модуль задачи для пользователей. Используйте адаптивную карточку или внедренное представление веб-страницы.

## <a name="the-initial-invoke-request"></a>Начальный запрос на вызов

С помощью этого метода служба получит объект типа, и вам необходимо ответить объектом, содержащим адаптивную карту или URL-адрес внедренного представления `Activity` `composeExtension/fetchTask` `task` веб-страницы. Помимо стандартных свойств активности бота, полезные данные начального вызова содержат следующие метаданные запроса:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должен быть `invoke` . |
|`name`| Тип команды, выдаемой службе. Это должен быть `composeExtension/fetchTask` . |
|`from.id`| ИД пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| ИД объекта Azure Active Directory пользователя, который отправил запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| ИД канала (если запрос был сделан в канале). |
|`channelData.team.id`| ИД команды (если запрос был сделан в канале). |
|`value.commandId` | Содержит ИД вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренного представления веб-страницы. Это должен `default` быть или `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a>В следующем разделе перечислены свойства действий полезных нагрузки при вызове модуля задачи из чата 1:1:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должен быть `invoke` . |
|`name`| Тип команды, выдаемой службе. Это должен быть `composeExtension/fetchTask` . |
|`from.id`| ИД пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| ИД объекта Azure Active Directory пользователя, который отправил запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Получает или задает ИД сообщения, на которое отправляется ответ. |
|`value.commandId` | Содержит ИД вызываемой команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должен быть `compose` . |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренного представления веб-страницы. Это должен `default` быть или `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a>Свойства действия полезных нагрузки при вызове модуля задачи из группового чата перечислены в следующем разделе:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должен быть `invoke` . |
|`name`| Тип команды, выдаемой службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ИД пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| ИД объекта Azure Active Directory пользователя, который отправил запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Получает или задает ИД сообщения, на которое отправляется ответ. |
|`value.commandId` | Содержит ИД вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренного представления веб-страницы. Это должен `default` быть или `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a>Свойства активности полезных нагрузки при вызове модуля задачи из канала (новая публикация) перечислены в следующем разделе:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должен быть `invoke` . |
|`name`| Тип команды, выдаемой службе. Это должен быть `composeExtension/fetchTask` . |
|`from.id`| ИД пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| ИД объекта Azure Active Directory пользователя, который отправил запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| ИД канала (если запрос был сделан в канале). |
|`channelData.team.id`| ИД команды (если запрос был сделан в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Получает или задает ИД сообщения, на которое отправляется ответ. |
|`value.commandId` | Содержит ИД вызываемой команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должен быть `compose` . |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренного представления веб-страницы. Это должен `default` быть или `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a>Свойства активности полезных нагрузки при вызове модуля задачи из канала (ответ на поток) перечислены в следующем разделе:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должен быть `invoke` . |
|`name`| Тип команды, выдаемой службе. Это должно быть `composeExtension/fetchTask` . |
|`from.id`| ИД пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| ИД объекта Azure Active Directory пользователя, который отправил запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.channel.id`| ИД канала (если запрос был сделан в канале). |
|`channelData.team.id`| ИД команды (если запрос был сделан в канале). |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`ChannelData.legacy. replyToId`| Получает или задает ИД сообщения, на которое отправляется ответ. |
|`value.commandId` | Содержит ИД вызываемой команды. |
|`value.commandContext` | Контекст, который инициирует событие. Это должен быть `compose` . |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренного представления веб-страницы. Это должен `default` быть или `contrast` `dark` . |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a>Свойства активности полезных нагрузки при вызове модуля задачи из командного окна перечислены в следующем разделе:

|Имя свойства|Назначение|
|---|---|
|`type`| Тип запроса. Это должно быть `invoke` . |
|`name`| Тип команды, выдаемой службе. Это должен быть `composeExtension/fetchTask` . |
|`from.id`| ИД пользователя, отправив запрос. |
|`from.name`| Имя пользователя, отправив запрос. |
|`from.aadObjectId`| ИД объекта Azure Active Directory пользователя, который отправил запрос. |
|`channelData.tenant.id`| Идентификатор клиента Azure Active Directory. |
|`channelData.source.name`| Имя источника, из которого вызывается модуль задачи. |
|`value.commandId` | Содержит ИД вызываемой команды. |
|`value.commandContext` | Контекст, который вызвал событие. Это должно быть `compose` . |
|`value.context.theme` | Тема клиента пользователя, полезная для форматирования внедренного представления веб-страницы. Это должен `default` быть или `contrast` `dark` . |

### <a name="example-fetchtask-request"></a>Пример запроса fetchTask

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
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
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>Исходный запрос на вызов из сообщения

Когда бот вызывается из сообщения, а не области составить или панели команд, объект в исходном запросе должен содержать сведения о сообщении, из которых вызывается расширение обмена `value` сообщениями. Пример этого объекта см. в следующем разделе. Массивы и массивы являются необязательными и не присутствуют, если в исходном сообщении нет реакции или `reactions` `mentions` упоминаний.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>Ответ на fetchTask

Ответьте на запрос на вызов с помощью объекта, который содержит объект с адаптивной карточкой или URL-адресом веб-страницы, или `task` `taskInfo` простого строки сообщения.

|Имя свойства|Назначение|
|---|---|
|`type`| Может представлять форму или для `continue` `message` простого всплывающее всплывающее окна. |
|`value`| Либо `taskInfo` объект для формы, либо объект a `string` для сообщения. |

Схема объекта taskInfo:

|Имя свойства|Назначение|
|---|---|
|`title`| Заголовок модуля задачи.|
|`height`| Это должно быть либо integer (в пикселях), либо `small` `medium` , `large` .|
|`width`| Это должно быть либо integer (в пикселях), либо `small` `medium` , `large` .|
|`card`| Адаптивная карточка, определяющая форму (если она используется).
|`url`| URL-адрес, открываемый внутри модуля задачи в качестве внедренного представления веб-страницы.|
|`fallbackUrl`| Если клиент не поддерживает функцию модуля задачи, этот URL-адрес открывается на вкладке браузера. |

### <a name="with-an-adaptive-card"></a>С помощью адаптивной карточки

При использовании адаптивной карточки необходимо ответить объектом, содержащим `task` `value` адаптивную карточку.

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a>Пример отклика fetchTask с адаптивной картой

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

В этом примере помимо пакета Bot Framework SDK используется пакет [AdaptiveCards NuGet.](https://www.nuget.org/packages/AdaptiveCards)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a>С внедренным представлением веб-страницы

При использовании внедренного представления веб-страницы необходимо ответить объектом, содержащим URL-адрес веб-формы, который вы `task` `value` хотите загрузить. Домены любого URL-адреса, который требуется загрузить, должны быть включены в массив `validDomains` манифеста приложения. Полные [сведения о создании](~/task-modules-and-cards/what-are-task-modules.md) внедренного представления веб-страницы см. в документации по модулям задач.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a>Запрос на установку бота для беседы

Если приложение содержит бота для беседы, установите бота в беседе перед загрузкой модуля задачи. Полезно получить дополнительный контекст для модуля задачи. Типичный пример этого сценария — получить список для заполнения управления "Выбор людей" или списка каналов в команде.

Когда расширение обмена сообщениями получает вызов, проверьте, установлен ли бот в текущем контексте для `composeExtension/fetchTask` упрощения потока. Например, проверьте поток с помощью вызова получения составов. Если бот не установлен, возвращает адаптивную карточку с действием, которое запрашивает у пользователя установку бота. См. действие в следующем примере. У пользователя должно быть разрешение на установку приложений в этом расположении для проверки. Если установка приложения неуспешна, пользователь получает сообщение для связи с администратором.

#### <a name="example-of-the-response"></a>Пример ответа:

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

После установки бот получает еще одно сообщение об вызове `name = composeExtension/submitAction` с и `value.data.msteams.justInTimeInstall = true` .

#### <a name="example-of-the-invoke"></a>Пример вызова:

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

Ответ задачи на вызов должен быть похож на ответ установленного бота.

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a>Пример установки приложения с адаптивной картой во времени: 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="next-steps"></a>Дальнейшие действия

Если вы разрешаете пользователям отправлять ответ из модуля задачи, необходимо обработать действие отправки.

* [Создание модуля задачи и реагирование на него](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
