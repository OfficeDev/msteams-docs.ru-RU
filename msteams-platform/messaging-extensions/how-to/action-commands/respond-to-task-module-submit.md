---
title: Ответ на действие отправки модуля задач
author: clearab
description: Описывает, как реагировать на отправку действия модуля задач из команды действий расширения обмена сообщениями.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fecc0ace5f767da3764529a9e8a590b37e547bb0
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827944"
---
# <a name="respond-to-the-task-module-submit-action"></a>Ответ на действие отправки модуля задач

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

После отправки модуля задач веб-служба получает сообщение вызова с командным `composeExtension/submitAction` ИД и значениями параметров. У приложения есть пять секунд для ответа на вызов,  в противном случае пользователь получает сообщение об ошибке, которое не может достичь приложения, а любой ответ на вызов игнорируется клиентом Teams.

У вас есть следующие параметры для ответа:

* Нет ответа . Вы можете использовать действие отправки для запуска процесса во внешней системе и не предоставлять пользователю никаких отзывов. Это может быть полезно для длительных процессов, и вы можете предоставить обратную связь другим способом (например, с проактивным [сообщением.](~/bots/how-to/conversations/send-proactive-messages.md)
* [Другой модуль задач](#respond-with-another-task-module) — вы можете отвечать дополнительным модулем задач в рамках многоэтапного взаимодействия.
* [Ответ на](#respond-with-a-card-inserted-into-the-compose-message-area) карточку . Вы можете отвечать карточкой, с помощью которую пользователь может взаимодействовать и/или вставлять в сообщение.
* [Адаптивная карта от бота](#bot-response-with-adaptive-card) — вставьте адаптивную карточку непосредственно в беседу.
* [Запрос на проверку подлинности пользователя](~/messaging-extensions/how-to/add-authentication.md)
* [Запрос на предоставление пользователем дополнительной конфигурации](~/messaging-extensions/how-to/add-configuration-page.md)

Для проверки подлинности или настройки после завершения потока исходный вызов будет повторно отправлен в веб-службу. В следующей таблице показано, какие типы ответов доступны в зависимости от расположения ссылок расширения `commandContext` обмена сообщениями: 

|Тип ответа | составить | панель команд | message |
|--------------|:-------------:|:-------------:|:---------:|
|Ответ на карточку | x | x | x |
|Другой модуль задач | x | x | x |
|Бот с адаптивной картой | x |  | x |
| Нет ответа | x | x | x |

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

Наиболее распространенный способ ответа на запрос — это карта, вставленная в область `composeExtension/submitAction` составить сообщение. Затем пользователь может отправить карточку в беседу. Дополнительные сведения об использовании карт см. [в карточках и действиях карт.](~/task-modules-and-cards/cards/cards-actions.md)

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

Вы можете ответить на событие с `submitAction` помощью дополнительного модуля задач. Это может быть полезно, если:

* Необходимо собирать большие объемы информации.
* При необходимости динамического изменения собираемой информации на основе ввода пользователя
* Если необходимо проверить сведения, представленные пользователем, и потенциально повторно отправить форму сообщением об ошибке, если что-то не так. 

Метод ответа такой же, как [и ответ на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md) Если вы используете SDK Bot Framework, для отправки действий запускается одно и то же событие. Это означает, что необходимо добавить логику, которая определяет правильный ответ.

## <a name="bot-response-with-adaptive-card"></a>Ответ бота с адаптивной картой

>[!Note]
>Этот поток требует, чтобы вы добавили объект в манифест приложения и чтобы у вас была необходимая область, `bot` определяемая для бота. Используйте тот же ID, что и расширение обмена сообщениями для бота.

Вы также можете ответить на действие отправки, вставив сообщение с адаптивной картой в канал с помощью бота. Пользователь может предварительно просмотреть сообщение перед отправкой, а также, возможно, изменить или взаимодействовать с ним. Это может быть очень полезно в сценариях, в которых вы собираете информацию от пользователей перед созданием адаптивного ответа карточки или при обновлении карты после ее взаимодействия с ней. В следующем сценарии показано, как приложение Polly использует этот поток для настройки опроса без включаемых этапов настройки в диалог канала:

1. Пользователь выбирает расширение обмена сообщениями, чтобы вызвать модуль задач.
2. Пользователь настраивает опрос с помощью модуля задач.
3. После отправки модуля задач приложение использует сведения, предоставленные для построения опроса в качестве адаптивной карты, и отправляет его в качестве ответа `botMessagePreview` клиенту.
4. Затем пользователь может просмотреть сообщение адаптивной карты, прежде чем бот вставляет его в канал. Если приложение еще не является участником канала, выбор добавляет `Send` его.
   1. Пользователь также может выбрать сообщение, которое возвращает их в `Edit` исходный модуль задач.
5. Взаимодействие с адаптивной картой изменяет сообщение перед отправкой.
6. После выбора пользователем `Send` бота сообщение передается в канал.

### <a name="respond-to-initial-submit-action"></a>Реагирование на начальное действие отправки

Чтобы включить этот поток, модуль задач должен ответить на начальное сообщение предварительным просмотром карты, которую бот `composeExtension/submitAction` отправляет каналу. Это дает пользователю возможность проверить карту перед отправкой, а также попытаться установить бот в беседе, если она еще не установлена.

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
>Должен содержать действие с 1 адаптивным `activityPreview` вложением `message` карт. Значение `<< Card Payload >>` является местообнамерщиком для карточки, вы хотите отправить.

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

Расширение сообщения должно реагировать сейчас на два новых варианта `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"` и `value.botMessagePreviewAction = "edit"` .

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

Если пользователь перед отправкой редактирует карту, выбрав кнопку **Изменить,** вы получите вызов `composeExtension/submitAction` с помощью `value.botMessagePreviewAction = edit` . Обычно следует отвечать, возвращая отправленный модуль задач в ответ на начальный вызов, `composeExtension/fetchTask` который начал взаимодействие. Это позволяет пользователю начать процесс с повторного ввода исходной информации. Используйте доступную информацию для предварительного заполнения модуля задач, чтобы пользователю не нужно было заполнять всю информацию с нуля.

См. [ответы на начальное `fetchTask` событие](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Ответ на отправку botMessagePreview

После того как пользователь выберет кнопку **Отправка,** вы получите вызов `composeExtension/submitAction` с `value.botMessagePreviewAction = send` . Веб-служба должна создать и отправить на беседу проактивное сообщение с адаптивной картой, а также ответить на вызов.

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

В сценариях, когда бот отправляет сообщения от имени пользователя, приписывая сообщение этому пользователю, можно помочь с вовлечением и продемонстрировать более естественный поток взаимодействия. Эта функция позволяет приписать сообщение от бота пользователю, от имени которого оно было отправлено.

На следующем изображении слева находится сообщение карточки, отправленное ботом без атрибуции  пользователя, а справа — карточка, отправленная ботом с атрибуцией пользователя. 

![Снимок экрана](../../../assets/images/messaging-extension/user-attribution-bots.png)

Чтобы использовать атрибутику пользователя в командах, необходимо добавить объект упоминания в полезной нагрузке, которая `OnBehalfOf` `ChannelData` `Activity` отправляется в Teams.

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

Ниже приводится описание сущностями в `OnBehalfOf` массиве:

#### <a name="details-of--onbehalfof-entity-schema"></a>Сведения о  `OnBehalfOf` схеме сущности

|Поле|Тип|Описание|
|:---|:---|:---|
|`itemId`|Целое число|Должно быть 0|
|`mentionType`|Строка|Должно быть "лицом"|
|`mri`|Строка|Идентификатор ресурса сообщений (MRI) человека, от имени которого отправляется сообщение. Имя отправитель сообщения будет отображаться как \<user\> \<bot name\> "через".|
|`displayName`|Строка|Имя человека. Используется в качестве отката в разрешении имени случая недоступно.|
  
## <a name="next-steps"></a>Дальнейшие действия

Добавление команды поиска

* [Определить команды поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
