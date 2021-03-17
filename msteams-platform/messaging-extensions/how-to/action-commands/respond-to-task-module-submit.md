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
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="3dafd-103">Ответ на действие отправки модуля задач</span><span class="sxs-lookup"><span data-stu-id="3dafd-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="3dafd-104">После отправки модуля задач веб-служба получает сообщение вызова с командным `composeExtension/submitAction` ИД и значениями параметров.</span><span class="sxs-lookup"><span data-stu-id="3dafd-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="3dafd-105">У приложения есть пять секунд для ответа на вызов,  в противном случае пользователь получает сообщение об ошибке, которое не может достичь приложения, а любой ответ на вызов игнорируется клиентом Teams.</span><span class="sxs-lookup"><span data-stu-id="3dafd-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message **Unable to reach the app** and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="3dafd-106">У вас есть следующие параметры для ответа:</span><span class="sxs-lookup"><span data-stu-id="3dafd-106">You have the following options for responding:</span></span>

* <span data-ttu-id="3dafd-107">Нет ответа . Вы можете использовать действие отправки для запуска процесса во внешней системе и не предоставлять пользователю никаких отзывов.</span><span class="sxs-lookup"><span data-stu-id="3dafd-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="3dafd-108">Это может быть полезно для длительных процессов, и вы можете предоставить обратную связь другим способом (например, с проактивным [сообщением.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="3dafd-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="3dafd-109">[Другой модуль задач](#respond-with-another-task-module) — вы можете отвечать дополнительным модулем задач в рамках многоэтапного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="3dafd-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="3dafd-110">[Ответ на](#respond-with-a-card-inserted-into-the-compose-message-area) карточку . Вы можете отвечать карточкой, с помощью которую пользователь может взаимодействовать и/или вставлять в сообщение.</span><span class="sxs-lookup"><span data-stu-id="3dafd-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="3dafd-111">[Адаптивная карта от бота](#bot-response-with-adaptive-card) — вставьте адаптивную карточку непосредственно в беседу.</span><span class="sxs-lookup"><span data-stu-id="3dafd-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="3dafd-112">Запрос на проверку подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="3dafd-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="3dafd-113">Запрос на предоставление пользователем дополнительной конфигурации</span><span class="sxs-lookup"><span data-stu-id="3dafd-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="3dafd-114">Для проверки подлинности или настройки после завершения потока исходный вызов будет повторно отправлен в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="3dafd-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="3dafd-115">В следующей таблице показано, какие типы ответов доступны в зависимости от расположения ссылок расширения `commandContext` обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="3dafd-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="3dafd-116">Тип ответа</span><span class="sxs-lookup"><span data-stu-id="3dafd-116">Response Type</span></span> | <span data-ttu-id="3dafd-117">составить</span><span class="sxs-lookup"><span data-stu-id="3dafd-117">compose</span></span> | <span data-ttu-id="3dafd-118">панель команд</span><span class="sxs-lookup"><span data-stu-id="3dafd-118">command bar</span></span> | <span data-ttu-id="3dafd-119">message</span><span class="sxs-lookup"><span data-stu-id="3dafd-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="3dafd-120">Ответ на карточку</span><span class="sxs-lookup"><span data-stu-id="3dafd-120">Card response</span></span> | <span data-ttu-id="3dafd-121">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-121">x</span></span> | <span data-ttu-id="3dafd-122">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-122">x</span></span> | <span data-ttu-id="3dafd-123">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-123">x</span></span> |
|<span data-ttu-id="3dafd-124">Другой модуль задач</span><span class="sxs-lookup"><span data-stu-id="3dafd-124">Another task module</span></span> | <span data-ttu-id="3dafd-125">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-125">x</span></span> | <span data-ttu-id="3dafd-126">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-126">x</span></span> | <span data-ttu-id="3dafd-127">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-127">x</span></span> |
|<span data-ttu-id="3dafd-128">Бот с адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="3dafd-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="3dafd-129">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-129">x</span></span> |  | <span data-ttu-id="3dafd-130">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-130">x</span></span> |
| <span data-ttu-id="3dafd-131">Нет ответа</span><span class="sxs-lookup"><span data-stu-id="3dafd-131">No response</span></span> | <span data-ttu-id="3dafd-132">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-132">x</span></span> | <span data-ttu-id="3dafd-133">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-133">x</span></span> | <span data-ttu-id="3dafd-134">x</span><span class="sxs-lookup"><span data-stu-id="3dafd-134">x</span></span> |

> [!NOTE]
> * <span data-ttu-id="3dafd-135">Когда вы выбираете **Action.Submit** через карточки ME, он отправляет действие вызова с именем **composeExtension,** где значение равно обычной полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="3dafd-135">When you select **Action.Submit** through ME cards, it sends invoke activity with the name **composeExtension**, where the value is equal to the usual payload.</span></span>
> * <span data-ttu-id="3dafd-136">При выборе **Action.Submit** с помощью беседы вы получаете действие сообщения с именем **onCardButtonClicked,** где значение равно обычной полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="3dafd-136">When you select **Action.Submit** through conversation, you receive message activity with the name **onCardButtonClicked**, where the value is equal to the usual payload.</span></span>

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="3dafd-137">Событие вызовов submitAction</span><span class="sxs-lookup"><span data-stu-id="3dafd-137">The submitAction invoke event</span></span>

<span data-ttu-id="3dafd-138">Примеры получения сообщения вызова приводятся следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3dafd-138">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3dafd-139">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3dafd-139">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="3dafd-140">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="3dafd-140">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="3dafd-141">JSON</span><span class="sxs-lookup"><span data-stu-id="3dafd-141">JSON</span></span>](#tab/json)

<span data-ttu-id="3dafd-142">Это пример получаемого объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="3dafd-142">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="3dafd-143">Параметр `commandContext` указывает, откуда было вызвано расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="3dafd-143">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="3dafd-144">Объект содержит поля формы в качестве `data` параметров и значения, которые пользователь представил.</span><span class="sxs-lookup"><span data-stu-id="3dafd-144">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="3dafd-145">Объект JSON здесь сокращен, чтобы выделить наиболее релевантные поля.</span><span class="sxs-lookup"><span data-stu-id="3dafd-145">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="3dafd-146">Ответьте карточкой, вставленной в область составить сообщение</span><span class="sxs-lookup"><span data-stu-id="3dafd-146">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="3dafd-147">Наиболее распространенный способ ответа на запрос — это карта, вставленная в область `composeExtension/submitAction` составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="3dafd-147">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="3dafd-148">Затем пользователь может отправить карточку в беседу.</span><span class="sxs-lookup"><span data-stu-id="3dafd-148">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="3dafd-149">Дополнительные сведения об использовании карт см. [в карточках и действиях карт.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="3dafd-149">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3dafd-150">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3dafd-150">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="3dafd-151">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="3dafd-151">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="3dafd-152">JSON</span><span class="sxs-lookup"><span data-stu-id="3dafd-152">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="3dafd-153">Ответ с помощью другого модуля задач</span><span class="sxs-lookup"><span data-stu-id="3dafd-153">Respond with another task module</span></span>

<span data-ttu-id="3dafd-154">Вы можете ответить на событие с `submitAction` помощью дополнительного модуля задач.</span><span class="sxs-lookup"><span data-stu-id="3dafd-154">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="3dafd-155">Это может быть полезно, если:</span><span class="sxs-lookup"><span data-stu-id="3dafd-155">This can be useful when:</span></span>

* <span data-ttu-id="3dafd-156">Необходимо собирать большие объемы информации.</span><span class="sxs-lookup"><span data-stu-id="3dafd-156">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="3dafd-157">При необходимости динамического изменения собираемой информации на основе ввода пользователя</span><span class="sxs-lookup"><span data-stu-id="3dafd-157">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="3dafd-158">Если необходимо проверить сведения, представленные пользователем, и потенциально повторно отправить форму сообщением об ошибке, если что-то не так.</span><span class="sxs-lookup"><span data-stu-id="3dafd-158">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="3dafd-159">Метод ответа такой же, как [и ответ на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="3dafd-159">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="3dafd-160">Если вы используете SDK Bot Framework, для отправки действий запускается одно и то же событие.</span><span class="sxs-lookup"><span data-stu-id="3dafd-160">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="3dafd-161">Это означает, что необходимо добавить логику, которая определяет правильный ответ.</span><span class="sxs-lookup"><span data-stu-id="3dafd-161">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="3dafd-162">Ответ бота с адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="3dafd-162">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="3dafd-163">Этот поток требует, чтобы вы добавили объект в манифест приложения и чтобы у вас была необходимая область, `bot` определяемая для бота.</span><span class="sxs-lookup"><span data-stu-id="3dafd-163">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="3dafd-164">Используйте тот же ID, что и расширение обмена сообщениями для бота.</span><span class="sxs-lookup"><span data-stu-id="3dafd-164">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="3dafd-165">Вы также можете ответить на действие отправки, вставив сообщение с адаптивной картой в канал с помощью бота.</span><span class="sxs-lookup"><span data-stu-id="3dafd-165">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="3dafd-166">Пользователь может предварительно просмотреть сообщение перед отправкой, а также, возможно, изменить или взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="3dafd-166">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="3dafd-167">Это может быть очень полезно в сценариях, в которых вы собираете информацию от пользователей перед созданием адаптивного ответа карточки или при обновлении карты после ее взаимодействия с ней.</span><span class="sxs-lookup"><span data-stu-id="3dafd-167">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="3dafd-168">В следующем сценарии показано, как приложение Polly использует этот поток для настройки опроса без включаемых этапов настройки в диалог канала:</span><span class="sxs-lookup"><span data-stu-id="3dafd-168">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="3dafd-169">Пользователь выбирает расширение обмена сообщениями, чтобы вызвать модуль задач.</span><span class="sxs-lookup"><span data-stu-id="3dafd-169">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="3dafd-170">Пользователь настраивает опрос с помощью модуля задач.</span><span class="sxs-lookup"><span data-stu-id="3dafd-170">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="3dafd-171">После отправки модуля задач приложение использует сведения, предоставленные для построения опроса в качестве адаптивной карты, и отправляет его в качестве ответа `botMessagePreview` клиенту.</span><span class="sxs-lookup"><span data-stu-id="3dafd-171">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="3dafd-172">Затем пользователь может просмотреть сообщение адаптивной карты, прежде чем бот вставляет его в канал.</span><span class="sxs-lookup"><span data-stu-id="3dafd-172">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="3dafd-173">Если приложение еще не является участником канала, выбор добавляет `Send` его.</span><span class="sxs-lookup"><span data-stu-id="3dafd-173">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="3dafd-174">Пользователь также может выбрать сообщение, которое возвращает их в `Edit` исходный модуль задач.</span><span class="sxs-lookup"><span data-stu-id="3dafd-174">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="3dafd-175">Взаимодействие с адаптивной картой изменяет сообщение перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="3dafd-175">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="3dafd-176">После выбора пользователем `Send` бота сообщение передается в канал.</span><span class="sxs-lookup"><span data-stu-id="3dafd-176">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="3dafd-177">Реагирование на начальное действие отправки</span><span class="sxs-lookup"><span data-stu-id="3dafd-177">Respond to initial submit action</span></span>

<span data-ttu-id="3dafd-178">Чтобы включить этот поток, модуль задач должен ответить на начальное сообщение предварительным просмотром карты, которую бот `composeExtension/submitAction` отправляет каналу.</span><span class="sxs-lookup"><span data-stu-id="3dafd-178">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="3dafd-179">Это дает пользователю возможность проверить карту перед отправкой, а также попытаться установить бот в беседе, если она еще не установлена.</span><span class="sxs-lookup"><span data-stu-id="3dafd-179">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3dafd-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3dafd-180">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="3dafd-181">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="3dafd-181">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="3dafd-182">JSON</span><span class="sxs-lookup"><span data-stu-id="3dafd-182">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="3dafd-183">Должен содержать действие с 1 адаптивным `activityPreview` вложением `message` карт.</span><span class="sxs-lookup"><span data-stu-id="3dafd-183">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="3dafd-184">Значение `<< Card Payload >>` является местообнамерщиком для карточки, вы хотите отправить.</span><span class="sxs-lookup"><span data-stu-id="3dafd-184">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="3dafd-185">BotMessagePreview отправляет и редактирует события</span><span class="sxs-lookup"><span data-stu-id="3dafd-185">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="3dafd-186">Расширение сообщения должно реагировать сейчас на два новых варианта `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"` и `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="3dafd-186">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3dafd-187">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3dafd-187">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="3dafd-188">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="3dafd-188">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="3dafd-189">JSON</span><span class="sxs-lookup"><span data-stu-id="3dafd-189">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="3dafd-190">Ответ на изменение botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="3dafd-190">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="3dafd-191">Если пользователь перед отправкой редактирует карту, выбрав кнопку **Изменить,** вы получите вызов `composeExtension/submitAction` с помощью `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="3dafd-191">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="3dafd-192">Обычно следует отвечать, возвращая отправленный модуль задач в ответ на начальный вызов, `composeExtension/fetchTask` который начал взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="3dafd-192">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="3dafd-193">Это позволяет пользователю начать процесс с повторного ввода исходной информации.</span><span class="sxs-lookup"><span data-stu-id="3dafd-193">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="3dafd-194">Используйте доступную информацию для предварительного заполнения модуля задач, чтобы пользователю не нужно было заполнять всю информацию с нуля.</span><span class="sxs-lookup"><span data-stu-id="3dafd-194">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="3dafd-195">См. [ответы на начальное `fetchTask` событие](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="3dafd-195">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="3dafd-196">Ответ на отправку botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="3dafd-196">Respond to botMessagePreview send</span></span>

<span data-ttu-id="3dafd-197">После того как пользователь выберет кнопку **Отправка,** вы получите вызов `composeExtension/submitAction` с `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="3dafd-197">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="3dafd-198">Веб-служба должна создать и отправить на беседу проактивное сообщение с адаптивной картой, а также ответить на вызов.</span><span class="sxs-lookup"><span data-stu-id="3dafd-198">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3dafd-199">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3dafd-199">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="3dafd-200">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="3dafd-200">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="3dafd-201">JSON</span><span class="sxs-lookup"><span data-stu-id="3dafd-201">JSON</span></span>](#tab/json)

<span data-ttu-id="3dafd-202">Вы получаете новое `composeExtension/submitAction` сообщение, аналогичное следующему:</span><span class="sxs-lookup"><span data-stu-id="3dafd-202">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="3dafd-203">Атрибуция пользователей для сообщений ботов</span><span class="sxs-lookup"><span data-stu-id="3dafd-203">User attribution for bots messages</span></span> 

<span data-ttu-id="3dafd-204">В сценариях, когда бот отправляет сообщения от имени пользователя, приписывая сообщение этому пользователю, можно помочь с вовлечением и продемонстрировать более естественный поток взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="3dafd-204">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="3dafd-205">Эта функция позволяет приписать сообщение от бота пользователю, от имени которого оно было отправлено.</span><span class="sxs-lookup"><span data-stu-id="3dafd-205">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="3dafd-206">На следующем изображении слева находится сообщение карточки, отправленное ботом без атрибуции  пользователя, а справа — карточка, отправленная ботом с атрибуцией пользователя. </span><span class="sxs-lookup"><span data-stu-id="3dafd-206">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![Снимок экрана](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="3dafd-208">Чтобы использовать атрибутику пользователя в командах, необходимо добавить объект упоминания в полезной нагрузке, которая `OnBehalfOf` `ChannelData` `Activity` отправляется в Teams.</span><span class="sxs-lookup"><span data-stu-id="3dafd-208">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="3dafd-209">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="3dafd-209">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="3dafd-210">JSON</span><span class="sxs-lookup"><span data-stu-id="3dafd-210">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="3dafd-211">Ниже приводится описание сущностями в `OnBehalfOf` массиве:</span><span class="sxs-lookup"><span data-stu-id="3dafd-211">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="3dafd-212">Сведения о  `OnBehalfOf` схеме сущности</span><span class="sxs-lookup"><span data-stu-id="3dafd-212">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="3dafd-213">Поле</span><span class="sxs-lookup"><span data-stu-id="3dafd-213">Field</span></span>|<span data-ttu-id="3dafd-214">Тип</span><span class="sxs-lookup"><span data-stu-id="3dafd-214">Type</span></span>|<span data-ttu-id="3dafd-215">Описание</span><span class="sxs-lookup"><span data-stu-id="3dafd-215">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="3dafd-216">Целое число</span><span class="sxs-lookup"><span data-stu-id="3dafd-216">Integer</span></span>|<span data-ttu-id="3dafd-217">Должно быть 0</span><span class="sxs-lookup"><span data-stu-id="3dafd-217">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="3dafd-218">Строка</span><span class="sxs-lookup"><span data-stu-id="3dafd-218">String</span></span>|<span data-ttu-id="3dafd-219">Должно быть "лицом"</span><span class="sxs-lookup"><span data-stu-id="3dafd-219">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="3dafd-220">Строка</span><span class="sxs-lookup"><span data-stu-id="3dafd-220">String</span></span>|<span data-ttu-id="3dafd-221">Идентификатор ресурса сообщений (MRI) человека, от имени которого отправляется сообщение.</span><span class="sxs-lookup"><span data-stu-id="3dafd-221">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="3dafd-222">Имя отправитель сообщения будет отображаться как \<user\> \<bot name\> "через".</span><span class="sxs-lookup"><span data-stu-id="3dafd-222">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="3dafd-223">Строка</span><span class="sxs-lookup"><span data-stu-id="3dafd-223">String</span></span>|<span data-ttu-id="3dafd-224">Имя человека.</span><span class="sxs-lookup"><span data-stu-id="3dafd-224">Name of the person.</span></span> <span data-ttu-id="3dafd-225">Используется в качестве отката в разрешении имени случая недоступно.</span><span class="sxs-lookup"><span data-stu-id="3dafd-225">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="3dafd-226">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3dafd-226">Next Steps</span></span>

<span data-ttu-id="3dafd-227">Добавление команды поиска</span><span class="sxs-lookup"><span data-stu-id="3dafd-227">Add a search command</span></span>

* [<span data-ttu-id="3dafd-228">Определить команды поиска</span><span class="sxs-lookup"><span data-stu-id="3dafd-228">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
