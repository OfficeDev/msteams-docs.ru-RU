---
title: Запуск действий с расширениями обмена сообщениями
description: Создайте расширения для обмена сообщениями на основе действий, чтобы разрешить пользователям запускать внешние службы.
keywords: службы расширения обмена сообщениями Teams.
ms.openlocfilehash: 1a38b4f7bfb413defd28950ca9b97f7411cf9c09
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228033"
---
# <a name="initiate-actions-with-messaging-extensions"></a>Запуск действий с расширениями обмена сообщениями

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

Расширения обмена сообщениями на основе действий позволяют пользователям активировать действия во внешних службах в Teams.

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

В следующих разделах описано, как это сделать.

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>Расширения сообщений для типов действий

Чтобы инициировать действия из расширения обмена сообщениями, `type` задайте для `action`параметра значение. Ниже приведен пример манифеста с командой поиска и созданием. Одно расширение системы обмена сообщениями может содержать до 10 разных команд. Сюда могут входить как несколько команд поиска, так и несколько команд, основанных на действиях.

#### <a name="complete-app-manifest-example"></a>Пример полного манифеста приложения

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="initiate-actions-from-messages"></a>Инициация действий из сообщений

Кроме запуска действий из области создание сообщения, можно также использовать расширение системы обмена сообщениями, чтобы инициировать действие из сообщения. Это позволит отправить содержимое сообщения в Bot для обработки и при необходимости ответить на это сообщение с помощью метода, описанного при ответе [на отправку](#responding-to-submit). Ответ будет вставлен в ответ на сообщение, которое пользователи могут изменить перед отправкой. Пользователи могут получить доступ к своему расширению обмена сообщениями из меню переполнения `...` , а затем выбрать `Take action` , как показано на рисунке ниже.

![Пример инициирования действия из сообщения](~/assets/images/compose-extensions/messageextensions_messageaction.png)

Чтобы ваше расширение обмена сообщениями работало из сообщения, необходимо добавить `context` параметр в `commands` объект расширения обмена сообщениями в манифесте приложения, как показано в примере ниже. Допустимые строки для `context` массива: `"message"`, `"commandBox"`и `"compose"`. Значение по умолчанию — `["compose", "commandBox"]`. Для получения подробных сведений о `context` параметре обратитесь к разделу [define Commands](#define-commands) .

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

Ниже приведен пример `value` объекта, содержащего сведения о сообщении, которое будет отправлено в качестве части `composeExtension` запроса, отправляемого на сервер робота.

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

### <a name="test-via-uploading"></a>Тестирование через отправку

Вы можете проверить расширение системы обмена сообщениями, отправив свое приложение. Сведения о [том, как загрузить ваше приложение в группу,](~/concepts/deploy-and-publish/apps-upload.md) можно найти в разделе.

Чтобы открыть расширение системы обмена сообщениями, перейдите к любому из бесед или каналов. Нажмите кнопку **Дополнительные параметры** (**&#8943;**) в поле создать и выберите ваш добавочный номер для обмена сообщениями.

## <a name="collecting-input-from-users"></a>Сбор данных, вводимых пользователями

Существует три способа сбора информации от конечного пользователя в Teams.

### <a name="static-parameter-list"></a>Список статических параметров

В этом методе необходимо только определить статический список параметров в манифесте, как показано выше в команде "создать". Чтобы использовать этот метод, `fetchTask` убедитесь, что `false` в манифесте заданы и определены параметры.

Когда пользователь выбирает команду с помощью статических параметров, Teams создаст форму в модуле задач с параметрами, определенными в манифесте. При нажатии на `composeExtension/submitAction` команду Отправить сообщение a отправляется в Bot. В разделе [ответ на отправляются](#responding-to-submit) дополнительные сведения о ожидаемом наборе ответов.

### <a name="dynamic-input-using-an-adaptive-card"></a>Динамическое входное значение с использованием адаптивной карточки

В этом методе служба может определить настраиваемую адаптивную карточку для сбора данных, вводимых пользователем. Для этого подхода задайте для `fetchTask` `true` параметра значение в манифесте. Обратите внимание, что `fetchTask` если `true` вы задаете любые статические параметры, определенные для команды, будут игнорироваться.

В этом методе служба будет получать `composeExtension/fetchTask` событие и реагировать на [отклики](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)от функции адаптивного модуля задач на основе карты. Ниже приведен пример ответа с помощью адаптивной карточки:

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

Bot также может отвечать с ответом на запрос проверки подлинности и конфигурации, если пользователю необходимо проверить подлинность или настроить расширение перед тем, как получить входные данные пользователя.

### <a name="dynamic-input-using-a-web-view"></a>Динамическое входное значение с использованием веб-представления

В этом методе служба может показать `<iframe>` мини-приложение для отображения любого НАСТРАИВАЕМОГО пользовательского интерфейса и сбора вводимых пользователем данных. Для этого подхода задайте для `fetchTask` `true` параметра значение в манифесте.

Как и в случае с адаптивным продвижением карт, ваша `fetchTask` служба отправляет событие и требует [ответа на модуль задачи](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)на основе URL-адреса. Ниже приведен пример ответа с помощью адаптивной карточки:

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

### <a name="request-to-install-your-conversational-bot"></a>Запрос на установку программы "bot" для беседы

Если ваше приложение также содержит объект Bot для общения, возможно, перед загрузкой модуля задачи необходимо убедиться, что в беседе установлен почтовый робот. Это может быть удобно в тех случаях, когда требуется получить дополнительный контекст для модуля задач. Например, может потребоваться получить список для заполнения элемента управления "Выбор людей" или список каналов в команде.

Для упрощения этого процесса, когда расширение системы обмена сообщениями `composeExtension/fetchTask` сначала получает запрос на вызов, чтобы проверить, установлен ли ваш Bot в текущем контексте (например, вы можете сделать это с помощью попытки получения списка, например). Если сервер-робот не установлен, вы возвращаете адаптивную карту с действием, которое запрашивает у пользователя установку ленты, в примере ниже. Обратите внимание, что для этого необходимо, чтобы у пользователя было разрешение на установку приложений в этом расположении; Если они не смогут получить сообщение, попросите их обратиться к администратору.

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

Когда пользователь завершит установку, ваш робот получит еще одно сообщение Invoke с `name = composeExtension/submitAction`, и. `value.data.msteams.justInTimeInstall = true`

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

Вы должны ответить на этот вызов с тем же ответом задачи, на который вы ответили, если он уже установлен.

## <a name="responding-to-submit"></a>Ответ на отправляют

После того как пользователь завершит ввод данных, пользователь Bot получит `composeExtension/submitAction` событие с идентификатором команды и значением параметра.

Это различные ожидаемые ответы на `submitAction`.

### <a name="task-module-response"></a>Отклик модуля задачи

Он используется, когда расширение должно повязать диалоговые окна для получения дополнительных сведений. Ответ точно такой же, как `fetchTask` и упоминалось ранее.

### <a name="compose-extension-authconfig-response"></a>Ответ на запрос проверки подлинности и настройки расширения

Этот параметр используется, если для продолжения расширения требуется проверка подлинности или Настройка. Дополнительные сведения см. в [разделе "Проверка подлинности](~/resources/messaging-extension-v3/search-extensions.md#authentication) " в разделе "Поиск".

### <a name="compose-extension-result-response"></a>Ответ на результат расширения создания

Используется для вставки карточки в поле создание в результате выполнения команды. Это тот же ответ, который используется в команде поиска, но он ограничен одной картой или одним результатом в массиве.

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>Ответ с сообщением адаптивной карточки, отправленной с ленты

Вы также можете ответить на действие Отправить, вставив сообщение с адаптивной картой в канал с помощью ленты. Пользователь сможет просмотреть сообщение перед его отправкой и потенциально редактировать/взаимодействовать с ним. Это может быть очень удобно в сценариях, в которых необходимо собрать информацию от пользователей, прежде чем создавать адаптивный ответ карты. В приведенном ниже сценарии показано, как можно использовать этот процесс для настройки опроса без включения действий по настройке в сообщение канала.

1. Пользователь выбирает расширение системы обмена сообщениями для запуска модуля задачи.
1. Пользователь использует модуль задач для настройки опроса.
1. После отправки модуля задач конфигурации приложение использует сведения, представленные в модуле задачи, для создания адаптивной карточки и отправки ее в качестве `botMessagePreview` ответа клиенту.
1. После этого пользователь может просмотреть сообщение адаптивной карточки, прежде чем Bot вставит его в канал. Если Bot еще не является участником канала, щелчок `Send` добавит элемент Bot.
1. При взаимодействии с адаптивной картой изменится сообщение перед его отправкой.
1. После того, как `Send` пользователь нажмет на Bot, в канал будет отправлено сообщение.

Чтобы включить этот рабочий процесс, модуль задачи должен отвечать, как показано в примере ниже, который будет предоставлять пользователю сообщение о предварительном просмотре.

>[!Note]
>`activityPreview` Должен содержать `message` действие с ровно 1 вложенной картой.

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

Теперь для расширения сообщения необходимо ответить на два новых типа взаимодействия `value.botMessagePreviewAction = "send"` и. `value.botMessagePreviewAction = "edit"` Ниже приведен пример `value` объекта, который необходимо обработать:

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

При ответе на `edit` запрос необходимо ответить на `task` отклик со значениями, заполненными данными, которые уже были отправлены пользователем. При ответе на `send` запрос необходимо отправить сообщение каналу, содержащему завершенную адаптивную карту.

# <a name="typescriptnodejs"></a>[TypeScript/Node. js](#tab/typescript)

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

В этой статье *также приведены* [примеры кода Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

# <a name="cnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

В этом примере показан этот процесс с помощью [пакета SDK Microsoft. Bot. Connector. Teams (v3)](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).

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
