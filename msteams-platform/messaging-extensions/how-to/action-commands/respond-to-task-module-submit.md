---
title: Ответ на действие отправки модуля задач
author: clearab
description: Описывает, как реагировать на отправку действия модуля задач из команды действий расширения обмена сообщениями.
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3ed682eadde410a545f73768943a51ef95123e49
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019834"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="0d437-103">Ответ на действие отправки модуля задач</span><span class="sxs-lookup"><span data-stu-id="0d437-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="0d437-104">В этом документе вы можете узнать, как ваше приложение реагирует на команды действий, например на отправку действия модуля задач пользователя.</span><span class="sxs-lookup"><span data-stu-id="0d437-104">This document guides you on how your app responds to the action commands, such as user's task module submit action.</span></span>
<span data-ttu-id="0d437-105">После отправки модуля задач веб-служба получает сообщение вызова с командным `composeExtension/submitAction` ИД и значениями параметров.</span><span class="sxs-lookup"><span data-stu-id="0d437-105">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="0d437-106">У приложения есть пять секунд для ответа на вызов, в противном случае пользователь получает сообщение об ошибке, которое не может достичь **приложения,** и любой ответ на вызов игнорируется Teams клиентом.</span><span class="sxs-lookup"><span data-stu-id="0d437-106">Your app has five seconds to respond to the invoke, otherwise the user receives an error message **Unable to reach the app**, and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="0d437-107">У вас есть следующие варианты ответа:</span><span class="sxs-lookup"><span data-stu-id="0d437-107">You have the following options to respond:</span></span>

* <span data-ttu-id="0d437-108">Нет ответа. Используйте действие отправки, чтобы вызвать процесс во внешней системе и не предоставлять пользователю никаких отзывов.</span><span class="sxs-lookup"><span data-stu-id="0d437-108">No response: Use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="0d437-109">Это полезно для длительных процессов, и вы можете выбрать, чтобы предоставить обратную связь поочередно.</span><span class="sxs-lookup"><span data-stu-id="0d437-109">This is useful for long-running processes, and you can select to provide feedback alternately.</span></span> <span data-ttu-id="0d437-110">Например, вы можете дать обратную связь с помощью [активного сообщения.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="0d437-110">For example, you can give feedback with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="0d437-111">[Другой модуль задач.](#respond-with-another-task-module)Вы можете отвечать дополнительным модулем задач в рамках многоэтапного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="0d437-111">[Another task module](#respond-with-another-task-module): You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="0d437-112">[Ответ на карточку.](#respond-with-a-card-inserted-into-the-compose-message-area)Вы можете отвечать карточкой, с помощью которую пользователь может взаимодействовать или вставлять в сообщение.</span><span class="sxs-lookup"><span data-stu-id="0d437-112">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area): You can respond with a card that the user can interact with or insert into a message.</span></span>
* <span data-ttu-id="0d437-113">[Адаптивная карта из бота.](#bot-response-with-adaptive-card)Вставьте адаптивную карточку непосредственно в беседу.</span><span class="sxs-lookup"><span data-stu-id="0d437-113">[Adaptive Card from bot](#bot-response-with-adaptive-card): Insert an Adaptive Card directly into the conversation.</span></span>
* <span data-ttu-id="0d437-114">[Запрос пользователя на проверку подлинности.](~/messaging-extensions/how-to/add-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0d437-114">[Request the user to authenticate](~/messaging-extensions/how-to/add-authentication.md).</span></span>
* <span data-ttu-id="0d437-115">[Запрос пользователя для предоставления дополнительной конфигурации.](~/messaging-extensions/how-to/add-configuration-page.md)</span><span class="sxs-lookup"><span data-stu-id="0d437-115">[Request the user to provide additional configuration](~/messaging-extensions/how-to/add-configuration-page.md).</span></span>

<span data-ttu-id="0d437-116">Для проверки подлинности или настройки после завершения процесса пользователь вызывает повторное вызов в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="0d437-116">For authentication or configuration, after the user completes the process, the original invoke is resent to your web service.</span></span> <span data-ttu-id="0d437-117">В следующей таблице показано, какие типы ответов доступны в зависимости от расположения ссылок расширения `commandContext` обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="0d437-117">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="0d437-118">Тип ответа</span><span class="sxs-lookup"><span data-stu-id="0d437-118">Response Type</span></span> | <span data-ttu-id="0d437-119">Создание</span><span class="sxs-lookup"><span data-stu-id="0d437-119">Compose</span></span> | <span data-ttu-id="0d437-120">Командная планка</span><span class="sxs-lookup"><span data-stu-id="0d437-120">Command bar</span></span> | <span data-ttu-id="0d437-121">Сообщение</span><span class="sxs-lookup"><span data-stu-id="0d437-121">Message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="0d437-122">Ответ на карточку</span><span class="sxs-lookup"><span data-stu-id="0d437-122">Card response</span></span> | <span data-ttu-id="0d437-123">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-123">✔</span></span> | <span data-ttu-id="0d437-124">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-124">✔</span></span> | <span data-ttu-id="0d437-125">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-125">✔</span></span> |
|<span data-ttu-id="0d437-126">Другой модуль задач</span><span class="sxs-lookup"><span data-stu-id="0d437-126">Another task module</span></span> | <span data-ttu-id="0d437-127">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-127">✔</span></span> | <span data-ttu-id="0d437-128">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-128">✔</span></span> | <span data-ttu-id="0d437-129">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-129">✔</span></span> |
|<span data-ttu-id="0d437-130">Бот с адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="0d437-130">Bot with Adaptive Card</span></span> | <span data-ttu-id="0d437-131">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-131">✔</span></span> | <span data-ttu-id="0d437-132">x</span><span class="sxs-lookup"><span data-stu-id="0d437-132">x</span></span> | <span data-ttu-id="0d437-133">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-133">✔</span></span> |
| <span data-ttu-id="0d437-134">Нет ответа</span><span class="sxs-lookup"><span data-stu-id="0d437-134">No response</span></span> | <span data-ttu-id="0d437-135">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-135">✔</span></span> | <span data-ttu-id="0d437-136">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-136">✔</span></span> | <span data-ttu-id="0d437-137">✔</span><span class="sxs-lookup"><span data-stu-id="0d437-137">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="0d437-138">Когда вы выбираете **Action.Submit** через карточки ME, он отправляет действие вызова с именем **composeExtension,** где значение равно обычной полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="0d437-138">When you select **Action.Submit** through ME cards, it sends invoke activity with the name **composeExtension**, where the value is equal to the usual payload.</span></span>
> * <span data-ttu-id="0d437-139">При выборе **Action.Submit** с помощью беседы вы получаете действие сообщения с именем **onCardButtonClicked,** где значение равно обычной полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="0d437-139">When you select **Action.Submit** through conversation, you receive message activity with the name **onCardButtonClicked**, where the value is equal to the usual payload.</span></span>

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="0d437-140">Событие вызовов submitAction</span><span class="sxs-lookup"><span data-stu-id="0d437-140">The submitAction invoke event</span></span>

<span data-ttu-id="0d437-141">Примеры получения сообщения вызова приводятся следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0d437-141">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0d437-142">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0d437-142">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0d437-143">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0d437-143">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="0d437-144">JSON</span><span class="sxs-lookup"><span data-stu-id="0d437-144">JSON</span></span>](#tab/json)

<span data-ttu-id="0d437-145">Это пример получаемого объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="0d437-145">This is an example of the JSON object that you receive.</span></span> <span data-ttu-id="0d437-146">Параметр `commandContext` указывает, откуда было вызвано расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="0d437-146">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="0d437-147">Объект содержит поля формы в качестве `data` параметров и значения, которые пользователь представил.</span><span class="sxs-lookup"><span data-stu-id="0d437-147">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="0d437-148">Объект JSON здесь сокращен, чтобы выделить наиболее релевантные поля.</span><span class="sxs-lookup"><span data-stu-id="0d437-148">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="0d437-149">Ответьте карточкой, вставленной в область составить сообщение</span><span class="sxs-lookup"><span data-stu-id="0d437-149">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="0d437-150">Наиболее распространенный способ ответа на запрос — это карта, вставленная в область `composeExtension/submitAction` составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="0d437-150">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="0d437-151">Пользователь передает карточку в беседу.</span><span class="sxs-lookup"><span data-stu-id="0d437-151">The user submits the card to the conversation.</span></span> <span data-ttu-id="0d437-152">Дополнительные сведения об использовании карт см. в [карточках и действиях карт.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="0d437-152">For more information on using cards, see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0d437-153">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0d437-153">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0d437-154">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0d437-154">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="0d437-155">JSON</span><span class="sxs-lookup"><span data-stu-id="0d437-155">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="0d437-156">Ответ с помощью другого модуля задач</span><span class="sxs-lookup"><span data-stu-id="0d437-156">Respond with another task module</span></span>

<span data-ttu-id="0d437-157">Вы можете выбрать, чтобы ответить на `submitAction` событие с помощью дополнительного модуля задач.</span><span class="sxs-lookup"><span data-stu-id="0d437-157">You can select to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="0d437-158">Это полезно, когда:</span><span class="sxs-lookup"><span data-stu-id="0d437-158">This is useful when:</span></span>

* <span data-ttu-id="0d437-159">Необходимо собирать большие объемы информации.</span><span class="sxs-lookup"><span data-stu-id="0d437-159">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="0d437-160">Необходимо динамически изменить собираемую информацию на основе ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="0d437-160">You need to dynamically change the information you are collecting based on user input.</span></span>
* <span data-ttu-id="0d437-161">Необходимо проверить сведения, представленные пользователем, и повторно отправить форму с сообщением об ошибке, если что-то не так.</span><span class="sxs-lookup"><span data-stu-id="0d437-161">You need to validate the information submitted by the user and resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="0d437-162">Метод ответа такой же, как [и ответ на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="0d437-162">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="0d437-163">Если вы используете SDK Bot Framework, для отправки действий запускается одно и то же событие.</span><span class="sxs-lookup"><span data-stu-id="0d437-163">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="0d437-164">Чтобы сделать эту работу, необходимо добавить логику, которая определяет правильный ответ.</span><span class="sxs-lookup"><span data-stu-id="0d437-164">To make this work, you must add logic that determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="0d437-165">Ответ бота с адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="0d437-165">Bot response with Adaptive Card</span></span>

> [!NOTE]
> <span data-ttu-id="0d437-166">Обязательным условием получения ответа бота с адаптивной картой является то, что необходимо добавить объект в манифест приложения и определить требуемую область `bot` для бота.</span><span class="sxs-lookup"><span data-stu-id="0d437-166">The prerequisite to get the bot response with an Adaptive card is that you must add the `bot` object to your app manifest, and define the required scope for the bot.</span></span> <span data-ttu-id="0d437-167">Используйте тот же ID, что и расширение обмена сообщениями для бота.</span><span class="sxs-lookup"><span data-stu-id="0d437-167">Use the same ID as your messaging extension for your bot.</span></span>
 
<span data-ttu-id="0d437-168">Вы также можете ответить на сообщение, вставив сообщение с адаптивной картой `submitAction` в канал с помощью бота.</span><span class="sxs-lookup"><span data-stu-id="0d437-168">You can also respond to the `submitAction` by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="0d437-169">Пользователь может предварительно просмотреть сообщение перед его отправкой.</span><span class="sxs-lookup"><span data-stu-id="0d437-169">The user can preview the message before submitting it.</span></span> <span data-ttu-id="0d437-170">Это очень полезно в сценариях, в которых вы собираете информацию от пользователей перед созданием ответа адаптивной карты или при обновлении карты после ее взаимодействия с ней.</span><span class="sxs-lookup"><span data-stu-id="0d437-170">This is very useful in scenarios where you gather information from the users before creating an Adaptive Card response, or when you update the card after someone interacts with it.</span></span> 

<span data-ttu-id="0d437-171">В следующем сценарии показано, как приложение Polly настраивает опрос, не включая этапы настройки в диалог канала:</span><span class="sxs-lookup"><span data-stu-id="0d437-171">The following scenario shows how the app Polly configures a poll without including the configuration steps in the channel conversation:</span></span>

<span data-ttu-id="0d437-172">**Настройка опроса**</span><span class="sxs-lookup"><span data-stu-id="0d437-172">**To configure the poll**</span></span>

1. <span data-ttu-id="0d437-173">Пользователь выбирает расширение обмена сообщениями для вызова модуля задач.</span><span class="sxs-lookup"><span data-stu-id="0d437-173">The user selects the messaging extension to invoke the task module.</span></span>
1. <span data-ttu-id="0d437-174">Пользователь настраивает опрос с помощью модуля задач.</span><span class="sxs-lookup"><span data-stu-id="0d437-174">The user configures the poll with the task module.</span></span>
1. <span data-ttu-id="0d437-175">После отправки модуля задач приложение использует сведения, предоставленные для создания опроса в качестве адаптивной карты, и отправляет его в качестве ответа `botMessagePreview` клиенту.</span><span class="sxs-lookup"><span data-stu-id="0d437-175">After submitting the task module, the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
1. <span data-ttu-id="0d437-176">Затем пользователь может просмотреть сообщение адаптивной карты, прежде чем бот вставляет его в канал.</span><span class="sxs-lookup"><span data-stu-id="0d437-176">The user can then preview the Adaptive Card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="0d437-177">Если приложение еще не является участником канала, выберите `Send` добавить его.</span><span class="sxs-lookup"><span data-stu-id="0d437-177">If the app is not already a member of the channel, select `Send` to add it.</span></span>

    > [!NOTE] 
    > * <span data-ttu-id="0d437-178">Пользователи также могут выбрать `Edit` сообщение, которое возвращает их в исходный модуль задач.</span><span class="sxs-lookup"><span data-stu-id="0d437-178">The users can also select to `Edit` the message, which returns them to the original task module.</span></span> 
    > * <span data-ttu-id="0d437-179">Взаимодействие с адаптивной картой изменяет сообщение перед отправкой.</span><span class="sxs-lookup"><span data-stu-id="0d437-179">Interaction with the Adaptive Card changes the message before sending it.</span></span>
1. <span data-ttu-id="0d437-180">После выбора пользователем `Send` бота сообщение передается в канал.</span><span class="sxs-lookup"><span data-stu-id="0d437-180">After the user selects `Send` the bot posts the message to the channel.</span></span>

## <a name="respond-to-initial-submit-action"></a><span data-ttu-id="0d437-181">Реагирование на начальное действие отправки</span><span class="sxs-lookup"><span data-stu-id="0d437-181">Respond to initial submit action</span></span>

<span data-ttu-id="0d437-182">Модуль задач должен отвечать на начальное сообщение предварительным просмотром карты, которую отправляет бот `composeExtension/submitAction` каналу.</span><span class="sxs-lookup"><span data-stu-id="0d437-182">Your task module must respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot sends to the channel.</span></span> <span data-ttu-id="0d437-183">Пользователь может проверить карту перед отправкой, а также попытаться установить бот в беседе, если бот еще не установлен.</span><span class="sxs-lookup"><span data-stu-id="0d437-183">The user can verify the card before sending, and also try to install your bot in the conversation if the bot is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0d437-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0d437-184">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0d437-185">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0d437-185">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="0d437-186">JSON</span><span class="sxs-lookup"><span data-stu-id="0d437-186">JSON</span></span>](#tab/json)

> [!NOTE]
> * <span data-ttu-id="0d437-187">Необходимо содержать действие с одним вложением `activityPreview` `message` адаптивной карты.</span><span class="sxs-lookup"><span data-stu-id="0d437-187">The `activityPreview` must contain a `message` activity with exactly one Adaptive Card attachment.</span></span> <span data-ttu-id="0d437-188">Значение `<< Card Payload >>` — это местоодатель для карточки, которая будет отправляться.</span><span class="sxs-lookup"><span data-stu-id="0d437-188">The `<< Card Payload >>` value is a placeholder for the card you want to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="0d437-189">BotMessagePreview отправляет и редактирует события</span><span class="sxs-lookup"><span data-stu-id="0d437-189">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="0d437-190">Расширение обмена сообщениями должно отвечать на два новых типа `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"` и `value.botMessagePreviewAction = "edit"` .</span><span class="sxs-lookup"><span data-stu-id="0d437-190">Your messaging extension must respond to two new types of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0d437-191">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0d437-191">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0d437-192">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0d437-192">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="0d437-193">JSON</span><span class="sxs-lookup"><span data-stu-id="0d437-193">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="0d437-194">Ответ на изменение botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="0d437-194">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="0d437-195">Если пользователь перед отправкой редактирует карту, выбрав **изменение,** вы получите вызов `composeExtension/submitAction` с помощью `value.botMessagePreviewAction = edit` .</span><span class="sxs-lookup"><span data-stu-id="0d437-195">If the user edits the card before sending, by selecting **Edit**, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="0d437-196">Вы должны ответить, возвращая отправленный модуль задач в ответ на начальный вызов, `composeExtension/fetchTask` который начал взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="0d437-196">You must respond by returning the task module you sent, in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="0d437-197">Это позволяет пользователю начать процесс повторного ввода исходной информации.</span><span class="sxs-lookup"><span data-stu-id="0d437-197">This allows the user to start the process by re-entering the original information.</span></span> <span data-ttu-id="0d437-198">Используйте доступные сведения для обновления модуля задач, чтобы пользователю не было необходимости заполнять всю информацию с нуля.</span><span class="sxs-lookup"><span data-stu-id="0d437-198">Use the available information to update the task module so that the user need not fill out all information from scratch.</span></span>
<span data-ttu-id="0d437-199">Дополнительные сведения об ответе на начальное событие см. в `fetchTask` [ответе на начальное `fetchTask` событие.](~/messaging-extensions/how-to/action-commands/create-task-module.md)</span><span class="sxs-lookup"><span data-stu-id="0d437-199">For more information on responding to the initial `fetchTask` event, see [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="0d437-200">Ответ на отправку botMessagePreview</span><span class="sxs-lookup"><span data-stu-id="0d437-200">Respond to botMessagePreview send</span></span>

<span data-ttu-id="0d437-201">После того как пользователь выбирает **отправку,** вы получите вызов `composeExtension/submitAction` с `value.botMessagePreviewAction = send` .</span><span class="sxs-lookup"><span data-stu-id="0d437-201">After the user selects the **Send**, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="0d437-202">Веб-служба должна создать и отправить на беседу проактивное сообщение с адаптивной картой, а также ответить на вызов.</span><span class="sxs-lookup"><span data-stu-id="0d437-202">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0d437-203">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0d437-203">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="0d437-204">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="0d437-204">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="0d437-205">JSON</span><span class="sxs-lookup"><span data-stu-id="0d437-205">JSON</span></span>](#tab/json)

<span data-ttu-id="0d437-206">Вы получаете новое `composeExtension/submitAction` сообщение, аналогичное следующему:</span><span class="sxs-lookup"><span data-stu-id="0d437-206">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="0d437-207">Атрибуция пользователей для сообщений ботов</span><span class="sxs-lookup"><span data-stu-id="0d437-207">User attribution for bots messages</span></span> 

<span data-ttu-id="0d437-208">В сценариях, когда бот отправляет сообщения от имени пользователя, приписка сообщения этому пользователю помогает с вовлечением и демонстрирует более естественный поток взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="0d437-208">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user helps with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="0d437-209">Эта функция позволяет приписать сообщение от бота пользователю, от имени которого оно было отправлено.</span><span class="sxs-lookup"><span data-stu-id="0d437-209">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="0d437-210">На следующем изображении слева находится сообщение карточки, отправленное ботом без атрибуции пользователя, а справа — карточка, отправленная ботом с атрибуцией пользователя.</span><span class="sxs-lookup"><span data-stu-id="0d437-210">In the following image, on the left is a card message sent by a bot without user attribution and on the right is a card sent by a bot with user attribution.</span></span>

![Боты атрибуции пользователей](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="0d437-212">Чтобы использовать атрибутику пользователя в командах, необходимо добавить объект упоминания в полезной нагрузке, которая отправляется в `OnBehalfOf` `ChannelData` `Activity` Teams.</span><span class="sxs-lookup"><span data-stu-id="0d437-212">To use the user attribution in teams, you must add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="0d437-213">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="0d437-213">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="0d437-214">JSON</span><span class="sxs-lookup"><span data-stu-id="0d437-214">JSON</span></span>](#tab/json-1)

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

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="0d437-215">Сведения о  `OnBehalfOf` схеме сущности</span><span class="sxs-lookup"><span data-stu-id="0d437-215">Details of  `OnBehalfOf` entity schema</span></span>

<span data-ttu-id="0d437-216">В следующем разделе описаны сущностями в `OnBehalfOf` массиве:</span><span class="sxs-lookup"><span data-stu-id="0d437-216">The following section is a description of the entities in the `OnBehalfOf` Array:</span></span>

|<span data-ttu-id="0d437-217">Поле</span><span class="sxs-lookup"><span data-stu-id="0d437-217">Field</span></span>|<span data-ttu-id="0d437-218">Тип</span><span class="sxs-lookup"><span data-stu-id="0d437-218">Type</span></span>|<span data-ttu-id="0d437-219">Описание</span><span class="sxs-lookup"><span data-stu-id="0d437-219">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="0d437-220">Целое число</span><span class="sxs-lookup"><span data-stu-id="0d437-220">Integer</span></span>|<span data-ttu-id="0d437-221">Описывает идентификацию элемента.</span><span class="sxs-lookup"><span data-stu-id="0d437-221">Describes identification of the item.</span></span> <span data-ttu-id="0d437-222">Его значение должно быть `0` .</span><span class="sxs-lookup"><span data-stu-id="0d437-222">Its value must be `0`.</span></span>|
|`mentionType`|<span data-ttu-id="0d437-223">String</span><span class="sxs-lookup"><span data-stu-id="0d437-223">String</span></span>|<span data-ttu-id="0d437-224">Описывает упоминание о "человеке".</span><span class="sxs-lookup"><span data-stu-id="0d437-224">Describes the mention of a "person".</span></span>|
|`mri`|<span data-ttu-id="0d437-225">String</span><span class="sxs-lookup"><span data-stu-id="0d437-225">String</span></span>|<span data-ttu-id="0d437-226">Идентификатор ресурса сообщений (MRI) человека, от имени которого отправляется сообщение.</span><span class="sxs-lookup"><span data-stu-id="0d437-226">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="0d437-227">Имя отправитель сообщения будет отображаться как \<user\> \<bot name\> "через".</span><span class="sxs-lookup"><span data-stu-id="0d437-227">Message sender name would appear as "\<user\> through \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="0d437-228">String</span><span class="sxs-lookup"><span data-stu-id="0d437-228">String</span></span>|<span data-ttu-id="0d437-229">Имя человека.</span><span class="sxs-lookup"><span data-stu-id="0d437-229">Name of the person.</span></span> <span data-ttu-id="0d437-230">Используется в качестве отката в разрешении имени случая недоступно.</span><span class="sxs-lookup"><span data-stu-id="0d437-230">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="code-sample"></a><span data-ttu-id="0d437-231">Пример кода</span><span class="sxs-lookup"><span data-stu-id="0d437-231">Code sample</span></span>

| <span data-ttu-id="0d437-232">Имя образца</span><span class="sxs-lookup"><span data-stu-id="0d437-232">Sample Name</span></span>           | <span data-ttu-id="0d437-233">Описание</span><span class="sxs-lookup"><span data-stu-id="0d437-233">Description</span></span> | <span data-ttu-id="0d437-234">.NET</span><span class="sxs-lookup"><span data-stu-id="0d437-234">.NET</span></span>    | <span data-ttu-id="0d437-235">Node.js</span><span class="sxs-lookup"><span data-stu-id="0d437-235">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="0d437-236">Teams расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0d437-236">Teams messaging extension action</span></span>| <span data-ttu-id="0d437-237">Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач.</span><span class="sxs-lookup"><span data-stu-id="0d437-237">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="0d437-238">View</span><span class="sxs-lookup"><span data-stu-id="0d437-238">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="0d437-239">View</span><span class="sxs-lookup"><span data-stu-id="0d437-239">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="0d437-240">Teams расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="0d437-240">Teams messaging extension search</span></span>   |  <span data-ttu-id="0d437-241">Описывает, как определить команды поиска и реагировать на поиски.</span><span class="sxs-lookup"><span data-stu-id="0d437-241">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="0d437-242">View</span><span class="sxs-lookup"><span data-stu-id="0d437-242">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="0d437-243">View</span><span class="sxs-lookup"><span data-stu-id="0d437-243">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="0d437-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d437-244">Next Step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d437-245">Определить команды поиска</span><span class="sxs-lookup"><span data-stu-id="0d437-245">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

