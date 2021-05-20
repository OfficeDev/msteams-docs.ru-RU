---
title: Инициировать действия с расширением обмена сообщениями
description: Создание расширений обмена сообщениями на основе действий, чтобы позволить пользователям вызывать внешние службы
localization_priority: Normal
ms.topic: how-to
keywords: команды обмена сообщениями расширения обмена сообщениями поиск
ms.openlocfilehash: bfb3295726c355164f080c15e3759ea36a99d914
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566742"
---
# <a name="initiate-actions-with-messaging-extensions"></a>Инициировать действия с расширением обмена сообщениями

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширения обмена сообщениями на основе действий позволяют пользователям инициировать действия во внешних службах, находясь внутри Teams.

![Пример карты расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

Следующие разделы описывают, как это сделать.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>Расширения сообщений типа действия

Для инициирования действий от расширения обмена сообщениями `type` установите параметр `action` на . Ниже приведен пример манифеста с поиском и командой создания. Одно расширение обмена сообщениями может иметь до 10 различных команд. Это может включать в себя как несколько поисковых запросов, так и несколько команд на основе действий.

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

В дополнение к инициированию действий из области композиции сообщений, вы также можете использовать расширение обмена сообщениями для инициирования действия из сообщения. Это позволит вам отправить содержимое сообщения вашему боту для обработки, и дополнительно ответить на это сообщение с ответом с помощью [метода, описанного в Ответ представить](#responding-to-submit). Ответ будет вставлен в ответ на сообщение, которое пользователи могут редактировать перед отправкой. Пользователи могут получить доступ к расширению обмена сообщениями из меню `...` переполнения, а затем выбрать `Take action` как на следующем изображении:

![Пример инициирования действия из сообщения](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Чтобы расширение обмена сообщениями работало из сообщения, необходимо добавить параметр к объекту расширения обмена сообщениями в `context` приложении, как это имеет место в `commands` приведенной ниже примере. Действительные строки для `context` `"message"` массива, `"commandBox"` и `"compose"` . Значение по умолчанию — `["compose", "commandBox"]`. Для получения [подробной информации](#define-commands) о параметре можно посмотреть раздел «Определить `context` команды».

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

Ниже приведен пример объекта, содержащего `value` сведения о сообщении, которые будут отправлены в рамках `composeExtension` запроса, отправленного вашему боту.

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

### <a name="test-via-uploading"></a>Тест через загрузку

Вы можете протестировать расширение обмена сообщениями, загрузив приложение. Для получения дополнительной [информации см.](~/concepts/deploy-and-publish/apps-upload.md)

Чтобы открыть расширение обмена сообщениями, перейдите на любой из ваших чатов или каналов. Выберите **кнопку «Больше** **&#8943;»**(подробнее) в поле для составления и выберите расширение обмена сообщениями.

## <a name="collecting-input-from-users"></a>Сбор входных данных от пользователей

Существует три способа сбора информации от конечному пользователю в Teams.

### <a name="static-parameter-list"></a>Статический список параметров

В этом методе все, что вам нужно сделать, это определить статический список параметров в манифесте, как показано выше в команде "Создать To Do" . Для использования этого метода `fetchTask` убедитесь, установлен `false` и что вы определяете параметры в манифесте.

Когда пользователь выбирает команду со статическими параметрами, Teams будет генерировать форму в модуле задач с параметрами, определенными в манифесте. При ударе Отправить `composeExtension/submitAction` отправляется бот. Для получения дополнительной информации об ожидаемом наборе ответов [см.](#responding-to-submit)

### <a name="dynamic-input-using-an-adaptive-card"></a>Динамический ввод с помощью адаптивной карты

В этом методе служба может определить пользовательскую адаптивную карту для сбора пользовательского ввода. Для этого подхода установите `fetchTask` параметр в `true` манифесте. Обратите внимание, что при `fetchTask` наборе `true` каких-либо статических параметров, определенных для команды, будет проигнорировано.

В этом методе ваш сервис получит событие `composeExtension/fetchTask` и должен ответить с адаптивной картой на основе [ответа модуля задач.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) Ниже приводится пример ответа с адаптивной картой:

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

Бот также может ответить ответом auth/config, если пользователю необходимо проверить подлинность или настроить расширение перед вводом пользователя.

### <a name="dynamic-input-using-a-web-view"></a>Динамический ввод с помощью веб-представления

В этом методе служба может показать виджет на `<iframe>` основе, чтобы показать любой пользовательский интерфейс и собрать пользовательский ввод. Для этого подхода установите `fetchTask` параметр в `true` манифесте.

Так же, как в адаптивном потоке карт ваша служба будет отправлять `fetchTask` события и должен ответить с URL-адресом на [основе ответа модуля задач.](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) Ниже приводится пример ответа с адаптивной картой:

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

Если ваше приложение также содержит разговорного бота, может потребоваться убедиться, что ваш бот установлен в разговоре перед загрузкой модуля задачи. Это может быть полезно в ситуациях, когда вам нужно получить дополнительный контекст для вас модуль задачи. Например, может потребоваться взять с 1900 человек список для заполнения управления сборщиками данных или список каналов в команде.

Чтобы облегчить этот поток, когда расширение обмена сообщениями сначала получает `composeExtension/fetchTask` проверку вызова, чтобы увидеть, если ваш бот установлен в текущем контексте. Вы можете сделать это, пытаясь получить список вызова, например, Если ваш бот не установлен, вы возвращаете адаптивную карту с действием, которое просит пользователя установить ваш бот Смотрите пример ниже. Обратите внимание, что для этого требуется разрешение пользователя на установку приложений в этом месте; если они не могут, им будет представлено сообщение с просьбой связаться с администратором.

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

Как только пользователь завершит установку, ваш бот получит еще одно сообщение вызова `name = composeExtension/submitAction` с , и `value.data.msteams.justInTimeInstall = true` .

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

Вы должны ответить на этот вызов с той же задачей ответ вы бы ответили, если бот был уже установлен.

## <a name="responding-to-submit"></a>Ответ на отправку

Как только пользователь завершает ввод ввода, бот получит событие с `composeExtension/submitAction` идентификатором команды и набором значений параметров.

Это различные ожидаемые ответы на `submitAction` .

### <a name="task-module-response"></a>Ответ на модуль задач

Это используется, когда расширение необходимо цепочки диалоги вместе, чтобы получить больше информации. Ответ точно такой же, как упоминалось `fetchTask` ранее.

### <a name="compose-extension-authconfig-response"></a>Составьте расширение auth/config ответ

Это используется, когда расширение необходимо либо проверить подлинность, либо настроить для продолжения. Для получения дополнительной информации [смотрите раздел аутентификации](~/resources/messaging-extension-v3/search-extensions.md#authentication) в разделе поиска.

### <a name="compose-extension-result-response"></a>Составьте ответ на результат расширения

Это используется для вставки карты в поле compose в результате команды. Это тот же ответ, который используется в команде поиска, но он ограничен одной картой или одним результатом в массиве.

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Ответить с адаптивной картой сообщение, отправленное от бота

Вы также можете ответить на отправку действий, вставив сообщение с адаптивной картой в канал с ботом. Пользователь сможет просмотреть сообщение перед отправкой, а также, возможно, редактировать/взаимодействовать с ним. Это может быть очень полезно в сценариях, где вам нужно собрать информацию от пользователей, прежде чем создавать адаптивный ответ карты. В следующем сценарии показано, как можно использовать этот поток для настройки опроса без включения шагов конфигурации в сообщение канала.

1. Пользователь нажимает на расширение обмена сообщениями, чтобы вызвать модуль задачи.
1. Пользователь использует модуль задач для настройки опроса.
1. После отправки модуля задачи конфигурации приложение использует информацию, представленную в модуле задачи, для создания адаптивной карты и `botMessagePreview` отправляет ее в качестве ответа клиенту.
1. Пользователь может просмотреть адаптивное сообщение карты, прежде чем бот вставить его в канал. Если бот еще не является членом канала, `Send` нажав будет добавить бота.
1. Взаимодействие с адаптивной картой изменит сообщение перед отправкой.
1. После того, как `Send` пользователь нажимает бот будет размещать сообщение на канале.

Для обеспечения этого потока модуль задачи должен отвечать, как в приведеном ниже примере, который представит предварительное сообщение пользователю.

>[!Note]
>Необходимо `activityPreview` содержать действие с `message` помощью ровно 1 адаптивного вложения карты.

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

Теперь расширение сообщения должно будет реагировать на два новых типа взаимодействий `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` и. Ниже приведен пример `value` объекта, который необходимо обработать:

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

При ответе на `edit` запрос вы должны ответить с `task` значениями, населенными информацией, которую пользователь уже представил. При ответе на запрос `send` следует отправить сообщение каналу, содержащее доработанную адаптивную карту.

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

Этот пример показывает этот поток с [помощью Microsoft.Bot.Connector.Teams SDK (v3).](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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

[Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)