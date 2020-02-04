---
title: Создание и отправка модуля задач
author: clearab
description: Обработка начального действия Invoke и ответ с модулем задачи из команды расширения для обмена сообщениями о действиях
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f5f96e71517d45f52d17d2d70c583ec1eec3babd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675484"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="3c788-103">Создание и отправка модуля задач</span><span class="sxs-lookup"><span data-stu-id="3c788-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="3c788-104">Если вы не заполняете модуль задач параметрами, определенными в манифесте приложения, вам потребуется создать модуль задачи, который будет представлен пользователям.</span><span class="sxs-lookup"><span data-stu-id="3c788-104">If you are not populating your task module with parameters defined in your app manifest, you'll need to create the task module to be presented to your users.</span></span> <span data-ttu-id="3c788-105">Можно использовать либо адаптивную карту, либо встроенное веб-представление.</span><span class="sxs-lookup"><span data-stu-id="3c788-105">You can use either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="3c788-106">Начальный запрос вызова</span><span class="sxs-lookup"><span data-stu-id="3c788-106">The initial invoke request</span></span>

<span data-ttu-id="3c788-107">При использовании этого метода служба получает `Activity` объект типа `composeExtension/fetchTask`, и вам потребуется ответить на `task` объект, содержащий либо адаптивную карту, либо URL-адрес встроенного веб-представления.</span><span class="sxs-lookup"><span data-stu-id="3c788-107">Using this method you service will receive an `Activity` object of type `composeExtension/fetchTask`, and you'll need to respond with a `task` object containing either the adaptive card or a URL to the embedded web view.</span></span> <span data-ttu-id="3c788-108">В дополнение к стандартным свойствам действия Bot, начальная полезная нагрузка вызова содержит следующие метаданные запроса:</span><span class="sxs-lookup"><span data-stu-id="3c788-108">In addition to the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="3c788-109">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="3c788-109">Property name</span></span>|<span data-ttu-id="3c788-110">Назначение</span><span class="sxs-lookup"><span data-stu-id="3c788-110">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="3c788-111">Тип запроса; должно быть `invoke`.</span><span class="sxs-lookup"><span data-stu-id="3c788-111">Type of request; must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="3c788-112">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="3c788-112">Type of command that is issued to your service.</span></span> <span data-ttu-id="3c788-113">Будет `composeExtension/fetchTask`.</span><span class="sxs-lookup"><span data-stu-id="3c788-113">Will be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="3c788-114">Идентификатор пользователя, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="3c788-114">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="3c788-115">Имя пользователя, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="3c788-115">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="3c788-116">Идентификатор объекта Azure Active Directory пользователя, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="3c788-116">Azure Active Directory object id of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="3c788-117">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c788-117">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="3c788-118">Идентификатор канала (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="3c788-118">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="3c788-119">Идентификатор группы (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="3c788-119">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="3c788-120">Содержит идентификатор вызываемой команды.</span><span class="sxs-lookup"><span data-stu-id="3c788-120">Contains the Id of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="3c788-121">Контекст, который инициировал событие.</span><span class="sxs-lookup"><span data-stu-id="3c788-121">The context that triggered the event.</span></span> <span data-ttu-id="3c788-122">Будет `compose`.</span><span class="sxs-lookup"><span data-stu-id="3c788-122">Will be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="3c788-123">Тема клиента пользователя, которая полезна для встроенного форматирования веб-представления.</span><span class="sxs-lookup"><span data-stu-id="3c788-123">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="3c788-124">Будет иметь `default` `contrast` или `dark`.</span><span class="sxs-lookup"><span data-stu-id="3c788-124">Will be `default`, `contrast` or `dark`.</span></span> |

### <a name="example-fetchtask-request"></a><span data-ttu-id="3c788-125">Пример запроса Фетчтаск</span><span class="sxs-lookup"><span data-stu-id="3c788-125">Example fetchTask request</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="3c788-126">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="3c788-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="3c788-127">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="3c788-127">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="3c788-128">JSON</span><span class="sxs-lookup"><span data-stu-id="3c788-128">JSON</span></span>](#tab/json)

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

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="3c788-129">Запрос начального вызова из сообщения</span><span class="sxs-lookup"><span data-stu-id="3c788-129">Initial invoke request from a message</span></span>

<span data-ttu-id="3c788-130">Когда Bot вызывается из сообщения, а не из области создания или панели команд, `value` объект в исходном запросе будет содержать сведения о сообщении, из которого было вызвано расширение системы обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="3c788-130">When your bot is invoked from a message rather than the compose area or the command bar, the `value` object in the initial request will contain the details of the message your messaging extension was invoked from.</span></span> <span data-ttu-id="3c788-131">Ниже приведен пример этого объекта.</span><span class="sxs-lookup"><span data-stu-id="3c788-131">An example of this object is below.</span></span> <span data-ttu-id="3c788-132">`reactions` Массивы `mentions` и массивы являются необязательными и не будут представлены, если в исходном сообщении нет реакции или упоминаний.</span><span class="sxs-lookup"><span data-stu-id="3c788-132">The `reactions` and `mentions` arrays are optional, and will not be present if there are no reactions or mentions in the original message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="3c788-133">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="3c788-133">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="3c788-134">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="3c788-134">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="3c788-135">JSON</span><span class="sxs-lookup"><span data-stu-id="3c788-135">JSON</span></span>](#tab/json)

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

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="3c788-136">Ответ на Фетчтаск</span><span class="sxs-lookup"><span data-stu-id="3c788-136">Respond to the fetchTask</span></span>

<span data-ttu-id="3c788-137">Ответьте на запрос Invoke с `task` объектом, который содержит `taskInfo` объект со адаптивной картой или URL-адресом или простым строковым сообщением.</span><span class="sxs-lookup"><span data-stu-id="3c788-137">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the adaptive card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="3c788-138">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="3c788-138">Property name</span></span>|<span data-ttu-id="3c788-139">Назначение</span><span class="sxs-lookup"><span data-stu-id="3c788-139">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="3c788-140">Может быть либо `continue` представление формы, либо `message` простое всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="3c788-140">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="3c788-141">Либо `taskInfo` объект для формы, либо сообщение `string` для сообщения.</span><span class="sxs-lookup"><span data-stu-id="3c788-141">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="3c788-142">Схема для объекта Таскинфо:</span><span class="sxs-lookup"><span data-stu-id="3c788-142">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="3c788-143">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="3c788-143">Property name</span></span>|<span data-ttu-id="3c788-144">Назначение</span><span class="sxs-lookup"><span data-stu-id="3c788-144">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="3c788-145">Название модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="3c788-145">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="3c788-146">Может быть либо целым числом (в пикселях) `small`, `medium`либо `large`,,.</span><span class="sxs-lookup"><span data-stu-id="3c788-146">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="3c788-147">Может быть либо целым числом (в пикселях) `small`, `medium`либо `large`,,.</span><span class="sxs-lookup"><span data-stu-id="3c788-147">Can be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="3c788-148">Адаптивная карточка, определяющая форму (если она используется).</span><span class="sxs-lookup"><span data-stu-id="3c788-148">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="3c788-149">URL-адрес, который должен быть открыт в модуле задач как Внедренное представление веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="3c788-149">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="3c788-150">Если клиент не поддерживает функцию модуля задач, этот URL-адрес открывается на вкладке браузера.</span><span class="sxs-lookup"><span data-stu-id="3c788-150">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="with-an-adaptive-card"></a><span data-ttu-id="3c788-151">С помощью адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="3c788-151">With an adaptive card</span></span>

<span data-ttu-id="3c788-152">При использовании адаптивной карты необходимо ответить на `task` объект с `value` объектом, содержащим адаптивную карточку.</span><span class="sxs-lookup"><span data-stu-id="3c788-152">When using an adaptive card, you'll need to respond with a `task` object with the `value` object containing an adaptive card.</span></span>

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a><span data-ttu-id="3c788-153">Пример ответа Фетчтаск с помощью адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="3c788-153">Example fetchTask response with an adaptive card</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="3c788-154">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="3c788-154">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="3c788-155">В этом примере используется [пакет NuGet адаптивекардс](https://www.nuget.org/packages/AdaptiveCards) в дополнение к пакету SDK для Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="3c788-155">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

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

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="3c788-156">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="3c788-156">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="3c788-157">JSON</span><span class="sxs-lookup"><span data-stu-id="3c788-157">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "card":
      {
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
        ],
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json"
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a><span data-ttu-id="3c788-158">С внедренным представлением веб-сайта</span><span class="sxs-lookup"><span data-stu-id="3c788-158">With an embedded web view</span></span>

<span data-ttu-id="3c788-159">При использовании внедренного веб-представления необходимо ответить на `task` объект с `value` объектом, содержащим URL-адрес веб-формы, которую нужно загрузить.</span><span class="sxs-lookup"><span data-stu-id="3c788-159">When using an embedded web view, you'll need to respond with a `task` object with the `value` object containing the URL to the web form you'd like to load.</span></span> <span data-ttu-id="3c788-160">Домены любого URL-адреса, который вы хотите загрузить, должны быть `validDomains` включены в массив манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="3c788-160">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="3c788-161">В [документации модуля задачи](~/task-modules-and-cards/what-are-task-modules.md) представлены полные сведения о создании внедренного веб-представления.</span><span class="sxs-lookup"><span data-stu-id="3c788-161">See the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md) for complete information on building your embedded web view.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="3c788-162">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="3c788-162">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="3c788-163">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="3c788-163">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="3c788-164">JSON</span><span class="sxs-lookup"><span data-stu-id="3c788-164">JSON</span></span>](#tab/json)

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

## <a name="next-steps"></a><span data-ttu-id="3c788-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c788-165">Next steps</span></span>

<span data-ttu-id="3c788-166">Если вы разрешите пользователям отправку ответа из модуля задач, необходимо обработать действие отправки.</span><span class="sxs-lookup"><span data-stu-id="3c788-166">If you allow your users to send a response back from the task module, you'll need to handle the submit action.</span></span>

* [<span data-ttu-id="3c788-167">Создание модуля задачи и ответ на него</span><span class="sxs-lookup"><span data-stu-id="3c788-167">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
