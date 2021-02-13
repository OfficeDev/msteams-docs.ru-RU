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
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="fbdd4-103">Реагирование на действие отправки модуля задачи</span><span class="sxs-lookup"><span data-stu-id="fbdd4-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="fbdd4-104">После отправки пользователем модуля задачи веб-служба получает сообщение об вызове со значениями ИД команды `composeExtension/submitAction` и параметров.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="fbdd4-105">У вашего приложения есть пять секунд на ответ на вызов, в противном случае пользователь получает сообщение об *ошибке,* не достигаемого приложением, а любой ответ на вызов игнорируется клиентом Teams.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message *Unable to reach the app*, and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="fbdd4-106">У вас есть следующие варианты ответа:</span><span class="sxs-lookup"><span data-stu-id="fbdd4-106">You have the following options for responding:</span></span>

* <span data-ttu-id="fbdd4-107">Нет ответа — вы можете использовать действие отправки для запуска процесса во внешней системе и не предоставлять пользователю никаких отзывов.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="fbdd4-108">Это может быть полезно для длительных процессов, и вы можете отправить отзыв другим способом (например, с помощью упреждающего [сообщения).](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="fbdd4-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="fbdd4-109">[Другой модуль задачи](#respond-with-another-task-module) — вы можете ответить дополнительным модулем задачи в рамках многоэтапного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="fbdd4-110">[Ответ карточки.](#respond-with-a-card-inserted-into-the-compose-message-area) Вы можете ответить карточкой, с помощью которую пользователь сможет взаимодействовать и/или вставлять данные в сообщение.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="fbdd4-111">[Адаптивная карточка из бота:](#bot-response-with-adaptive-card) вставка адаптивной карточки непосредственно в беседу.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="fbdd4-112">Запрос проверки подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="fbdd4-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="fbdd4-113">Запрос на предоставление пользователем дополнительной настройки</span><span class="sxs-lookup"><span data-stu-id="fbdd4-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="fbdd4-114">Для проверки подлинности или настройки после завершения пользователем потока исходный вызов перенаправляется в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="fbdd4-115">В следующей таблице показано, какие типы ответов доступны в зависимости от расположения вызова `commandContext` расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="fbdd4-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="fbdd4-116">Тип ответа</span><span class="sxs-lookup"><span data-stu-id="fbdd4-116">Response Type</span></span> | <span data-ttu-id="fbdd4-117">compose</span><span class="sxs-lookup"><span data-stu-id="fbdd4-117">compose</span></span> | <span data-ttu-id="fbdd4-118">панель команд</span><span class="sxs-lookup"><span data-stu-id="fbdd4-118">command bar</span></span> | <span data-ttu-id="fbdd4-119">message</span><span class="sxs-lookup"><span data-stu-id="fbdd4-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="fbdd4-120">Ответ карточки</span><span class="sxs-lookup"><span data-stu-id="fbdd4-120">Card response</span></span> | <span data-ttu-id="fbdd4-121">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-121">x</span></span> | <span data-ttu-id="fbdd4-122">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-122">x</span></span> | <span data-ttu-id="fbdd4-123">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-123">x</span></span> |
|<span data-ttu-id="fbdd4-124">Другой модуль задачи</span><span class="sxs-lookup"><span data-stu-id="fbdd4-124">Another task module</span></span> | <span data-ttu-id="fbdd4-125">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-125">x</span></span> | <span data-ttu-id="fbdd4-126">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-126">x</span></span> | <span data-ttu-id="fbdd4-127">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-127">x</span></span> |
|<span data-ttu-id="fbdd4-128">Бот с адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="fbdd4-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="fbdd4-129">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-129">x</span></span> |  | <span data-ttu-id="fbdd4-130">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-130">x</span></span> |
| <span data-ttu-id="fbdd4-131">Без ответа</span><span class="sxs-lookup"><span data-stu-id="fbdd4-131">No response</span></span> | <span data-ttu-id="fbdd4-132">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-132">x</span></span> | <span data-ttu-id="fbdd4-133">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-133">x</span></span> | <span data-ttu-id="fbdd4-134">x</span><span class="sxs-lookup"><span data-stu-id="fbdd4-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="fbdd4-135">Событие вызова submitAction</span><span class="sxs-lookup"><span data-stu-id="fbdd4-135">The submitAction invoke event</span></span>

<span data-ttu-id="fbdd4-136">Примеры получения сообщения вызова:</span><span class="sxs-lookup"><span data-stu-id="fbdd4-136">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="fbdd4-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="fbdd4-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="fbdd4-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="fbdd4-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="fbdd4-139">JSON</span><span class="sxs-lookup"><span data-stu-id="fbdd4-139">JSON</span></span>](#tab/json)

<span data-ttu-id="fbdd4-140">Это пример получаемого объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-140">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="fbdd4-141">Этот параметр указывает, откуда активировали расширение обмена `commandContext` сообщениями.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="fbdd4-142">Объект содержит поля формы в качестве параметров `data` и значения, отправленные пользователем.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="fbdd4-143">Здесь объект JSON сокращен, чтобы выделить наиболее релевантные поля.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="fbdd4-144">Ответ с помощью карточки, вставленной в область сообщения составить</span><span class="sxs-lookup"><span data-stu-id="fbdd4-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="fbdd4-145">Наиболее распространенный способ ответа на запрос — карточка, вставленная `composeExtension/submitAction` в область составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="fbdd4-146">Затем пользователь может отправить карточку в беседу.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="fbdd4-147">Дополнительные сведения об использовании карточек см. [в карточках и действиях карт.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="fbdd4-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="fbdd4-148">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="fbdd4-148">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="fbdd4-149">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="fbdd4-149">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="fbdd4-150">JSON</span><span class="sxs-lookup"><span data-stu-id="fbdd4-150">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="fbdd4-151">Ответ с помощью другого модуля задачи</span><span class="sxs-lookup"><span data-stu-id="fbdd4-151">Respond with another task module</span></span>

<span data-ttu-id="fbdd4-152">Вы можете ответить на событие `submitAction` с помощью дополнительного модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="fbdd4-153">Это может быть полезно, если:</span><span class="sxs-lookup"><span data-stu-id="fbdd4-153">This can be useful when:</span></span>

* <span data-ttu-id="fbdd4-154">Необходимо собирать большие объемы информации.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="fbdd4-155">Если вам нужно динамически изменить собираемую информацию на основе пользовательского ввода</span><span class="sxs-lookup"><span data-stu-id="fbdd4-155">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="fbdd4-156">Если вам нужно проверить сведения, отправленные пользователем, и, возможно, повторно отправить форму с сообщением об ошибке, если что-то не так.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="fbdd4-157">Метод ответа такой же, как и ответ [на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="fbdd4-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="fbdd4-158">Если вы используете SDK Bot Framework, одинаковые триггеры событий для обоих действий отправки.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-158">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="fbdd4-159">Это означает, что необходимо добавить логику, которая определяет правильный ответ.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-159">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="fbdd4-160">Ответ бота с помощью адаптивной карточки</span><span class="sxs-lookup"><span data-stu-id="fbdd4-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="fbdd4-161">Для этого потока необходимо добавить объект в манифест приложения и определить для бота необходимую `bot` область.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="fbdd4-162">Используйте тот же ИД, что и расширение для обмена сообщениями для бота.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-162">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="fbdd4-163">Вы также можете ответить на действие отправки, вставив сообщение с адаптивной карточкой в канал с помощью бота.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="fbdd4-164">Пользователь может просмотреть сообщение перед отправкой, а также, возможно, изменить или взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-164">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="fbdd4-165">Это может быть очень полезно в сценариях, когда вы собираете сведения от пользователей перед созданием ответа адаптивной карточки или обновляете карточку после того, как кто-то взаимодействует с ней.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-165">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="fbdd4-166">В следующем сценарии показано, как приложение Polly использует этот поток для настройки опроса без включаемых действий по настройке в беседу канала:</span><span class="sxs-lookup"><span data-stu-id="fbdd4-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="fbdd4-167">Пользователь выбирает расширение обмена сообщениями для запуска модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-167">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="fbdd4-168">Пользователь настраивает опрос с помощью модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-168">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="fbdd4-169">После отправки модуля задачи приложение использует сведения, предоставленные для создания опроса в качестве адаптивной карточки, и отправляет его клиенту в качестве `botMessagePreview` ответа.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="fbdd4-170">Затем пользователь может просмотреть сообщение адаптивной карточки, прежде чем бот вставляет его в канал.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="fbdd4-171">Если приложение еще не является участником канала, выбор добавляет `Send` его.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-171">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="fbdd4-172">Пользователь также может выбрать сообщение, которое возвращает его в `Edit` исходный модуль задачи.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-172">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="fbdd4-173">Взаимодействие с адаптивной картой изменяет сообщение перед его отправкой.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="fbdd4-174">После того как пользователь выберет `Send` бота, сообщение будет выкладывано в канал.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-174">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="fbdd4-175">Реагирование на первоначальное действие отправки</span><span class="sxs-lookup"><span data-stu-id="fbdd4-175">Respond to initial submit action</span></span>

<span data-ttu-id="fbdd4-176">Чтобы включить этот поток, модуль задачи должен ответить на исходное сообщение предварительной версией карточки, отправляемой ботом `composeExtension/submitAction` в канал.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="fbdd4-177">Это дает пользователю возможность проверить карточку перед отправкой, а также попытаться установить бота в беседе, если она еще не установлена.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-177">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="fbdd4-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="fbdd4-178">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="fbdd4-179">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="fbdd4-179">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="fbdd4-180">JSON</span><span class="sxs-lookup"><span data-stu-id="fbdd4-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="fbdd4-181">Действие `activityPreview` должно содержать только `message` 1 адаптивный вложение карточки.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="fbdd4-182">Значение `<< Card Payload >>` — это замеитель для карточки, отправляемой вами.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="fbdd4-183">События отправки и изменения botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="fbdd4-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="fbdd4-184">Расширение сообщения должно реагировать на два новых варианта `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"` и `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="fbdd4-184">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="fbdd4-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="fbdd4-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="fbdd4-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="fbdd4-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="fbdd4-187">JSON</span><span class="sxs-lookup"><span data-stu-id="fbdd4-187">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="fbdd4-188">Реагирование на редактирование botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="fbdd4-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="fbdd4-189">Если пользователь редактирует карточку перед  отправкой, нажатием кнопки "Изменить", вы получите вызов с помощью `composeExtension/submitAction` `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="fbdd4-189">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="fbdd4-190">Обычно в ответ на первоначальный вызов, который начал взаимодействие, следует возвращать модуль задачи, отправленный в ответ на `composeExtension/fetchTask` его первоначальный вызов.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="fbdd4-191">Это позволяет пользователю начать процесс повторно, повторно введите исходные сведения.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="fbdd4-192">Используйте доступные сведения для предварительного заполнения модуля задачи, чтобы пользователю не нужно было заполнять всю информацию с нуля.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-192">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="fbdd4-193">См. [ответ на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="fbdd4-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="fbdd4-194">Ответ на отправку botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="fbdd4-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="fbdd4-195">После того как  пользователь нажал кнопку "Отправить", вы получите вызов с помощью `composeExtension/submitAction` `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="fbdd4-195">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="fbdd4-196">Веб-служба должна создать и отправить в беседу упреждающие сообщения с адаптивной карточкой, а также ответить на вызов.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-196">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="fbdd4-197">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="fbdd4-197">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="fbdd4-198">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="fbdd4-198">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="fbdd4-199">JSON</span><span class="sxs-lookup"><span data-stu-id="fbdd4-199">JSON</span></span>](#tab/json)

<span data-ttu-id="fbdd4-200">Вы получаете новое `composeExtension/submitAction` сообщение, аналогичное следующему:</span><span class="sxs-lookup"><span data-stu-id="fbdd4-200">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="fbdd4-201">Атрибут пользователя для сообщений ботов</span><span class="sxs-lookup"><span data-stu-id="fbdd4-201">User attribution for bots messages</span></span> 

<span data-ttu-id="fbdd4-202">В сценариях, когда бот отправляет сообщения от имени пользователя, присвоение сообщений этому пользователю может помочь с вовлечением и продемонстрировать более естественный поток взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-202">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="fbdd4-203">Эта функция позволяет приписать сообщение от бота пользователю, от имени которого оно было отправлено.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-203">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="fbdd4-204">На следующем изображении слева находится карточка,  отправленная ботом без атрибуции пользователя,  а справа — карточка, отправленная ботом с атрибуцией пользователя.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-204">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![Снимок экрана](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="fbdd4-206">Чтобы использовать атрибут пользователя в командах, необходимо добавить объект упоминания в полезной нагрузке, `OnBehalfOf` `ChannelData` которая `Activity` отправляется в Teams.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-206">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="fbdd4-207">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="fbdd4-207">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="fbdd4-208">JSON</span><span class="sxs-lookup"><span data-stu-id="fbdd4-208">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="fbdd4-209">В следующем разделе приводится описание сущностями в `OnBehalfOf` массиве:</span><span class="sxs-lookup"><span data-stu-id="fbdd4-209">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="fbdd4-210">Сведения о  `OnBehalfOf` схеме сущности</span><span class="sxs-lookup"><span data-stu-id="fbdd4-210">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="fbdd4-211">Поле</span><span class="sxs-lookup"><span data-stu-id="fbdd4-211">Field</span></span>|<span data-ttu-id="fbdd4-212">Тип</span><span class="sxs-lookup"><span data-stu-id="fbdd4-212">Type</span></span>|<span data-ttu-id="fbdd4-213">Описание</span><span class="sxs-lookup"><span data-stu-id="fbdd4-213">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="fbdd4-214">Целое число</span><span class="sxs-lookup"><span data-stu-id="fbdd4-214">Integer</span></span>|<span data-ttu-id="fbdd4-215">Должно быть 0</span><span class="sxs-lookup"><span data-stu-id="fbdd4-215">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="fbdd4-216">String</span><span class="sxs-lookup"><span data-stu-id="fbdd4-216">String</span></span>|<span data-ttu-id="fbdd4-217">Должно быть "person"</span><span class="sxs-lookup"><span data-stu-id="fbdd4-217">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="fbdd4-218">String</span><span class="sxs-lookup"><span data-stu-id="fbdd4-218">String</span></span>|<span data-ttu-id="fbdd4-219">Идентификатор ресурса сообщения (MRI) пользователя, от имени которого отправляется сообщение.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-219">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="fbdd4-220">Имя отправитель сообщения будет отображаться как " \<user\> через \<bot name\> ".</span><span class="sxs-lookup"><span data-stu-id="fbdd4-220">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="fbdd4-221">String</span><span class="sxs-lookup"><span data-stu-id="fbdd4-221">String</span></span>|<span data-ttu-id="fbdd4-222">Имя человека.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-222">Name of the person.</span></span> <span data-ttu-id="fbdd4-223">Используется в качестве отката, если разрешение имен недоступно.</span><span class="sxs-lookup"><span data-stu-id="fbdd4-223">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="fbdd4-224">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fbdd4-224">Next Steps</span></span>

<span data-ttu-id="fbdd4-225">Добавление команды поиска</span><span class="sxs-lookup"><span data-stu-id="fbdd4-225">Add a search command</span></span>

* [<span data-ttu-id="fbdd4-226">Определить команды поиска</span><span class="sxs-lookup"><span data-stu-id="fbdd4-226">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
