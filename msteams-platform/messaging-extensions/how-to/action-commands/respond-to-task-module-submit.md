---
title: Ответ на действие отправки модуля задач
author: surbhigupta
description: Описывает, как реагировать на отправку действия модуля задач из команды действий расширения обмена сообщениями.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 79687dd98f8d88e365ae1528b36806d3ffc559d3
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157688"
---
# <a name="respond-to-the-task-module-submit-action"></a>Ответ на действие отправки модуля задач

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

В этом документе вы можете узнать, как ваше приложение реагирует на команды действий, например на отправку действия модуля задач пользователя.
После отправки модуля задач веб-служба получает сообщение вызова с командным `composeExtension/submitAction` ИД и значениями параметров. У приложения есть пять секунд для ответа на вызов, в противном случае пользователь получает сообщение об ошибке, которое не может достичь **приложения,** и любой ответ на вызов игнорируется Teams клиентом.

У вас есть следующие варианты ответа:

* Нет ответа. Используйте действие отправки, чтобы вызвать процесс во внешней системе и не предоставлять пользователю никаких отзывов. Это полезно для длительных процессов, и вы можете выбрать, чтобы предоставить обратную связь поочередно. Например, вы можете дать обратную связь с помощью [активного сообщения.](~/bots/how-to/conversations/send-proactive-messages.md)
* [Другой модуль задач.](#respond-with-another-task-module)Вы можете отвечать дополнительным модулем задач в рамках многоэтапного взаимодействия.
* [Ответ на карточку.](#respond-with-a-card-inserted-into-the-compose-message-area)Вы можете отвечать карточкой, с помощью которую пользователь может взаимодействовать или вставлять в сообщение.
* [Адаптивная карта из бота.](#bot-response-with-adaptive-card)Вставьте адаптивную карточку непосредственно в беседу.
* [Запрос пользователя на проверку подлинности.](~/messaging-extensions/how-to/add-authentication.md)
* [Запрос пользователя на предоставление дополнительной конфигурации]~/get-started/first-message-extension.md).

Для проверки подлинности или настройки после завершения процесса пользователь вызывает повторное вызов в веб-службу. В следующей таблице показано, какие типы ответов доступны в зависимости от расположения ссылок расширения `commandContext` обмена сообщениями: 

|Тип ответа | Создание | Командная планка | Сообщение |
|--------------|:-------------:|:-------------:|:---------:|
|Ответ на карточку | ✔ | ✔ | ✔ |
|Другой модуль задач | ✔ | ✔ | ✔ |
|Бот с адаптивной картой | ✔ | x | ✔ |
| Нет ответа | ✔ | ✔ | ✔ |

> [!NOTE]
> * Когда вы выбираете **Action.Submit** через карточки ME, он отправляет действие вызова с именем **composeExtension,** где значение равно обычной полезной нагрузке.
> * При выборе **Action.Submit** с помощью беседы вы получаете действие сообщения с именем **onCardButtonClicked,** где значение равно обычной полезной нагрузке.

## <a name="the-submitaction-invoke-event"></a>Событие вызовов submitAction

Примеры получения сообщения вызова приводятся следующим образом:

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

Это пример получаемого объекта JSON. Параметр `commandContext` указывает, откуда было вызвано расширение обмена сообщениями. Объект содержит поля формы в качестве `data` параметров и значения, которые пользователь представил. Объект JSON здесь сокращен, чтобы выделить наиболее релевантные поля.

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Ответьте карточкой, вставленной в область составить сообщение

Наиболее распространенный способ ответа на запрос — это карта, вставленная в область `composeExtension/submitAction` составить сообщение. Пользователь передает карточку в беседу. Дополнительные сведения об использовании карт см. в [карточках и действиях карт.](~/task-modules-and-cards/cards/cards-actions.md)

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

## <a name="respond-with-another-task-module"></a>Ответ с помощью другого модуля задач

Вы можете выбрать, чтобы ответить на `submitAction` событие с помощью дополнительного модуля задач. Это полезно, когда:

* Необходимо собирать большие объемы информации.
* Необходимо динамически изменить собираемую информацию на основе ввода пользователя.
* Необходимо проверить сведения, представленные пользователем, и повторно отправить форму с сообщением об ошибке, если что-то не так. 

Метод ответа такой же, как [и ответ на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md) Если вы используете SDK Bot Framework, для отправки действий запускается одно и то же событие. Чтобы сделать эту работу, необходимо добавить логику, которая определяет правильный ответ.

## <a name="bot-response-with-adaptive-card"></a>Ответ бота с адаптивной картой

> [!NOTE]
> Обязательным условием получения ответа бота с адаптивной картой является то, что необходимо добавить объект в манифест приложения и определить требуемую область `bot` для бота. Используйте тот же ID, что и расширение обмена сообщениями для бота.
 
Вы также можете ответить на сообщение, вставив сообщение с адаптивной картой `submitAction` в канал с помощью бота. Пользователь может предварительно просмотреть сообщение перед его отправкой. Это очень полезно в сценариях, в которых вы собираете информацию от пользователей перед созданием ответа адаптивной карты или при обновлении карты после ее взаимодействия с ней. 

В следующем сценарии показано, как приложение Polly настраивает опрос, не включая этапы настройки в диалог канала:

**Настройка опроса**

1. Пользователь выбирает расширение обмена сообщениями для вызова модуля задач.
1. Пользователь настраивает опрос с помощью модуля задач.
1. После отправки модуля задач приложение использует сведения, предоставленные для создания опроса в качестве адаптивной карты, и отправляет его в качестве ответа `botMessagePreview` клиенту.
1. Затем пользователь может просмотреть сообщение адаптивной карты, прежде чем бот вставляет его в канал. Если приложение еще не является участником канала, выберите `Send` добавить его.

    > [!NOTE] 
    > * Пользователи также могут выбрать `Edit` сообщение, которое возвращает их в исходный модуль задач. 
    > * Взаимодействие с адаптивной картой изменяет сообщение перед отправкой.
1. После выбора пользователем `Send` бота сообщение передается в канал.

## <a name="respond-to-initial-submit-action"></a>Реагирование на начальное действие отправки

Модуль задач должен отвечать на начальное сообщение предварительным просмотром карты, которую отправляет бот `composeExtension/submitAction` каналу. Пользователь может проверить карту перед отправкой, а также попытаться установить бот в беседе, если бот еще не установлен.

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

> [!NOTE]
> * Необходимо содержать действие с одним вложением `activityPreview` `message` адаптивной карты. Значение `<< Card Payload >>` — это местоодатель для карточки, которая будет отправляться.

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>BotMessagePreview отправляет и редактирует события

Расширение обмена сообщениями должно отвечать на два новых типа `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"` и `value.botMessagePreviewAction = "edit"` .

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

### <a name="respond-to-botmessagepreview-edit"></a>Ответ на изменение botMessagePreview

Если пользователь перед отправкой редактирует карту, выбрав **изменение,** вы получите вызов `composeExtension/submitAction` с помощью `value.botMessagePreviewAction = edit` . Вы должны ответить, возвращая отправленный модуль задач в ответ на начальный вызов, `composeExtension/fetchTask` который начал взаимодействие. Это позволяет пользователю начать процесс повторного ввода исходной информации. Используйте доступные сведения для обновления модуля задач, чтобы пользователю не было необходимости заполнять всю информацию с нуля.
Дополнительные сведения об ответе на начальное событие см. в `fetchTask` [ответе на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md)

### <a name="respond-to-botmessagepreview-send"></a>Ответ на отправку botMessagePreview

После того как пользователь выбирает **отправку,** вы получите вызов `composeExtension/submitAction` с `value.botMessagePreviewAction = send` . Веб-служба должна создать и отправить на беседу проактивное сообщение с адаптивной картой, а также ответить на вызов.

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

### <a name="user-attribution-for-bots-messages"></a>Атрибуция пользователей для сообщений ботов 

В сценариях, когда бот отправляет сообщения от имени пользователя, приписка сообщения этому пользователю помогает с вовлечением и демонстрирует более естественный поток взаимодействия. Эта функция позволяет приписать сообщение от бота пользователю, от имени которого оно было отправлено.

На следующем изображении слева находится сообщение карточки, отправленное ботом без атрибуции пользователя, а справа — карточка, отправленная ботом с атрибуцией пользователя.

![Боты атрибуции пользователей](../../../assets/images/messaging-extension/user-attribution-bots.png)

Чтобы использовать атрибутику пользователя в командах, необходимо добавить объект упоминания в полезной нагрузке, которая отправляется в `OnBehalfOf` `ChannelData` `Activity` Teams.

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

#### <a name="details-of--onbehalfof-entity-schema"></a>Сведения о  `OnBehalfOf` схеме сущности

В следующем разделе описаны сущностями в `OnBehalfOf` массиве:

|Поле|Тип|Описание|
|:---|:---|:---|
|`itemId`|Целое число|Описывает идентификацию элемента. Его значение должно быть `0` .|
|`mentionType`|String|Описывает упоминание о "человеке".|
|`mri`|String|Идентификатор ресурса сообщений (MRI) человека, от имени которого отправляется сообщение. Имя отправитель сообщения будет отображаться как \<user\> \<bot name\> "через".|
|`displayName`|Строка|Имя человека. Используется в качестве отката в разрешении имени случая недоступно.|
  
## <a name="code-sample"></a>Пример кода

| Имя образца           | Описание | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams расширения обмена сообщениями| Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams расширения обмена сообщениями   |  Описывает, как определить команды поиска и реагировать на поиски.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Определить команды поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)

