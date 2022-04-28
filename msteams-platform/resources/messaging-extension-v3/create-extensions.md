---
title: Запуск действий с расширениями сообщений
description: Создание расширений сообщений на основе действий, позволяющих пользователям активировать внешние службы
ms.localizationpriority: medium
ms.topic: how-to
keywords: Поиск расширений сообщений teams
ms.openlocfilehash: a29d1a5b49845d930ac4efbdd3967bd6b4446891
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104372"
---
# <a name="initiate-actions-with-message-extensions"></a>Запуск действий с расширениями сообщений

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширения сообщений на основе действий позволяют пользователям активировать действия во внешних службах в Teams.

![Пример карточки расширения сообщения](~/assets/images/compose-extensions/ceexample.png)

В следующих разделах описано, как это сделать.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="action-type-message-extensions"></a>Расширения сообщений типа действия

Чтобы инициировать действия из расширения сообщения, задайте для параметра `type` значение .`action` Ниже приведен пример манифеста с командой поиска и создания. Одно расширение сообщения может содержать до 10 разных команд. Это может включать как несколько команд поиска, так и несколько команд на основе действий.

### <a name="complete-app-manifest-example"></a>Полный пример манифеста приложения

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": false,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
              "inputType": "text"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a>Инициация действий из сообщений

Помимо инициации действий из области создания сообщений, вы также можете использовать расширение сообщения для инициации действия из сообщения. Это позволит отправить содержимое сообщения боту для обработки и при необходимости ответить на него ответом с помощью метода, описанного в разделе "Ответ на [отправку"](#responding-to-submit). Ответ будет вставлен в качестве ответа на сообщение, которое пользователи могут изменить перед отправкой. Пользователи могут получить доступ к расширению сообщения из меню переполнения `...` `Take action` , а затем выбрать его, как показано на следующем рисунке:

![Пример инициации действия из сообщения](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Чтобы расширение сообщения можно было использовать из сообщения, добавьте параметр в объект расширения сообщения в манифесте приложения, `context` `commands` как показано в следующем примере. Допустимые строки для массива`context`: `"message"`и `"compose"``"commandBox"`. Значение по умолчанию — `["compose", "commandBox"]`. Полные [сведения о параметре см](#define-commands)`context`. в разделе "Определение команд":

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

Ниже приведен пример объекта, содержащего `value` сведения о `composeExtension` сообщении, которые будут отправляться в рамках запроса, отправляемого боту.

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
        "content": "this is the message"
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

### <a name="test-via-uploading"></a>Тестирование с помощью отправки

Расширение сообщения можно протестировать, передав приложение. Дополнительные сведения см. [в статье "Отправка приложения в команду"](~/concepts/deploy-and-publish/apps-upload.md).

Чтобы открыть расширение сообщения, перейдите к любому из чатов или каналов. Нажмите **кнопку "Дополнительные** параметры **" (&#8943;**) в поле создания сообщения и выберите расширение сообщения.

## <a name="collecting-input-from-users"></a>Сбор входных данных от пользователей

Существует три способа сбора сведений от конечного пользователя в Teams.

### <a name="static-parameter-list"></a>Список статических параметров

В этом методе необходимо только определить статический список параметров в манифесте, как показано выше в команде "Список дел". Чтобы использовать этот метод, `fetchTask` убедитесь, что задано значение `false` и что параметры определены в манифесте.

Когда пользователь выбирает команду со статическими параметрами, Teams создает форму в модуле задач с определенными параметрами в манифесте. При нажатии клавиши Submit a `composeExtension/submitAction` отправляется боту. Дополнительные сведения о ожидаемом наборе ответов см. в [разделе "Ответ на отправку"](#responding-to-submit).

### <a name="dynamic-input-using-an-adaptive-card"></a>Динамический ввод с помощью адаптивной карточки

В этом методе служба может определить пользовательскую адаптивную карточку для сбора входных данных пользователя. Для этого подхода задайте параметр `fetchTask` в `true` манифесте. Если вы заданы, `fetchTask` `true` любые статические параметры, определенные для команды, будут игнорироваться.

В этом методе служба получает `composeExtension/fetchTask` событие и отвечает ответом модуля задачи на основе адаптивной [карточки](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object). Ниже приведен пример ответа с адаптивной карточкой:

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

Бот также может ответить ответом проверки подлинности или конфигурации, если пользователю необходимо выполнить проверку подлинности или настроить расширение перед получением входных данных пользователя.

### <a name="dynamic-input-using-a-web-view"></a>Динамический ввод с помощью веб-представления

В этом методе служба может отобразить мини-приложение `<iframe>` на основе, чтобы отобразить любой пользовательский интерфейс и собрать данные, введенные пользователем. Для этого подхода задайте параметр `fetchTask` в `true` манифесте.

Как и в потоке адаптивной карточки `fetchTask` , служба отправляет событие и отвечает ответом модуля задачи на основе [URL-адреса](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object). Ниже приведен пример ответа с адаптивной карточкой:

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a>Запрос на установку чат-бота

Если приложение содержит бот беседы, убедитесь, что оно установлено в беседе перед загрузкой модуля задачи. Это может быть полезно в ситуациях, когда необходимо получить дополнительный контекст для модуля задачи. Например, может потребоваться получить список, чтобы заполнить элемент управления выбора людей или список каналов в команде.

Чтобы упростить этот поток, когда расширение `composeExtension/fetchTask` сообщения впервые получает проверку на вызов, чтобы узнать, установлен ли бот в текущем контексте. Это можно получить, выполнив вызов get roster. Например, если бот не установлен, возвращается адаптивная карточка с действием, которое запрашивает у пользователя установку бота. Пользователь должен иметь разрешение на установку приложений в этом расположении. Если установить его не удается, в сообщении будет предложено обратиться к администратору.

Ниже приведен пример ответа.

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

Когда пользователь завершит установку, бот получит еще одно сообщение об вызове с и `name = composeExtension/submitAction``value.data.msteams.justInTimeInstall = true`.

Ниже приведен пример вызова:

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

Ответ на вызов с тем же ответом задачи, который вы бы ответили, если бот уже был установлен.

## <a name="responding-to-submit"></a>Реагирование на отправку

Когда пользователь завершит ввод входных данных, `composeExtension/submitAction` бот получит событие с заданными идентификатором команды и значениями параметров.

Это различные ожидаемые ответы на запрос `submitAction`.

### <a name="task-module-response"></a>Ответ модуля задач

Это используется, когда расширению необходимо объединить диалоги в цепочку, чтобы получить дополнительные сведения. Ответ точно такой же, как упоминалось `fetchTask` ранее.

### <a name="compose-extension-authconfig-response"></a>Ответ проверки подлинности или конфигурации расширения Compose

Это используется, когда расширению необходимо либо выполнить проверку подлинности, либо настроить для продолжения. Дополнительные сведения см. [в разделе проверки подлинности](~/resources/messaging-extension-v3/search-extensions.md#authentication) в разделе поиска.

### <a name="compose-extension-result-response"></a>Ответ на результат создания расширения

Он используется для вставки карточки в поле создания в результате выполнения команды. Это тот же ответ, который используется в команде поиска, но он ограничен одной карточкой или одним результатом в массиве.

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Ответ с помощью адаптивного сообщения карточки, отправленного от бота

Ответ на действие отправки путем вставки сообщения с адаптивной карточкой в канал с помощью бота. Пользователь может просмотреть сообщение перед его отправкой, а также, возможно, изменить или взаимодействовать с ним. Это может быть полезно в сценариях, в которых необходимо собрать сведения от пользователей перед созданием адаптивного ответа карточки. В следующем сценарии показано, как использовать этот поток для настройки опроса без указания шагов настройки в сообщении канала.

1. Пользователь выбирает расширение сообщения для активации модуля задачи.
1. Пользователь использует модуль задач для настройки опроса.
1. После отправки модуля задачи конфигурации приложение использует сведения, предоставленные в модуле задачи, `botMessagePreview` для создания адаптивной карточки и отправляет ее в качестве ответа клиенту.
1. Затем пользователь может просмотреть сообщение адаптивной карточки, прежде чем бот вставит его в канал. Если бот еще не является участником канала, `Send` при нажатии кнопки будет добавлен бот.
1. Взаимодействие с адаптивной картой изменит сообщение перед отправкой.
1. Когда пользователь выберет бота `Send` , он опубликует сообщение в канале.

Чтобы включить этот поток, модуль задачи должен ответить, как в приведенном ниже примере, который будет представлять пользователю сообщение предварительного просмотра.

>[!Note]
>Должен `activityPreview` содержать действие с `message` ровно 1 вложением адаптивной карточки.

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

Теперь расширение сообщения будет отвечать на два новых типа взаимодействий. `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` Ниже приведен пример объекта `value` , который необходимо обработать:

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

При ответе на запрос `edit` вы должны ответить ответом со значениями, `task` заполненными сведениями, которые пользователь уже отправил. При ответе на запрос `send` необходимо отправить сообщение в канал, содержащий завершенную адаптивную карточку.

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

В этом примере показан этот поток с помощью [Microsoft.Bot.Connector.Teams Пакет SDK (версия 3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```

## <a name="see-also"></a>См. также

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
