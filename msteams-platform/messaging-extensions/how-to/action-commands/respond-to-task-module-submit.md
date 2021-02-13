---
title: Реагирование на действие отправки модуля задачи
author: clearab
description: Описывает, как реагировать на действие отправки модуля задачи из команды действия расширения обмена сообщениями
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1fb2f2dc51d7de1208a5a913abf2d38cb80c401a
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231647"
---
# <a name="respond-to-the-task-module-submit-action"></a>Реагирование на действие отправки модуля задачи

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

После отправки пользователем модуля задачи веб-служба получает сообщение об вызове со значениями ИД команды `composeExtension/submitAction` и параметров. У вашего приложения есть пять секунд на ответ на вызов, в противном случае пользователь получает сообщение об *ошибке,* не достигаемого приложением, а любой ответ на вызов игнорируется клиентом Teams.

У вас есть следующие варианты ответа:

* Нет ответа — вы можете использовать действие отправки для запуска процесса во внешней системе и не предоставлять пользователю никаких отзывов. Это может быть полезно для длительных процессов, и вы можете отправить отзыв другим способом (например, с помощью упреждающего [сообщения).](~/bots/how-to/conversations/send-proactive-messages.md)
* [Другой модуль задачи](#respond-with-another-task-module) — вы можете ответить дополнительным модулем задачи в рамках многоэтапного взаимодействия.
* [Ответ карточки.](#respond-with-a-card-inserted-into-the-compose-message-area) Вы можете ответить карточкой, с помощью которую пользователь сможет взаимодействовать и/или вставлять данные в сообщение.
* [Адаптивная карточка из бота:](#bot-response-with-adaptive-card) вставка адаптивной карточки непосредственно в беседу.
* [Запрос проверки подлинности пользователя](~/messaging-extensions/how-to/add-authentication.md)
* [Запрос на предоставление пользователем дополнительной настройки](~/messaging-extensions/how-to/add-configuration-page.md)

Для проверки подлинности или настройки после завершения пользователем потока исходный вызов перенаправляется в веб-службу. В следующей таблице показано, какие типы ответов доступны в зависимости от расположения вызова `commandContext` расширения обмена сообщениями: 

|Тип ответа | compose | панель команд | message |
|--------------|:-------------:|:-------------:|:---------:|
|Ответ карточки | x | x | x |
|Другой модуль задачи | x | x | x |
|Бот с адаптивной картой | x |  | x |
| Без ответа | x | x | x |

## <a name="the-submitaction-invoke-event"></a>Событие вызова submitAction

Примеры получения сообщения вызова:

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

Это пример получаемого объекта JSON. Этот параметр указывает, откуда активировали расширение обмена `commandContext` сообщениями. Объект содержит поля формы в качестве параметров `data` и значения, отправленные пользователем. Здесь объект JSON сокращен, чтобы выделить наиболее релевантные поля.

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Ответ с помощью карточки, вставленной в область сообщения составить

Наиболее распространенный способ ответа на запрос — карточка, вставленная `composeExtension/submitAction` в область составить сообщение. Затем пользователь может отправить карточку в беседу. Дополнительные сведения об использовании карточек см. [в карточках и действиях карт.](~/task-modules-and-cards/cards/cards-actions.md)

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var createCardData = ((JObject)action.Data).ToObject<CreateCardData>();
var card = new HeroCard
{
     Title = createCardData.Title,
     Subtitle = createCardData.Subtitle,
     Text = createCardData.Text,
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

## <a name="respond-with-another-task-module"></a>Ответ с помощью другого модуля задачи

Вы можете ответить на событие `submitAction` с помощью дополнительного модуля задачи. Это может быть полезно, если:

* Необходимо собирать большие объемы информации.
* Если вам нужно динамически изменить собираемую информацию на основе пользовательского ввода
* Если вам нужно проверить сведения, отправленные пользователем, и, возможно, повторно отправить форму с сообщением об ошибке, если что-то не так. 

Метод ответа такой же, как и ответ [на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md) Если вы используете SDK Bot Framework, одинаковые триггеры событий для обоих действий отправки. Это означает, что необходимо добавить логику, которая определяет правильный ответ.

## <a name="bot-response-with-adaptive-card"></a>Ответ бота с помощью адаптивной карточки

>[!Note]
>Для этого потока необходимо добавить объект в манифест приложения и определить для бота необходимую `bot` область. Используйте тот же ИД, что и расширение для обмена сообщениями для бота.

Вы также можете ответить на действие отправки, вставив сообщение с адаптивной карточкой в канал с помощью бота. Пользователь может просмотреть сообщение перед отправкой, а также, возможно, изменить или взаимодействовать с ним. Это может быть очень полезно в сценариях, когда вы собираете сведения от пользователей перед созданием ответа адаптивной карточки или обновляете карточку после того, как кто-то взаимодействует с ней. В следующем сценарии показано, как приложение Polly использует этот поток для настройки опроса без включаемых действий по настройке в беседу канала:

1. Пользователь выбирает расширение обмена сообщениями для запуска модуля задачи.
2. Пользователь настраивает опрос с помощью модуля задачи.
3. После отправки модуля задачи приложение использует сведения, предоставленные для создания опроса в качестве адаптивной карточки, и отправляет его клиенту в качестве `botMessagePreview` ответа.
4. Затем пользователь может просмотреть сообщение адаптивной карточки, прежде чем бот вставляет его в канал. Если приложение еще не является участником канала, выбор добавляет `Send` его.
   1. Пользователь также может выбрать сообщение, которое возвращает его в `Edit` исходный модуль задачи.
5. Взаимодействие с адаптивной картой изменяет сообщение перед его отправкой.
6. После того как пользователь выберет `Send` бота, сообщение будет выкладывано в канал.

### <a name="respond-to-initial-submit-action"></a>Реагирование на первоначальное действие отправки

Чтобы включить этот поток, модуль задачи должен ответить на исходное сообщение предварительной версией карточки, отправляемой ботом `composeExtension/submitAction` в канал. Это дает пользователю возможность проверить карточку перед отправкой, а также попытаться установить бота в беседе, если она еще не установлена.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic createCardData = ((JObject) action.Data).ToObject(typeof(JObject));
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
>Действие `activityPreview` должно содержать только `message` 1 адаптивный вложение карточки. Значение `<< Card Payload >>` — это замеитель для карточки, отправляемой вами.

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>События отправки и изменения botMessagePreview

Расширение сообщения должно реагировать на два новых варианта `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"` и `value.botMessagePreviewAction = "edit"` .

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

### <a name="respond-to-botmessagepreview-edit"></a>Реагирование на редактирование botMessagePreview

Если пользователь редактирует карточку перед  отправкой, нажатием кнопки "Изменить", вы получите вызов с помощью `composeExtension/submitAction` `value.botMessagePreviewAction = edit` . Обычно в ответ на первоначальный вызов, который начал взаимодействие, следует возвращать модуль задачи, отправленный в ответ на `composeExtension/fetchTask` его первоначальный вызов. Это позволяет пользователю начать процесс повторно, повторно введите исходные сведения. Используйте доступные сведения для предварительного заполнения модуля задачи, чтобы пользователю не нужно было заполнять всю информацию с нуля.

См. [ответ на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md)

### <a name="respond-to-botmessagepreview-send"></a>Ответ на отправку botMessagePreview

После того как  пользователь нажал кнопку "Отправить", вы получите вызов с помощью `composeExtension/submitAction` `value.botMessagePreviewAction = send` . Веб-служба должна создать и отправить в беседу упреждающие сообщения с адаптивной карточкой, а также ответить на вызов.

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

Вы получаете новое `composeExtension/submitAction` сообщение, аналогичное следующему:

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

### <a name="user-attribution-for-bots-messages"></a>Атрибут пользователя для сообщений ботов 

В сценариях, когда бот отправляет сообщения от имени пользователя, присвоение сообщений этому пользователю может помочь с вовлечением и продемонстрировать более естественный поток взаимодействия. Эта функция позволяет приписать сообщение от бота пользователю, от имени которого оно было отправлено.

На следующем изображении слева находится карточка,  отправленная ботом без атрибуции пользователя,  а справа — карточка, отправленная ботом с атрибуцией пользователя.

![Снимок экрана](../../../assets/images/messaging-extension/user-attribution-bots.png)

Чтобы использовать атрибут пользователя в командах, необходимо добавить объект упоминания в полезной нагрузке, `OnBehalfOf` `ChannelData` которая `Activity` отправляется в Teams.

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

В следующем разделе приводится описание сущностями в `OnBehalfOf` массиве:

#### <a name="details-of--onbehalfof-entity-schema"></a>Сведения о  `OnBehalfOf` схеме сущности

|Поле|Тип|Описание|
|:---|:---|:---|
|`itemId`|Целое число|Должно быть 0|
|`mentionType`|String|Должно быть "person"|
|`mri`|String|Идентификатор ресурса сообщения (MRI) пользователя, от имени которого отправляется сообщение. Имя отправитель сообщения будет отображаться как " \<user\> через \<bot name\> ".|
|`displayName`|String|Имя человека. Используется в качестве отката, если разрешение имен недоступно.|
  
## <a name="next-steps"></a>Дальнейшие действия

Добавление команды поиска

* [Определить команды поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
