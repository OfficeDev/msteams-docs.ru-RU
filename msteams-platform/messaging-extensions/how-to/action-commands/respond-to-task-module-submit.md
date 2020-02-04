---
title: Ответ на действие отправить модуль задач
author: clearab
description: В этой статье описывается, как реагировать на действия по отправке модуля задач из команды действия расширения системы обмена сообщениями
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 33a9388ee84dcf03a5bda59c5a5139c6f49bde6c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675482"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="5594d-103">Ответ на действие отправить модуль задач</span><span class="sxs-lookup"><span data-stu-id="5594d-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="5594d-104">После того как пользователь отправит модуль задач, веб-служба получит сообщение `composeExtension/submitAction` Invoke с идентификатором команды и значением параметра.</span><span class="sxs-lookup"><span data-stu-id="5594d-104">Once a user submits the task module, your web service will receive a `composeExtension/submitAction` invoke message with the command id and parameter values set.</span></span> <span data-ttu-id="5594d-105">В течение пяти секунд приложение будет отвечать на вызов, в противном случае пользователь получит сообщение об ошибке "не удается получить доступ к приложению", а любой ответ на вызов будет игнорироваться клиентом Teams.</span><span class="sxs-lookup"><span data-stu-id="5594d-105">Your app will have five seconds to respond to the invoke, otherwise the user will receive an "Unable to reach the app" error message, and any reply to the invoke will be ignored by the Teams client.</span></span>

<span data-ttu-id="5594d-106">Вы можете отвечать следующим параметрам.</span><span class="sxs-lookup"><span data-stu-id="5594d-106">You have the following options for responding.</span></span>

* <span data-ttu-id="5594d-107">Нет ответа — вы можете использовать действие Отправить для запуска процесса во внешней системе и не предоставлять пользователю никаких отзывов.</span><span class="sxs-lookup"><span data-stu-id="5594d-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="5594d-108">Это может быть удобно для длительных процессов, и вы можете оставить отзыв другим способом (например, с помощью [упреждающего сообщения](~/bots/how-to/conversations/send-proactive-messages.md)).</span><span class="sxs-lookup"><span data-stu-id="5594d-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="5594d-109">[Другой модуль задач](#respond-with-another-task-module) — вы можете ответить на дополнительный модуль задач как часть многоэтапного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="5594d-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="5594d-110">[Ответ с картой](#respond-with-a-card-inserted-into-the-compose-message-area) — вы можете ответить на карточку, которую пользователь сможет взаимодействовать с или вставить в сообщение.</span><span class="sxs-lookup"><span data-stu-id="5594d-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="5594d-111">[Адаптивная карта из ленты](#bot-response-with-adaptive-card) вставьте адаптивную карту непосредственно в беседу.</span><span class="sxs-lookup"><span data-stu-id="5594d-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="5594d-112">Запрос проверки подлинности пользователя</span><span class="sxs-lookup"><span data-stu-id="5594d-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="5594d-113">Запрос на предоставление пользователю дополнительной настройки</span><span class="sxs-lookup"><span data-stu-id="5594d-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="5594d-114">В приведенной ниже таблице показано, какие типы ответов доступны в зависимости от расположения вызова`commandContext`() расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="5594d-114">The table below shows which types of responses are available based on the invoke location (`commandContext`) of the messaging extension.</span></span> <span data-ttu-id="5594d-115">Для проверки подлинности или конфигурации после того, как пользователь завершит выполнение, исходный вызов будет повторно отправлен в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="5594d-115">For authentication or configuration, once the user completes the flow the original invoke will be re-sent to your web service.</span></span>

|<span data-ttu-id="5594d-116">Тип ответа</span><span class="sxs-lookup"><span data-stu-id="5594d-116">Response Type</span></span> | <span data-ttu-id="5594d-117">графический</span><span class="sxs-lookup"><span data-stu-id="5594d-117">compose</span></span> | <span data-ttu-id="5594d-118">панель команд</span><span class="sxs-lookup"><span data-stu-id="5594d-118">command bar</span></span> | <span data-ttu-id="5594d-119">message</span><span class="sxs-lookup"><span data-stu-id="5594d-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="5594d-120">Ответ с картой</span><span class="sxs-lookup"><span data-stu-id="5594d-120">Card response</span></span> | <span data-ttu-id="5594d-121">x</span><span class="sxs-lookup"><span data-stu-id="5594d-121">x</span></span> | <span data-ttu-id="5594d-122">x</span><span class="sxs-lookup"><span data-stu-id="5594d-122">x</span></span> | <span data-ttu-id="5594d-123">x</span><span class="sxs-lookup"><span data-stu-id="5594d-123">x</span></span> |
|<span data-ttu-id="5594d-124">Другой модуль задач</span><span class="sxs-lookup"><span data-stu-id="5594d-124">Another task module</span></span> | <span data-ttu-id="5594d-125">x</span><span class="sxs-lookup"><span data-stu-id="5594d-125">x</span></span> | <span data-ttu-id="5594d-126">x</span><span class="sxs-lookup"><span data-stu-id="5594d-126">x</span></span> | <span data-ttu-id="5594d-127">x</span><span class="sxs-lookup"><span data-stu-id="5594d-127">x</span></span> |
|<span data-ttu-id="5594d-128">Bot с адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="5594d-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="5594d-129">x</span><span class="sxs-lookup"><span data-stu-id="5594d-129">x</span></span> |  | <span data-ttu-id="5594d-130">x</span><span class="sxs-lookup"><span data-stu-id="5594d-130">x</span></span> |
| <span data-ttu-id="5594d-131">Нет ответа</span><span class="sxs-lookup"><span data-stu-id="5594d-131">No response</span></span> | <span data-ttu-id="5594d-132">x</span><span class="sxs-lookup"><span data-stu-id="5594d-132">x</span></span> | <span data-ttu-id="5594d-133">x</span><span class="sxs-lookup"><span data-stu-id="5594d-133">x</span></span> | <span data-ttu-id="5594d-134">x</span><span class="sxs-lookup"><span data-stu-id="5594d-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="5594d-135">Событие Invoke Субмитактион</span><span class="sxs-lookup"><span data-stu-id="5594d-135">The submitAction invoke event</span></span>

<span data-ttu-id="5594d-136">Ниже приводятся примеры получения сообщения вызова.</span><span class="sxs-lookup"><span data-stu-id="5594d-136">Below are examples of receiving the invoke message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="5594d-137">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="5594d-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="5594d-138">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="5594d-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="5594d-139">JSON</span><span class="sxs-lookup"><span data-stu-id="5594d-139">JSON</span></span>](#tab/json)

<span data-ttu-id="5594d-140">Пример объекта JSON, который вы получите.</span><span class="sxs-lookup"><span data-stu-id="5594d-140">This is an example of the JSON object you will receive.</span></span> <span data-ttu-id="5594d-141">`commandContext` Параметр указывает, откуда было инициировано расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="5594d-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="5594d-142">`data` Объект содержит поля формы в качестве параметров и значения, которые пользователь отправил.</span><span class="sxs-lookup"><span data-stu-id="5594d-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="5594d-143">Объект JSON в этом разделе сокращается, чтобы выделить наиболее релевантные поля.</span><span class="sxs-lookup"><span data-stu-id="5594d-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="5594d-144">Ответ с картой, вставленной в область "Создание сообщения"</span><span class="sxs-lookup"><span data-stu-id="5594d-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="5594d-145">Наиболее распространенным способом ответа на `composeExtension/submitAction` запрос является карта, вставленная в область сообщения создать.</span><span class="sxs-lookup"><span data-stu-id="5594d-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="5594d-146">Затем пользователь может послать карточку в беседу.</span><span class="sxs-lookup"><span data-stu-id="5594d-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="5594d-147">Дополнительные сведения об использовании [карт см.](~/task-modules-and-cards/cards/cards-actions.md)</span><span class="sxs-lookup"><span data-stu-id="5594d-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="5594d-148">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="5594d-148">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="5594d-149">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="5594d-149">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="5594d-150">JSON</span><span class="sxs-lookup"><span data-stu-id="5594d-150">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="5594d-151">Ответ с другим модулем задач</span><span class="sxs-lookup"><span data-stu-id="5594d-151">Respond with another task module</span></span>

<span data-ttu-id="5594d-152">Вы можете ответить на `submitAction` событие с помощью дополнительного модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="5594d-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="5594d-153">Это может быть удобно, если:</span><span class="sxs-lookup"><span data-stu-id="5594d-153">This can be useful when:</span></span>

* <span data-ttu-id="5594d-154">Необходимо собрать большой объем информации.</span><span class="sxs-lookup"><span data-stu-id="5594d-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="5594d-155">Динамическое изменение собираемых данных на основе вводимых пользователем данных</span><span class="sxs-lookup"><span data-stu-id="5594d-155">If you need to dynamically change what information you're collecting based on user input</span></span>
* <span data-ttu-id="5594d-156">Если вам нужно проверить данные, отправленные пользователем, и потенциально отправить форму с сообщением об ошибке, если что-то не так.</span><span class="sxs-lookup"><span data-stu-id="5594d-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="5594d-157">Метод для ответа такой же, как и в ответ [на исходное `fetchTask` событие](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="5594d-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="5594d-158">Если вы используете пакет SDK для ленты, то одно и то же событие будет запущено для обоих действий.</span><span class="sxs-lookup"><span data-stu-id="5594d-158">If you're using the Bot Framework SDK the same event will trigger for both submit actions.</span></span> <span data-ttu-id="5594d-159">Это означает, что необходимо добавить логику, определяющую правильный ответ.</span><span class="sxs-lookup"><span data-stu-id="5594d-159">This mean you need to be sure to add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="5594d-160">Ответ Bot со адаптивной картой</span><span class="sxs-lookup"><span data-stu-id="5594d-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="5594d-161">Для этого процесса необходимо добавить `bot` объект в манифест приложения, и у вас есть необходимая область, определенная для Bot.</span><span class="sxs-lookup"><span data-stu-id="5594d-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="5594d-162">Используйте тот же идентификатор, что и для своего расширения обмена сообщениями для ленты.</span><span class="sxs-lookup"><span data-stu-id="5594d-162">Use the same Id as your messaging extension for your bot.</span></span>

<span data-ttu-id="5594d-163">Вы также можете ответить на действие Отправить, вставив сообщение с адаптивной картой в канал с помощью ленты.</span><span class="sxs-lookup"><span data-stu-id="5594d-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="5594d-164">Пользователь сможет просмотреть сообщение перед его отправкой и потенциально редактировать/взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="5594d-164">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="5594d-165">Это может быть очень удобно в тех случаях, когда необходимо собрать информацию от пользователей перед созданием ответа на адаптивную карту или при необходимости обновления карточки после того, как пользователь взаимодействует с ней.</span><span class="sxs-lookup"><span data-stu-id="5594d-165">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response, or when you're going to need to update the card after someone interacts with it.</span></span> <span data-ttu-id="5594d-166">В приведенном ниже сценарии показано, как приложение Полли использует этот процесс для настройки опроса без включения действий по настройке в беседе канала.</span><span class="sxs-lookup"><span data-stu-id="5594d-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation.</span></span>

1. <span data-ttu-id="5594d-167">Пользователь выбирает расширение системы обмена сообщениями для запуска модуля задачи.</span><span class="sxs-lookup"><span data-stu-id="5594d-167">The user clicks the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="5594d-168">Пользователь настраивает опрос с помощью задачи маудуле.</span><span class="sxs-lookup"><span data-stu-id="5594d-168">The user configures the poll with the task moudule.</span></span>
3. <span data-ttu-id="5594d-169">После отправки модуля задачи приложение использует сведения, предоставленные для создания опроса в качестве адаптивной карты, и отправляет его в `botMessagePreview` качестве ответа клиенту.</span><span class="sxs-lookup"><span data-stu-id="5594d-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="5594d-170">После этого пользователь может просмотреть сообщение адаптивной карточки перед вставкой ленты в канал.</span><span class="sxs-lookup"><span data-stu-id="5594d-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="5594d-171">Если приложение еще не является участником канала, его Нажатие `Send` будет добавлено.</span><span class="sxs-lookup"><span data-stu-id="5594d-171">If the app is not already a member of the channel, clicking `Send` will add the it.</span></span>
   1. <span data-ttu-id="5594d-172">Пользователь также может выбрать `Edit` сообщение, которое возвращает их в исходный модуль задач.</span><span class="sxs-lookup"><span data-stu-id="5594d-172">The user can also chose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="5594d-173">При взаимодействии с адаптивной картой изменяется сообщение перед его отправкой.</span><span class="sxs-lookup"><span data-stu-id="5594d-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="5594d-174">После того как пользователь `Send` нажмет сообщение в канале, вы отправляете его в канал.</span><span class="sxs-lookup"><span data-stu-id="5594d-174">Once the user clicks `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="5594d-175">Ответ на начальное действие по отправку</span><span class="sxs-lookup"><span data-stu-id="5594d-175">Respond to initial submit action</span></span>

<span data-ttu-id="5594d-176">Чтобы включить этот рабочий процесс, модуль задачи должен отвечать исходному `composeExtension/submitAction` сообщению с предварительным просмотром карты, отправляемой с канала в канале Bot.</span><span class="sxs-lookup"><span data-stu-id="5594d-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot will send to the channel.</span></span> <span data-ttu-id="5594d-177">Это дает пользователю возможность проверить карточку перед отправкой, а также попытаться установить Bot в беседе, если она еще не установлена.</span><span class="sxs-lookup"><span data-stu-id="5594d-177">This gives the user the opportunity to verify the card before sending, and also will attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="5594d-178">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="5594d-178">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="5594d-179">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="5594d-179">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="5594d-180">JSON</span><span class="sxs-lookup"><span data-stu-id="5594d-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="5594d-181">`activityPreview` Должен содержать `message` действие с ровно 1 вложенной картой.</span><span class="sxs-lookup"><span data-stu-id="5594d-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="5594d-182">`<< Card Payload >>` Значение — это заполнитель для карточки, которую вы хотите отправить.</span><span class="sxs-lookup"><span data-stu-id="5594d-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="5594d-183">События отправки и редактирования Ботмессажепревиев</span><span class="sxs-lookup"><span data-stu-id="5594d-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="5594d-184">Теперь ваше расширение сообщения должно реагировать на два новых вида `composeExtension/submitAction` вызова, где `value.botMessagePreviewAction = "send"`и. `value.botMessagePreviewAction = "edit"`</span><span class="sxs-lookup"><span data-stu-id="5594d-184">Your message extension will now need to respond to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="5594d-185">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="5594d-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="5594d-186">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="5594d-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="5594d-187">JSON</span><span class="sxs-lookup"><span data-stu-id="5594d-187">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="5594d-188">Отклик на редактирование Ботмессажепревиев</span><span class="sxs-lookup"><span data-stu-id="5594d-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="5594d-189">Если пользователь решил изменить карточку перед отправкой, нажав кнопку **изменить** , вы получите `composeExtension/submitAction` вызов с помощью `value.botMessagePreviewAction = edit`.</span><span class="sxs-lookup"><span data-stu-id="5594d-189">If the user decides to edit the card before sending by clicking the **Edit** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="5594d-190">Обычно необходимо ответить, выполнив возврат модуля задачи, отправленного в ответ на начальный `composeExtension/fetchTask` вызов, который начал взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="5594d-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="5594d-191">Это позволяет пользователю начать процесс, повторно вводя исходные данные.</span><span class="sxs-lookup"><span data-stu-id="5594d-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="5594d-192">Кроме того, следует рассмотреть возможность использования сведений, которые теперь доступны для предварительного заполнения модуля задач, чтобы пользователь не заполнил всю информацию с нуля.</span><span class="sxs-lookup"><span data-stu-id="5594d-192">You should also consider using the information you now have available to pre-populate the task module so the user doesn't have fill out all of the information from scratch.</span></span>

<span data-ttu-id="5594d-193">Узнайте, [как реагировать на `fetchTask` начальное событие](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span><span class="sxs-lookup"><span data-stu-id="5594d-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="5594d-194">Ответ на отправку Ботмессажепревиев</span><span class="sxs-lookup"><span data-stu-id="5594d-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="5594d-195">Когда пользователь нажимает кнопку **Отправить** , вы получите `composeExtension/submitAction` вызов с помощью `value.botMessagePreviewAction = send`команды.</span><span class="sxs-lookup"><span data-stu-id="5594d-195">Once the user clicks the **Send** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="5594d-196">Веб-службе потребуется создать и отправить упреждающее сообщение с помощью адаптивной карточки в беседу, а также ответить на вызов.</span><span class="sxs-lookup"><span data-stu-id="5594d-196">Your web service will need to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="5594d-197">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="5594d-197">C#/.NET</span></span>](#tab/dotnet)

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
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejstabjavascript"></a>[<span data-ttu-id="5594d-198">JavaScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="5594d-198">JavaScript/Node.js</span></span>](#tab/javascript)

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
      const responseActivity = { type: 'message', attachments: [adaptiveCard] };
    
      await context.sendActivity(responseActivity);
    }
}
```

# <a name="jsontabjson"></a>[<span data-ttu-id="5594d-199">JSON</span><span class="sxs-lookup"><span data-stu-id="5594d-199">JSON</span></span>](#tab/json)

<span data-ttu-id="5594d-200">Появится новое `composeExtension/submitAction` сообщение, аналогичное следующему:</span><span class="sxs-lookup"><span data-stu-id="5594d-200">You will receive a new `composeExtension/submitAction` message similar to the one below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5594d-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5594d-201">Next Steps</span></span>

<span data-ttu-id="5594d-202">Добавление команды поиска</span><span class="sxs-lookup"><span data-stu-id="5594d-202">Add a search command</span></span>

* [<span data-ttu-id="5594d-203">Определение команд поиска</span><span class="sxs-lookup"><span data-stu-id="5594d-203">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
