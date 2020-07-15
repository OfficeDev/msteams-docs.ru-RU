---
title: Ответ на действие отправить модуль задач
author: clearab
description: В этой статье описывается, как реагировать на действия по отправке модуля задач из команды действия расширения системы обмена сообщениями
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: cc62bd6643fad9b3f2054d6595dd509b75c59680
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137663"
---
# <a name="respond-to-the-task-module-submit-action"></a>Ответ на действие отправить модуль задач

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

После того как пользователь отправит модуль задач, веб-служба получит `composeExtension/submitAction` сообщение Invoke с идентификатором команды и значением параметра. В течение пяти секунд приложение будет отвечать на вызов, в противном случае пользователь получит сообщение об ошибке "не удается получить доступ к приложению", а любой ответ на вызов будет игнорироваться клиентом Teams.

Вы можете отвечать следующим параметрам.

* Нет ответа — вы можете использовать действие Отправить для запуска процесса во внешней системе и не предоставлять пользователю никаких отзывов. Это может быть удобно для длительных процессов, и вы можете оставить отзыв другим способом (например, с помощью [упреждающего сообщения](~/bots/how-to/conversations/send-proactive-messages.md)).
* [Другой модуль задач](#respond-with-another-task-module) — вы можете ответить на дополнительный модуль задач как часть многоэтапного взаимодействия.
* [Ответ с картой](#respond-with-a-card-inserted-into-the-compose-message-area) — вы можете ответить на карточку, которую пользователь сможет взаимодействовать с или вставить в сообщение.
* [Адаптивная карта из ленты](#bot-response-with-adaptive-card) вставьте адаптивную карту непосредственно в беседу.
* [Запрос проверки подлинности пользователя](~/messaging-extensions/how-to/add-authentication.md)
* [Запрос на предоставление пользователю дополнительной настройки](~/messaging-extensions/how-to/add-configuration-page.md)

В приведенной ниже таблице показано, какие типы ответов доступны в зависимости от расположения вызова ( `commandContext` ) расширения обмена сообщениями. Для проверки подлинности или конфигурации после того, как пользователь завершит выполнение, исходный вызов будет повторно отправлен в веб-службу.

|Тип ответа | графический | панель команд | message |
|--------------|:-------------:|:-------------:|:---------:|
|Ответ с картой | x | x | x |
|Другой модуль задач | x | x | x |
|Bot с адаптивной картой | x |  | x |
| Нет ответа | x | x | x |

## <a name="the-submitaction-invoke-event"></a>Событие Invoke Субмитактион

Ниже приводятся примеры получения сообщения вызова.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

Пример объекта JSON, который вы получите. `commandContext`Параметр указывает, откуда было инициировано расширение обмена сообщениями. `data`Объект содержит поля формы в качестве параметров и значения, которые пользователь отправил. Объект JSON в этом разделе сокращается, чтобы выделить наиболее релевантные поля.

```json
{
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith",
  "serviceUrl": "https://smba.trafficmanager.net/amer/",
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "id": "submitButton",
      "formField1": "formField1_value",
      "formField2": "formField2_value",
      "formField3": "formField3_value"
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  }
}
```

* * *

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Ответ с картой, вставленной в область "Создание сообщения"

Наиболее распространенным способом ответа на `composeExtension/submitAction` запрос является карта, вставленная в область сообщения создать. Затем пользователь может послать карточку в беседу. Дополнительные сведения об использовании [карт см.](~/task-modules-and-cards/cards/cards-actions.md)

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    dynamic Data = JObject.Parse(action.Data.ToString());
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var card = new HeroCard
    {
        Title = Data["formField1"] as string,
        Subtitle = Data["formField2"]  as string,
        Text = Data["formField3"]  as string,
    };

    var attachments = new List<MessagingExtensionAttachment>();
    attachments.Add(new MessagingExtensionAttachment
    {
        Content = card,
        ContentType = HeroCard.ContentType,
        Preview = card.ToAttachment(),
    });

    response.ComposeExtension.Attachments = attachments;

    return response;

}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const data = action.data;
    const heroCard = CardFactory.heroCard(data.title, data.text);
    heroCard.content.subtitle = data.subTitle;
    const attachment = { contentType: heroCard.contentType, content: heroCard.content, preview: heroCard };

    return {
      composeExtension: {
        type: 'result',
        attachmentLayout: 'list',
        attachments: [
          attachment
        ]
      }
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "composeExtension": {
    "attachmentLayout": "list",
    "type": "result",
    "attachments": [
      {
        "preview": {
          "contentType": "application/vnd.microsoft.card.hero",
          "content": {
            "title": "formField1_value",
            "subtitle": "formField2_value",
            "text": "formField3_value"
          }
        },
        "contentType": "application/vnd.microsoft.card.hero",
        "content": {
          "title": "formField1_value",
          "subtitle": "formField2_value",
          "text": "formField3_value"
        }
      }
    ]
  }
}
```

* * *

## <a name="respond-with-another-task-module"></a>Ответ с другим модулем задач

Вы можете ответить на `submitAction` событие с помощью дополнительного модуля задачи. Это может быть удобно, если:

* Необходимо собрать большой объем информации.
* Динамическое изменение собираемых данных на основе вводимых пользователем данных
* Если вам нужно проверить данные, отправленные пользователем, и потенциально отправить форму с сообщением об ошибке, если что-то не так. 

Метод для ответа такой же, как и в ответ [на исходное `fetchTask` событие](~/messaging-extensions/how-to/action-commands/create-task-module.md). Если вы используете пакет SDK для ленты, то одно и то же событие будет запущено для обоих действий. Это означает, что необходимо добавить логику, определяющую правильный ответ.

## <a name="bot-response-with-adaptive-card"></a>Ответ Bot со адаптивной картой

>[!Note]
>Для этого процесса необходимо добавить `bot` объект в манифест приложения, и у вас есть необходимая область, определенная для Bot. Используйте тот же идентификатор, что и для своего расширения обмена сообщениями для ленты.

Вы также можете ответить на действие Отправить, вставив сообщение с адаптивной картой в канал с помощью ленты. Пользователь сможет просмотреть сообщение перед его отправкой и потенциально редактировать/взаимодействовать с ним. Это может быть очень удобно в тех случаях, когда необходимо собрать информацию от пользователей перед созданием ответа на адаптивную карту или при необходимости обновления карточки после того, как пользователь взаимодействует с ней. В приведенном ниже сценарии показано, как приложение Полли использует этот процесс для настройки опроса без включения действий по настройке в беседе канала.

1. Пользователь выбирает расширение системы обмена сообщениями для запуска модуля задачи.
2. Пользователь настраивает опрос с помощью модуля задач.
3. После отправки модуля задачи приложение использует сведения, предоставленные для создания опроса в качестве адаптивной карты, и отправляет его в качестве `botMessagePreview` ответа клиенту.
4. После этого пользователь может просмотреть сообщение адаптивной карточки перед вставкой ленты в канал. Если приложение еще не является участником канала, его Нажатие `Send` будет добавлено.
   1. Пользователь также может выбрать `Edit` сообщение, которое возвращает их в исходный модуль задач.
5. При взаимодействии с адаптивной картой изменяется сообщение перед его отправкой.
6. После того как пользователь нажмет `Send` сообщение в канале, вы отправляете его в канал.

### <a name="respond-to-initial-submit-action"></a>Ответ на начальное действие по отправку

Чтобы включить этот рабочий процесс, модуль задачи должен отвечать исходному `composeExtension/submitAction` сообщению с предварительным просмотром карты, отправляемой с канала в канале Bot. Это дает пользователю возможность проверить карточку перед отправкой, а также попытаться установить Bot в беседе, если она еще не установлена.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic Data = JObject.Parse(action.Data.ToString());
  var response = new MessagingExtensionActionResponse
  {
    ComposeExtension = new MessagingExtensionResult
    {
      Type = "botMessagePreview",
      ActivityPreview = MessageFactory.Attachment(new Attachment
      {
        Content = new AdaptiveCard("1.0")
        {
          Body = new List<AdaptiveElement>()
          {
            new AdaptiveTextBlock() { Text = "FormField1 value was:", Size = AdaptiveTextSize.Large },
            new AdaptiveTextBlock() { Text = Data["FormField1"] as string }
          },
          Height = AdaptiveHeight.Auto,
          Actions = new List<AdaptiveAction>()
          {
            new AdaptiveSubmitAction
            {
              Type = AdaptiveSubmitAction.TypeName,
              Title = "Submit",
              Data = new JObject { { "submitLocation", "messagingExtensionFetchTask" } },
            },
          }
        },
        ContentType = AdaptiveCard.ContentType
      }) as Activity
    }
  };

  return response;
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const submittedData = action.data;
    const adaptiveCard = CardFactory.adaptiveCard({
      actions: [
        { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
      ],
      body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submittedData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
        {
          choices: [
            { title: submittedData.Option1, value: submittedData.Option1 },
            { title: submittedData.Option2, value: submittedData.Option2 },
            { title: submittedData.Option3, value: submittedData.Option3 }
          ],
          id: 'Choices',
          isMultiSelect: submittedData.MultiSelect,
          style: 'expanded',
          type: 'Input.ChoiceSet'
        }
      ],
      type: 'AdaptiveCard',
      version: '1.0'
    });
    return {
      composeExtension: {
        activityPreview: MessageFactory.attachment(adaptiveCard, null, null, InputHints.ExpectingInput),
        type: 'botMessagePreview'
      }
    };
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

>[!Note]
>`activityPreview`Должен содержать `message` действие с ровно 1 вложенной картой. `<< Card Payload >>`Значение — это заполнитель для карточки, которую вы хотите отправить.

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

* * *

### <a name="the-botmessagepreview-send-and-edit-events"></a>События отправки и редактирования Ботмессажепревиев

Теперь ваше расширение сообщения должно реагировать на два новых вида `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"` и `value.botMessagePreviewAction = "edit"` .

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewEditAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionBotMessagePreviewEdit(context, action) {

    //handle the event
  }
  
  handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {

    //handle the event
  }
}

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "edit | send",
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

* * *

### <a name="respond-to-botmessagepreview-edit"></a>Отклик на редактирование Ботмессажепревиев

Если пользователь решил изменить карточку перед отправкой, нажав кнопку **изменить** , вы получите `composeExtension/submitAction` вызов с помощью `value.botMessagePreviewAction = edit` . Обычно необходимо ответить, выполнив возврат модуля задачи, отправленного в ответ на начальный `composeExtension/fetchTask` вызов, который начал взаимодействие. Это позволяет пользователю начать процесс, повторно вводя исходные данные. Кроме того, следует рассмотреть возможность использования сведений, которые теперь доступны для предварительного заполнения модуля задач, чтобы пользователь не заполнил всю информацию с нуля.

Узнайте, [как реагировать на начальное `fetchTask` событие](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Ответ на отправку Ботмессажепревиев

Когда пользователь нажимает кнопку **Отправить** , вы получите `composeExtension/submitAction` вызов с помощью команды `value.botMessagePreviewAction = send` . Веб-службе потребуется создать и отправить упреждающее сообщение с помощью адаптивной карточки в беседу, а также ответить на вызов.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var activityPreview = action.BotActivityPreview[0];
  var attachmentContent = activityPreview.Attachments[0].Content;
  var previewedCard = JsonConvert.DeserializeObject<AdaptiveCard>(attachmentContent.ToString(),
          new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore });
  
  previewedCard.Version = "1.0";

  var responseActivity = Activity.CreateMessageActivity();
  Attachment attachment = new Attachment()
  {
    ContentType = AdaptiveCard.ContentType,
    Content = previewedCard
  };
  responseActivity.Attachments.Add(attachment);
  
  // Attribute the message to the user on whose behalf the bot is posting
  responseActivity.ChannelData = new {
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }
  };
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {
      // The data has been returned to the bot in the action structure.
      const activityPreview = action.botActivityPreview[0];
      const attachmentContent = activityPreview.attachments[0].content;
      const userText = attachmentContent.body[1].text;
      const choiceSet = attachmentContent.body[3];

      const submitData = {
        MultiSelect: choiceSet.isMultiSelect ? 'true' : 'false',
        Option1: choiceSet.choices[0].title,
        Option2: choiceSet.choices[1].title,
        Option3: choiceSet.choices[2].title,
        Question: userText
      };

      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [
          { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
        ],
        body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submitData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
          {
            choices: [
                { title: submitData.Option1, value: submitData.Option1 },
                { title: submitData.Option2, value: submitData.Option2 },
                { title: submitData.Option3, value: submitData.Option3 }
            ],
            id: 'Choices',
            isMultiSelect: submitData.MultiSelect,
            style: 'expanded',
            type: 'Input.ChoiceSet'
          }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });
      const responseActivity = { type: 'message', attachments: [adaptiveCard], channelData: {
          onBehalfOf: [
              { itemId: 0, mentionType: 'person', mri: context.activity.from.id, displayname: context.activity.from.name }
          ]
      }};

      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

Появится новое `composeExtension/submitAction` сообщение, аналогичное следующему:

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send",
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

* * *

### <a name="user-attribution-for-bots-messages"></a>Атрибуты пользователей для сообщений Боты 

В сценариях, где Bot отправляет сообщения от имени пользователя, применяя к сообщению этого пользователя, вы можете помочь в задействовании и продемонстрировать более естественный процесс взаимодействия. Эта функция позволяет присвоить сообщение от пользователя Bot пользователю, от имени которого оно было отправлено.

На изображении внизу слева отображается сообщение с картой, отправленное с помощью элемента "Bot *без* атрибутов пользователя", а справа — карта, отправленная *с помощью атрибутов пользователя.*

![Снимок экрана](../../../assets/images/messaging-extension/user-attribution-bots.png)

Чтобы использовать атрибуты пользователей в Teams, необходимо добавить `OnBehalfOf` сущность "упоминание" в `ChannelData` `Activity` полезные данные, отправляемые в Teams.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-1)

```csharp
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }

```

# <a name="json"></a>[JSON](#tab/json-1)

```json
{
    "text": "Hello World!",
    "ChannelData": {
        "OnBehalfOf": [{
            "itemid": 0,
            "mentionType": "person",
            "mri": "29:orgid:89e6508d-6c0f-4ffe-9f6a-b58416d965ae",
            "displayName": "Sowrabh N R S"
        }]
    }
}
```

* * *

Ниже приведено описание сущностей в `OnBehalfOf` массиве.

#### <a name="details-of--onbehalfof-entity-schema"></a>Сведения о `OnBehalfOf` схеме объекта

|Поле|Тип|Описание|
|:---|:---|:---|
|`itemId`|Integer|Должно быть равно 0|
|`mentionType`|String|Должно быть "Person"|
|`mri`|String|Идентификатор ресурса сообщения (МРИ) пользователя, от имени которого отправляется сообщение. В качестве имени отправителя сообщения будет использоваться " \<user\> Via \<bot name\> ".|
|`displayName`|String|Имя пользователя. Используется в качестве резервного при разрешении имени в случае недоступности.|
  
## <a name="next-steps"></a>Дальнейшие действия

Добавление команды поиска

* [Определить команды поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
