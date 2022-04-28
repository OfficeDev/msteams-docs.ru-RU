---
title: Ответ на действие отправки модуля задач
author: surbhigupta
description: Описывает, как реагировать на действие отправки модуля задачи из команды действия расширения сообщения с помощью упреждающего сообщения, другого модуля задачи, бота адаптивной карточки и т. д. с помощью примеров кода.
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 4cd42fec6209b79a43ba6cc7489d5ac9afea3759
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104478"
---
# <a name="respond-to-the-task-module-submit-action"></a>Ответ на действие отправки модуля задач

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

В этом документе описывается, как ваше приложение реагирует на команды действий, такие как действие отправки модуля задач пользователя.
После того как пользователь отправит модуль задачи, `composeExtension/submitAction` веб-служба получит сообщение об вызове с идентификатором команды и значениями параметров. У приложения есть пять секунд для ответа на вызов. В противном случае пользователь получает сообщение об ошибке **"Не** удается подключиться к приложению", а любой ответ на вызов игнорируется Teams клиентом.

У вас есть следующие варианты ответа:

* Нет ответа: используйте действие отправки, чтобы активировать процесс во внешней системе и не предоставлять пользователю никаких отзывов. Это полезно для длительных процессов и для предоставления обратной связи по-другому. Например, вы можете оставить отзыв с [упреждающим сообщением](~/bots/how-to/conversations/send-proactive-messages.md).
* [Другой модуль задач](#respond-with-another-task-module). Вы можете ответить дополнительным модулем задачи в рамках многоэтапного взаимодействия.
* [Ответ карточки](#respond-with-a-card-inserted-into-the-compose-message-area): вы можете ответить карточкой, с помощью которую пользователь может взаимодействовать или вставить сообщение.
* [Адаптивная карточка из бота](#bot-response-with-adaptive-card): вставка адаптивной карточки непосредственно в беседу.
* [Запрос пользователя на проверку подлинности](~/messaging-extensions/how-to/add-authentication.md).
* [Запросите у пользователя дополнительную конфигурацию](~/get-started/first-message-extension.md).

Для проверки подлинности или настройки после того, как пользователь завершит процесс, исходный вызов будет повторно вызван в веб-службу. В следующей таблице показано, какие типы ответов доступны в зависимости `commandContext` от расположения вызова расширения сообщения:

|Тип ответа | Создание | Панель команд | Сообщение |
|--------------|:-------------:|:-------------:|:---------:|
|Ответ карточки | ✔ | ✔ | ✔ |
|Другой модуль задачи | ✔ | ✔ | ✔ |
|Бот с адаптивной карточкой | ✔ | x | ✔ |
| Нет ответа | ✔ | ✔ | ✔ |

> [!NOTE]
>
> * При выборе **action.Submit** с помощью карточек ME он отправляет действие вызова с именем **composeExtension**, где значение равно обычным полезным данным.
> * При выборе **Action.Submit** через беседу вы получаете действие сообщения с именем **onCardButtonClicked**, где значение равно обычным полезным данным.

Если приложение содержит чат-бот, установите бот в беседе и загрузите модуль задачи. Бот полезен для получения дополнительного контекста для модуля задачи. Сведения об установке чат-бота см. в разделе ["Запрос на установку бота для общения"](create-task-module.md#request-to-install-your-conversational-bot).

## <a name="the-submitaction-invoke-event"></a>Событие вызова submitAction

Ниже приведены примеры получения сообщения об вызове.

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

Это пример получаемого объекта JSON. Параметр `commandContext` указывает, откуда было запущено расширение сообщения. Объект `data` содержит поля в форме в качестве параметров и значения, отправленные пользователем. Объект JSON выделяет наиболее релевантные поля.

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>Ответ с помощью карточки, вставленной в область сообщения создания

Чаще всего ответ на `composeExtension/submitAction` запрос выполняется с помощью карточки, вставленной в область сообщения создания. Пользователь отправляет карточку в беседу. Дополнительные сведения об использовании карточек см. [в разделе карточек и действий с карточками](~/task-modules-and-cards/cards/cards-actions.md).

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

Вы можете ответить на событие с `submitAction` помощью дополнительного модуля задачи. Это полезно в следующих случаях:

* Сбор больших объемов информации.
* Динамическое изменение коллекции сведений на основе введенных пользователем данных.
* Проверьте данные, отправленные пользователем, и повторно передайте форму с сообщением об ошибке, если что-то не так.

Метод ответа совпадает с ответом [на исходное `fetchTask` событие](~/messaging-extensions/how-to/action-commands/create-task-module.md). Если вы используете пакет SDK Bot Framework, для обоих действий отправки используются одинаковые триггеры событий. Чтобы сделать это, необходимо добавить логику, которая определяет правильный ответ.

## <a name="bot-response-with-adaptive-card"></a>Ответ бота с адаптивной карточкой

> [!NOTE]
> Чтобы получить ответ бота `bot` с адаптивной карточкой, необходимо добавить объект в манифест приложения и определить требуемую область для бота. Используйте тот же идентификатор, что и расширение сообщения для бота.

Вы также можете ответить на сообщение `submitAction` , вставив сообщение с адаптивной карточкой в канал с помощью бота. Пользователь может просмотреть сообщение перед его отправкой. Это полезно в сценариях, когда вы собираете сведения от пользователей перед созданием ответа адаптивной карточки или обновляете карточку после взаимодействия с ней.

В следующем сценарии показано, как приложение Polly настраивает опрос без указания шагов настройки в беседе канала:

Чтобы настроить опрос, выполните указанные ниже действия.

1. Пользователь выбирает расширение сообщения для вызова модуля задачи.
1. Пользователь настраивает опрос с помощью модуля задачи.
1. После отправки модуля задачи приложение использует сведения, `botMessagePreview` предоставленные для создания опроса в качестве адаптивной карточки, и отправляет его в качестве ответа клиенту.
1. Затем пользователь может просмотреть сообщение адаптивной карточки, прежде чем бот вставит его в канал. Если приложение не является членом канала, `Send` выберите, чтобы добавить его.

    > [!NOTE]
    >
    > * Пользователи также могут выбрать сообщение `Edit` , которое возвращает их в исходный модуль задачи.
    > * Взаимодействие с адаптивной карточкой изменяет сообщение перед отправкой.
    >
1. Когда пользователь выберет бота `Send` , сообщение будет отправлено в канал.

## <a name="respond-to-initial-submit-action"></a>Реагирование на первоначальное действие отправки

Модуль задачи должен ответить на исходное `composeExtension/submitAction` сообщение с предварительной версией карточки, которую бот отправляет в канал. Пользователь может проверить карточку перед отправкой и попытаться установить бот в беседе, если бот еще не установлен.

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
>
> * Должен `activityPreview` содержать действие с `message` одним вложением адаптивной карточки. Значение `<< Card Payload >>` является заполнителем для карточки, которую вы хотите отправить.

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

Расширение сообщения должно отвечать на два новых `composeExtension/submitAction` типа вызова: where `value.botMessagePreviewAction = "send"`и `value.botMessagePreviewAction = "edit"`.

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

### <a name="respond-to-botmessagepreview-edit"></a>Реагирование на изменение botMessagePreview

Если пользователь изменяет карточку перед отправкой, выбрав команду **"** Изменить", вы получите `composeExtension/submitAction` вызов с `value.botMessagePreviewAction = edit`помощью . Ответ, возвращая отправленный модуль задачи в ответ на `composeExtension/fetchTask` начальный вызов, который начал взаимодействие. Это позволяет пользователю начать процесс, повторно введите исходные сведения. Используйте доступные сведения, чтобы обновить модуль задачи, чтобы пользователю не нужно было заполнять всю информацию с нуля.
Дополнительные сведения об ответе на исходное `fetchTask` событие см. [в ответе на исходное `fetchTask` событие](~/messaging-extensions/how-to/action-commands/create-task-module.md).

### <a name="respond-to-botmessagepreview-send"></a>Ответ на отправку botMessagePreview

Когда пользователь нажмет **кнопку "Отправить**", вы получите вызов `composeExtension/submitAction` с помощью `value.botMessagePreviewAction = send`. Веб-служба должна создать и отправить в беседу упреждающее сообщение с адаптивной карточкой, а также ответить на вызов.

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

Вы получите новое сообщение `composeExtension/submitAction` , аналогичное следующему:

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

### <a name="user-attribution-for-bots-messages"></a>Атрибуты пользователей для сообщений ботов

В сценариях, когда бот отправляет сообщения от имени пользователя, атрибутив сообщение этому пользователю, помогает обеспечить вовлеченность и продемонстрировать более естественный поток взаимодействия. Эта функция позволяет атрибутив сообщение от бота пользователю, от имени которого оно было отправлено.

На следующем рисунке слева отображается сообщение карточки, отправленное ботом без атрибута пользователя, а справа — карточка, отправленная ботом с атрибутом пользователя.

![Боты атрибутов пользователей](../../../assets/images/messaging-extension/user-attribution-bots.png)

Чтобы использовать атрибуты пользователей в командах, `OnBehalfOf` `ChannelData` `Activity` необходимо добавить сущность упоминания в полезные данные, отправляемые Teams.

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

В следующем разделе приводится описание сущностей в массиве `OnBehalfOf` :

|Поле|Тип|Описание|
|:---|:---|:---|
|`itemId`|Целое число|Описывает идентификацию элемента. Его значение должно быть .`0`|
|`mentionType`|String|Описывает упоминание "person".|
|`mri`|String|Идентификатор ресурса сообщения (MRI) пользователя, от имени которого отправляется сообщение. Имя отправителя сообщения будет отображаться как "\<user\> через \<bot name\>".|
|`displayName`|String|Имя человека. Используется в качестве резервного варианта в случае недоступности разрешения имен.|
  
## <a name="code-sample"></a>Пример кода

| Имя образца           | Описание | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams расширения сообщения| Описывает, как определить команды действий, создать модуль задач и реагировать на действие отправки модуля задачи. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams расширения сообщения   |  Описывает, как определить команды поиска и реагировать на поисковые запросы.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Определить команды поиска](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="see-also"></a>См. также

[Ответ на команду поиска](~/messaging-extensions/how-to/search-commands/respond-to-search.md)
