---
title: Инициировать действия с расширениями обмена сообщениями
description: Создание расширений обмена сообщениями на основе действий, позволяющих пользователям запускать внешние службы
ms.localizationpriority: medium
ms.topic: how-to
keywords: команды расширения обмена сообщениями расширениями обмена сообщениями поиска
ms.openlocfilehash: f028a26693eef03686ad6ad57423b30d4d861934
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157291"
---
# <a name="initiate-actions-with-messaging-extensions"></a>Инициировать действия с расширениями обмена сообщениями

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширения обмена сообщениями на основе действий позволяют пользователям запускать действия во внешних службах во время Teams.

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

В следующих разделах описано, как это сделать.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>Расширения сообщений типа действия

Чтобы инициировать действия из расширения обмена сообщениями, задан `type` параметр `action` . Ниже приведен пример манифеста с поиском и командой создания. Одно расширение обмена сообщениями может иметь до 10 различных команд. Это может включать как несколько команд поиска, так и несколько команд на основе действий.

#### <a name="complete-app-manifest-example"></a>Полный пример манифеста приложения

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
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
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

### <a name="initiate-actions-from-messages"></a>Инициировать действия из сообщений

Помимо инициации действий из области составить сообщение, вы также можете использовать расширение обмена сообщениями, чтобы инициировать действие из сообщения. Это позволит отправлять содержимое сообщения боту для обработки и необязательно отвечать на это сообщение ответом с помощью метода, описанного в ответе для [отправки.](#responding-to-submit) Ответ будет вставлен в качестве ответа на сообщение, которое пользователи могут изменить перед отправкой. Пользователи могут получить доступ к расширению обмена сообщениями из меню переполнения, а затем выбрать, `...` `Take action` как на следующем изображении:

![Пример инициирования действия из сообщения](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Чтобы расширение обмена сообщениями работало из сообщения, необходимо добавить параметр к объекту расширения обмена сообщениями в манифесте приложения, как в `context` `commands` примере ниже. Допустимые строки `context` для массива `"message"` являются , `"commandBox"` и `"compose"` . Значение по умолчанию — `["compose", "commandBox"]`. Подробные [сведения](#define-commands) о параметре см. в разделе Определить `context` команды.

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

Ниже приведен пример объекта, содержащего сведения о сообщении, которые будут отправлены в рамках запроса, `value` `composeExtension` отправленного вашему боту.

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

### <a name="test-via-uploading"></a>Тестирование с помощью загрузки

Вы можете протестировать расширение обмена сообщениями, загрузив приложение. Дополнительные сведения см. [в сайте Uploading your app in a team.](~/concepts/deploy-and-publish/apps-upload.md)

Чтобы открыть расширение обмена сообщениями, перейдите к любому из ваших чатов или каналов. Выберите **кнопку Дополнительные** параметры **(&#8943;)** в поле составить и выберите расширение обмена сообщениями.

## <a name="collecting-input-from-users"></a>Сбор входных данных от пользователей

Существует три способа сбора сведений от пользователя в Teams.

### <a name="static-parameter-list"></a>Список статических параметров

В этом методе необходимо определить статический список параметров манифеста, как показано выше в команде "Создание To Do". Для использования этого метода задана настройка и определение `fetchTask` `false` параметров в манифесте.

Когда пользователь выбирает команду со статичными параметрами, Teams создает форму в модуле задач с параметрами, определенными в манифесте. При нажатии Отправить `composeExtension/submitAction` отправляется боту. Дополнительные сведения о ожидаемом наборе ответов см. в [ответе на отправку.](#responding-to-submit)

### <a name="dynamic-input-using-an-adaptive-card"></a>Динамический ввод с помощью адаптивной карты

В этом методе служба может определить настраиваемую адаптивную карту для сбора ввода конечных пользователей. Для этого подхода установите параметр `fetchTask` в `true` манифесте. Обратите внимание, что если вы заданы какие-либо статические параметры, определенные для `fetchTask` `true` команды, будут проигнорированы.

В этом методе служба получает событие и отвечает адаптивным ответом модуля задач на основе `composeExtension/fetchTask` [карт.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) Ниже приводится пример ответа с адаптивной картой:

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

Бот также может отвечать ответом auth/config, если пользователю необходимо проверить подлинность или настроить расширение перед получением ввода пользователя.

### <a name="dynamic-input-using-a-web-view"></a>Динамический ввод с помощью веб-представления

В этом методе служба может показать основанный виджет, чтобы показать любой пользовательский `<iframe>` пользовательский интерфейс и собрать пользовательский ввод. Для этого подхода установите параметр `fetchTask` в `true` манифесте.

Так же, как и в потоке адаптивной карты, служба отправляет событие и отвечает ответом целевого модуля на основе `fetchTask` [URL-адресов.](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) Ниже приводится пример ответа с адаптивной картой:

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

### <a name="request-to-install-your-conversational-bot"></a>Запрос на установку разговорного бота

Если ваше приложение также содержит разговорный бот, может потребоваться убедиться, что ваш бот установлен в беседе перед загрузкой модуля задач. Это может быть полезно в ситуациях, когда необходимо получить дополнительный контекст для модуля задач. Например, может потребоваться получить список для заполнения управления сборщиком людей или список каналов в команде.

Чтобы облегчить этот поток, когда расширение обмена сообщениями сначала получает проверку вызова, чтобы узнать, установлен ли ваш бот `composeExtension/fetchTask` в текущем контексте. Для этого можно выполнить вызов реестра получения, например, если бот не установлен, вы возвращаете адаптивную карту с действием, которое запрашивает у пользователя установку бота См. в примере ниже. Обратите внимание, что для этого пользователю необходимо иметь разрешение на установку приложений в этом расположении; если они не могут, им будет представлено сообщение с просьбой связаться со своим администратором.

Вот пример ответа:

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

Как только пользователь завершит установку, ваш бот получит еще одно сообщение вызова с `name = composeExtension/submitAction` и `value.data.msteams.justInTimeInstall = true` .

Вот пример вызова:

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

Вы должны ответить на этот вызов тем же ответом задачи, на который вы ответили бы, если бы бот уже был установлен.

## <a name="responding-to-submit"></a>Реагирование на отправку

После ввода ввода пользователь получит событие с набором командных `composeExtension/submitAction` и параметров.

Это различные ожидаемые ответы на `submitAction` .

### <a name="task-module-response"></a>Ответ модуля задач

Это используется, когда для получения дополнительных сведений в расширении необходимо цепные диалоги. Ответ точно такой же, как `fetchTask` упоминалось ранее.

### <a name="compose-extension-authconfig-response"></a>Compose extension auth/config response

Это используется, когда для продолжения расширения необходимо либо проверить подлинность, либо настроить. Дополнительные сведения см. [в разделе проверка](~/resources/messaging-extension-v3/search-extensions.md#authentication) подлинности в разделе поиск.

### <a name="compose-extension-result-response"></a>Compose extension result response

Это используется для вставки карточки в поле составить в результате команды. Это тот же ответ, который используется в команде поиска, но он ограничен одной картой или одним результатом в массиве.

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Ответьте адаптивным сообщением карточки, отправленным от бота

Вы также можете ответить на действие отправки, вставив сообщение с адаптивной картой в канал с помощью бота. Пользователь сможет предварительно просмотреть сообщение перед отправкой и, возможно, изменить или взаимодействовать с ним. Это может быть очень полезно в сценариях, в которых необходимо собрать информацию от пользователей перед созданием адаптивного ответа карты. В следующем сценарии показано, как использовать этот поток для настройки опроса без включаемых этапов настройки в сообщение канала.

1. Пользователь щелкает расширение обмена сообщениями, чтобы вызвать модуль задач.
1. Для настройки опроса пользователь использует модуль задач.
1. После отправки модуля задач конфигурации приложение использует сведения, представленные в модуле задач, для изготовления адаптивной карты и отправляет ее в качестве ответа `botMessagePreview` клиенту.
1. Пользователь может предварительно просмотреть сообщение адаптивной карты, прежде чем бот вставляет его в канал. Если бот еще не является участником канала, щелкнув, `Send` он добавит бота.
1. Взаимодействие с адаптивной картой изменит сообщение перед отправкой.
1. Как только пользователь `Send` щелкнет, бот будет отправлять сообщение в канал.

Чтобы включить этот поток, модуль задач должен отвечать, как в приведенной ниже примере, в которой будет представлено сообщение предварительного просмотра пользователю.

>[!Note]
>Должен содержать действие с 1 адаптивным `activityPreview` вложением `message` карт.

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

Теперь расширению сообщения потребуется ответить на два новых типа взаимодействий и `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` . Ниже приведен пример `value` объекта, необходимого для обработки:

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

При ответе на запрос необходимо ответить с помощью значений, заполняемых сведениями, которые пользователь `edit` `task` уже представил. При ответе на запрос необходимо отправить сообщение в канал, содержащий `send` завершенную адаптивную карту.

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

В этом примере показан этот поток с помощью [Microsoft.Bot.Connector.Teams SDK (v3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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