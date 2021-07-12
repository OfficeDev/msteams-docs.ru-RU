---
title: Добавление действий карточек в бот
description: Описание действий карточек в Microsoft Teams и их использования в ботах
localization_priority: Normal
ms.topic: conceptual
keywords: teams действия карточек боты
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254204"
---
# <a name="card-actions"></a><span data-ttu-id="9023c-104">Действия карточек</span><span class="sxs-lookup"><span data-stu-id="9023c-104">Card actions</span></span>

<span data-ttu-id="9023c-105">Карточки, используемые ботами и расширениями для обмена сообщениями в Teams, поддерживают следующие типы действий [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards):</span><span class="sxs-lookup"><span data-stu-id="9023c-105">Cards used by bots and messaging extensions in Teams support the following activity [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) types:</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-106">Действия `CardAction` отличаются от `potentialActions` для карточек соединителей Office 365 при их использовании из соединителей.</span><span class="sxs-lookup"><span data-stu-id="9023c-106">The `CardAction` actions differ from `potentialActions` for Office 365 Connector cards when used from connectors.</span></span>

| <span data-ttu-id="9023c-107">Тип</span><span class="sxs-lookup"><span data-stu-id="9023c-107">Type</span></span> | <span data-ttu-id="9023c-108">Действие</span><span class="sxs-lookup"><span data-stu-id="9023c-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="9023c-109">Открывает URL-адрес в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9023c-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="9023c-110">Отправляет боту сообщение и полезные данные от пользователя, нажавшего кнопку или коснувшегося карточки.</span><span class="sxs-lookup"><span data-stu-id="9023c-110">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="9023c-111">Отправляет отдельное сообщение в поток чата.</span><span class="sxs-lookup"><span data-stu-id="9023c-111">Sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="9023c-112">Отправляет боту сообщение от пользователя, нажавшего кнопку или коснувшегося карточки.</span><span class="sxs-lookup"><span data-stu-id="9023c-112">Sends a message to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="9023c-113">Это сообщение от пользователя боту отображается для всех участников беседы.</span><span class="sxs-lookup"><span data-stu-id="9023c-113">This message from user to bot is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="9023c-114">Отправляет боту сообщение и полезные данные от пользователя, нажавшего кнопку или коснувшегося карточки.</span><span class="sxs-lookup"><span data-stu-id="9023c-114">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="9023c-115">Это сообщение не отображается.</span><span class="sxs-lookup"><span data-stu-id="9023c-115">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="9023c-116">Инициирует поток OAuth, позволяя ботам подключаться к защищенным службам.</span><span class="sxs-lookup"><span data-stu-id="9023c-116">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="9023c-117">Teams не поддерживает типы `CardAction`, не указанные в предыдущей таблице.</span><span class="sxs-lookup"><span data-stu-id="9023c-117">Teams does not support `CardAction` types not listed in the previous table.</span></span>
>* <span data-ttu-id="9023c-118">Teams не поддерживает свойство `potentialActions`.</span><span class="sxs-lookup"><span data-stu-id="9023c-118">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="9023c-119">Действия с карточками отличаются от [рекомендуемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в Bot Framework или службе Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="9023c-119">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework or Azure Bot Service.</span></span> <span data-ttu-id="9023c-120">Рекомендуемые действия не поддерживаются в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9023c-120">Suggested actions are not supported in Microsoft Teams.</span></span> <span data-ttu-id="9023c-121">Если вы хотите, чтобы в сообщении бота Teams появлялись кнопки, используйте карточку.</span><span class="sxs-lookup"><span data-stu-id="9023c-121">If you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="9023c-122">Если вы используете действие карточки в расширении для обмена сообщениями, эти действия не будут работать, пока карточка не будет отправлена в канал.</span><span class="sxs-lookup"><span data-stu-id="9023c-122">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="9023c-123">Действия не работают, пока карточка находится в окне составления сообщения.</span><span class="sxs-lookup"><span data-stu-id="9023c-123">The actions do not work while the card is in the compose message box.</span></span>

## <a name="action-type-openurl"></a><span data-ttu-id="9023c-124">Тип действия openUrl</span><span class="sxs-lookup"><span data-stu-id="9023c-124">Action type openUrl</span></span>

<span data-ttu-id="9023c-125">Тип действия `openUrl` указывает URL-адрес, который необходимо открыть в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9023c-125">`openUrl` action type specifies a URL to launch in the default browser.</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-126">Бот не получает уведомления о том, какая нажата кнопка.</span><span class="sxs-lookup"><span data-stu-id="9023c-126">Your bot does not receive any notice on which button was selected.</span></span>

<span data-ttu-id="9023c-127">С помощью `openUrl` вы можете создать действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="9023c-127">With `openUrl`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="9023c-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-128">Property</span></span> | <span data-ttu-id="9023c-129">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-129">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="9023c-130">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="9023c-130">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="9023c-131">Это поле должно содержать полный и правильно оформленный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9023c-131">This field must contain a full and properly formed URL.</span></span> |

# <a name="json"></a>[<span data-ttu-id="9023c-132">JSON</span><span class="sxs-lookup"><span data-stu-id="9023c-132">JSON</span></span>](#tab/json)

<span data-ttu-id="9023c-133">Следующий код представляет собой пример типа действия `openUrl` в JSON:</span><span class="sxs-lookup"><span data-stu-id="9023c-133">The following code shows an example of `openUrl` action type in JSON:</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[<span data-ttu-id="9023c-134">C#</span><span class="sxs-lookup"><span data-stu-id="9023c-134">C#</span></span>](#tab/csharp)

<span data-ttu-id="9023c-135">Следующий код представляет собой пример типа действия `openUrl` в C#:</span><span class="sxs-lookup"><span data-stu-id="9023c-135">The following code shows an example of `openUrl` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9023c-136">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9023c-136">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="9023c-137">Следующий код представляет собой пример типа действия `openUrl` в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="9023c-137">The following code shows an example of `openUrl` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a><span data-ttu-id="9023c-138">Тип действия messageBack</span><span class="sxs-lookup"><span data-stu-id="9023c-138">Action type messageBack</span></span>

<span data-ttu-id="9023c-139">С помощью `messageBack` вы можете создать полностью настроенное действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="9023c-139">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="9023c-140">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-140">Property</span></span> | <span data-ttu-id="9023c-141">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-141">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="9023c-142">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="9023c-142">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="9023c-143">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="9023c-143">Optional.</span></span> <span data-ttu-id="9023c-144">Применяется пользователем в потоке чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="9023c-144">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="9023c-145">Этот текст не отправляется вашему боту.</span><span class="sxs-lookup"><span data-stu-id="9023c-145">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="9023c-146">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="9023c-146">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9023c-147">Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="9023c-147">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="9023c-148">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="9023c-148">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9023c-149">Используйте это свойство, чтобы упростить разработку бота.</span><span class="sxs-lookup"><span data-stu-id="9023c-149">Use this property to simplify bot development.</span></span> <span data-ttu-id="9023c-150">Ваш код может проверить одно свойство верхнего уровня для выполнения логики бота.</span><span class="sxs-lookup"><span data-stu-id="9023c-150">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="9023c-151">Гибкость `messageBack` означает, что ваш код не может оставить видимое сообщение пользователя в журнале, просто не используя `displayText`.</span><span class="sxs-lookup"><span data-stu-id="9023c-151">The flexibility of `messageBack` means that your code cannot leave a visible user message in the history simply by not using `displayText`.</span></span>

# <a name="json"></a>[<span data-ttu-id="9023c-152">JSON</span><span class="sxs-lookup"><span data-stu-id="9023c-152">JSON</span></span>](#tab/json)

<span data-ttu-id="9023c-153">Следующий код представляет собой пример типа действия `messageBack` в JSON:</span><span class="sxs-lookup"><span data-stu-id="9023c-153">The following code shows an example of `messageBack` action type in JSON:</span></span>

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

<span data-ttu-id="9023c-154">Свойство `value` может быть сериализованной строкой JSON или объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="9023c-154">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

# <a name="c"></a>[<span data-ttu-id="9023c-155">C#</span><span class="sxs-lookup"><span data-stu-id="9023c-155">C#</span></span>](#tab/csharp)

<span data-ttu-id="9023c-156">Следующий код представляет собой пример типа действия `messageBack` в C#:</span><span class="sxs-lookup"><span data-stu-id="9023c-156">The following code shows an example of `messageBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9023c-157">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9023c-157">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="9023c-158">Следующий код представляет собой пример типа действия `messageBack` в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="9023c-158">The following code shows an example of `messageBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a><span data-ttu-id="9023c-159">Пример входящего сообщения</span><span class="sxs-lookup"><span data-stu-id="9023c-159">Inbound message example</span></span>

<span data-ttu-id="9023c-160">`replyToId` содержит идентификатор сообщения, от которого поступило действие карточки.</span><span class="sxs-lookup"><span data-stu-id="9023c-160">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="9023c-161">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="9023c-161">Use it if you want to update the message.</span></span>

<span data-ttu-id="9023c-162">Следующий код представляет собой пример входящего сообщения:</span><span class="sxs-lookup"><span data-stu-id="9023c-162">The following code shows an example of inbound message:</span></span>

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a><span data-ttu-id="9023c-163">Тип действия imBack</span><span class="sxs-lookup"><span data-stu-id="9023c-163">Action type imBack</span></span>

<span data-ttu-id="9023c-164">Действие `imBack` вызывает обратное сообщение боту, как если бы пользователь ввел его в обычном сообщении чата.</span><span class="sxs-lookup"><span data-stu-id="9023c-164">The `imBack` action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="9023c-165">Ваш пользователь и все остальные пользователи канала могут видеть ответ, отправленный с использованием кнопки.</span><span class="sxs-lookup"><span data-stu-id="9023c-165">Your user and all other users in a channel can see the button response.</span></span>

<span data-ttu-id="9023c-166">С помощью `imBack` вы можете создать действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="9023c-166">With `imBack`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="9023c-167">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-167">Property</span></span> | <span data-ttu-id="9023c-168">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-168">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="9023c-169">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="9023c-169">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="9023c-170">Это поле должно содержать текстовую строку, используемую в чате и, следовательно, отправляемую обратно боту.</span><span class="sxs-lookup"><span data-stu-id="9023c-170">This field must contain the text string used in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="9023c-171">Это текст сообщения, который вы обрабатываете в боте для выполнения нужной логики.</span><span class="sxs-lookup"><span data-stu-id="9023c-171">This is the message text you process in your bot to perform the desired logic.</span></span> |

> [!NOTE]
> <span data-ttu-id="9023c-172">Поле `value` является простой строкой.</span><span class="sxs-lookup"><span data-stu-id="9023c-172">The `value` field is a simple string.</span></span> <span data-ttu-id="9023c-173">Форматирование и скрытые символы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9023c-173">There is no support for formatting or hidden characters.</span></span>

# <a name="json"></a>[<span data-ttu-id="9023c-174">JSON</span><span class="sxs-lookup"><span data-stu-id="9023c-174">JSON</span></span>](#tab/json)

<span data-ttu-id="9023c-175">Следующий код представляет собой пример типа действия `imBack` в JSON:</span><span class="sxs-lookup"><span data-stu-id="9023c-175">The following code shows an example of `imBack` action type in JSON:</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[<span data-ttu-id="9023c-176">C#</span><span class="sxs-lookup"><span data-stu-id="9023c-176">C#</span></span>](#tab/csharp)

<span data-ttu-id="9023c-177">Следующий код представляет собой пример типа действия `imBack` в C#:</span><span class="sxs-lookup"><span data-stu-id="9023c-177">The following code shows an example of `imBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9023c-178">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9023c-178">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="9023c-179">Следующий код представляет собой пример типа действия `imBack` в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="9023c-179">The following code shows an example of `imBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a><span data-ttu-id="9023c-180">Тип действия invoke</span><span class="sxs-lookup"><span data-stu-id="9023c-180">Action type invoke</span></span>

<span data-ttu-id="9023c-181">Действие `invoke` используется для вызова [модулей задач](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="9023c-181">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="9023c-182">Действие `invoke` содержит три свойства: `type`, `title` и `value`.</span><span class="sxs-lookup"><span data-stu-id="9023c-182">The `invoke` action contains three properties, `type`, `title`, and `value`.</span></span>

<span data-ttu-id="9023c-183">С помощью `invoke` вы можете создать действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="9023c-183">With `invoke`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="9023c-184">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-184">Property</span></span> | <span data-ttu-id="9023c-185">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-185">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="9023c-186">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="9023c-186">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="9023c-187">Это свойство может содержать строку, строковый объект JSON или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="9023c-187">This property can contain a string, a stringified JSON object, or a JSON object.</span></span> |

# <a name="json"></a>[<span data-ttu-id="9023c-188">JSON</span><span class="sxs-lookup"><span data-stu-id="9023c-188">JSON</span></span>](#tab/json)

<span data-ttu-id="9023c-189">Следующий код представляет собой пример типа действия `invoke` в JSON:</span><span class="sxs-lookup"><span data-stu-id="9023c-189">The following code shows an example of `invoke` action type in JSON:</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="9023c-190">Когда пользователь нажимает кнопку, бот получает объект `value` с некоторой дополнительной информацией.</span><span class="sxs-lookup"><span data-stu-id="9023c-190">When a user selects the button, your bot receives the `value` object with some additional information.</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-191">Тип действия `invoke`, а не `message`, т. е. `activity.Type == "invoke"`.</span><span class="sxs-lookup"><span data-stu-id="9023c-191">The activity type is `invoke` instead of `message` that is `activity.Type == "invoke"`.</span></span>

# <a name="c"></a>[<span data-ttu-id="9023c-192">C#</span><span class="sxs-lookup"><span data-stu-id="9023c-192">C#</span></span>](#tab/csharp)

<span data-ttu-id="9023c-193">Следующий код представляет собой пример типа действия `invoke` в C#:</span><span class="sxs-lookup"><span data-stu-id="9023c-193">The following code shows an example of `invoke` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9023c-194">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9023c-194">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="9023c-195">Следующий код представляет собой пример типа действия `invoke` в Node.js:</span><span class="sxs-lookup"><span data-stu-id="9023c-195">The following code shows an example of `invoke` action type in Node.js:</span></span>

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a><span data-ttu-id="9023c-196">Пример входящего сообщения invoke</span><span class="sxs-lookup"><span data-stu-id="9023c-196">Example of incoming invoke message</span></span>

<span data-ttu-id="9023c-197">Свойство `replyToId` верхнего уровня содержит идентификатор сообщения, от которого поступило действие карточки.</span><span class="sxs-lookup"><span data-stu-id="9023c-197">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="9023c-198">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="9023c-198">Use it if you want to update the message.</span></span>

<span data-ttu-id="9023c-199">Следующий код представляет собой пример входящего сообщения invoke:</span><span class="sxs-lookup"><span data-stu-id="9023c-199">The following code shows an example of incoming invoke message:</span></span>

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a><span data-ttu-id="9023c-200">Тип действия signin</span><span class="sxs-lookup"><span data-stu-id="9023c-200">Action type signin</span></span>

<span data-ttu-id="9023c-201">Тип действия `signin` инициирует поток OAuth, который позволяет ботам подключаться к защищенным службам.</span><span class="sxs-lookup"><span data-stu-id="9023c-201">`signin` action type initiates an OAuth flow that permits bots to connect with secure services.</span></span> <span data-ttu-id="9023c-202">Дополнительные сведения см. в статье о [потоке проверки подлинности в ботах](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="9023c-202">For more information, see [authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="9023c-203">Teams также поддерживает [действия адаптивных карточек](#adaptive-cards-actions) которые используются только в адаптивных карточках.</span><span class="sxs-lookup"><span data-stu-id="9023c-203">Teams also supports [Adaptive Cards actions](#adaptive-cards-actions) that are only used by Adaptive Cards.</span></span>

# <a name="json"></a>[<span data-ttu-id="9023c-204">JSON</span><span class="sxs-lookup"><span data-stu-id="9023c-204">JSON</span></span>](#tab/json)

<span data-ttu-id="9023c-205">Следующий код представляет собой пример типа действия `signin` в JSON:</span><span class="sxs-lookup"><span data-stu-id="9023c-205">The following code shows an example of `signin` action type in JSON:</span></span>

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[<span data-ttu-id="9023c-206">C#</span><span class="sxs-lookup"><span data-stu-id="9023c-206">C#</span></span>](#tab/csharp)

<span data-ttu-id="9023c-207">Следующий код представляет собой пример типа действия `signin` в C#:</span><span class="sxs-lookup"><span data-stu-id="9023c-207">The following code shows an example of `signin` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9023c-208">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9023c-208">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="9023c-209">Следующий код представляет собой пример типа действия `signin` в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="9023c-209">The following code shows an example of `signin` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a><span data-ttu-id="9023c-210">Действия адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="9023c-210">Adaptive Cards actions</span></span>

<span data-ttu-id="9023c-211">Адаптивные карточки поддерживают четыре типа действий:</span><span class="sxs-lookup"><span data-stu-id="9023c-211">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="9023c-212">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="9023c-212">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="9023c-213">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="9023c-213">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="9023c-214">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="9023c-214">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="9023c-215">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="9023c-215">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="9023c-216">Кроме того, вы можете изменить полезные данные адаптивной карточки `Action.Submit` для поддержки существующих действий Bot Framework с помощью свойства `msteams` в объекте `data`, относящемся к `Action.Submit`.</span><span class="sxs-lookup"><span data-stu-id="9023c-216">You can also modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using an `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="9023c-217">Следующий раздел посвящен использованию существующих действий Bot Framework с адаптивными карточками.</span><span class="sxs-lookup"><span data-stu-id="9023c-217">The next section provide details on how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-218">Добавление `msteams` к данным с помощью действия Bot Framework не работает с модулем задач адаптивной карточки.</span><span class="sxs-lookup"><span data-stu-id="9023c-218">Adding `msteams` to data with a Bot Framework action does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="9023c-219">Адаптивные карточки с действием messageBack</span><span class="sxs-lookup"><span data-stu-id="9023c-219">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="9023c-220">Чтобы включить действие `messageBack` в адаптивную карточку, включите в объект `msteams` следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="9023c-220">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-221">При необходимости можно включить в объект `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="9023c-221">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="9023c-222">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-222">Property</span></span> | <span data-ttu-id="9023c-223">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-223">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="9023c-224">Установите значение `messageBack`.</span><span class="sxs-lookup"><span data-stu-id="9023c-224">Set to `messageBack`.</span></span> |
| `displayText` | <span data-ttu-id="9023c-225">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="9023c-225">Optional.</span></span> <span data-ttu-id="9023c-226">Применяется пользователем в потоке чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="9023c-226">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="9023c-227">Этот текст не отправляется вашему боту.</span><span class="sxs-lookup"><span data-stu-id="9023c-227">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="9023c-228">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="9023c-228">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9023c-229">Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="9023c-229">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="9023c-230">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="9023c-230">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9023c-231">Используйте это свойство, чтобы упростить разработку бота.</span><span class="sxs-lookup"><span data-stu-id="9023c-231">Use this property to simplify bot development.</span></span> <span data-ttu-id="9023c-232">Ваш код может проверить одно свойство верхнего уровня для выполнения логики бота.</span><span class="sxs-lookup"><span data-stu-id="9023c-232">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="9023c-233">Следующий код представляет собой пример адаптивных карточек с действием `messageBack`:</span><span class="sxs-lookup"><span data-stu-id="9023c-233">The following code shows an example of Adaptive Cards with `messageBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="9023c-234">Адаптивные карточки с действием imBack</span><span class="sxs-lookup"><span data-stu-id="9023c-234">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="9023c-235">Чтобы включить действие `imBack` в адаптивную карточку, включите в объект `msteams` следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="9023c-235">To include an `imBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-236">При необходимости можно включить в объект `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="9023c-236">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="9023c-237">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-237">Property</span></span> | <span data-ttu-id="9023c-238">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-238">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="9023c-239">Установите значение `imBack`.</span><span class="sxs-lookup"><span data-stu-id="9023c-239">Set to `imBack`.</span></span> |
| `value` | <span data-ttu-id="9023c-240">Строка, которую необходимо вернуть в чат.</span><span class="sxs-lookup"><span data-stu-id="9023c-240">String that needs to be echoed back in the chat.</span></span> |

<span data-ttu-id="9023c-241">Следующий код представляет собой пример адаптивных карточек с действием `imBack`:</span><span class="sxs-lookup"><span data-stu-id="9023c-241">The following code shows an example of Adaptive Cards with `imBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="9023c-242">Адаптивные карточки с действием signin</span><span class="sxs-lookup"><span data-stu-id="9023c-242">Adaptive Cards with signin action</span></span>

<span data-ttu-id="9023c-243">Чтобы включить действие `signin` в адаптивную карточку, включите в объект `msteams` следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="9023c-243">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-244">При необходимости можно включить в объект `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="9023c-244">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="9023c-245">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-245">Property</span></span> | <span data-ttu-id="9023c-246">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-246">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="9023c-247">Установите значение `signin`.</span><span class="sxs-lookup"><span data-stu-id="9023c-247">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="9023c-248">В качестве значения задайте URL-адрес для перенаправления.</span><span class="sxs-lookup"><span data-stu-id="9023c-248">Set to the URL where you want to redirect.</span></span>  |

<span data-ttu-id="9023c-249">Следующий код представляет собой пример адаптивных карточек с действием `signin`:</span><span class="sxs-lookup"><span data-stu-id="9023c-249">The following code shows an example of Adaptive Cards with `signin` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="9023c-250">Адаптивные карточки с действием invoke</span><span class="sxs-lookup"><span data-stu-id="9023c-250">Adaptive Cards with invoke action</span></span>

<span data-ttu-id="9023c-251">Чтобы включить действие `invoke` в адаптивную карточку, включите в объект `msteams` следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="9023c-251">To include an `invoke` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="9023c-252">При необходимости можно включить в объект `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="9023c-252">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="9023c-253">Свойство</span><span class="sxs-lookup"><span data-stu-id="9023c-253">Property</span></span> | <span data-ttu-id="9023c-254">Описание</span><span class="sxs-lookup"><span data-stu-id="9023c-254">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="9023c-255">Установите значение `task/fetch`.</span><span class="sxs-lookup"><span data-stu-id="9023c-255">Set to `task/fetch`.</span></span> |
| `data` | <span data-ttu-id="9023c-256">Задайте значение.</span><span class="sxs-lookup"><span data-stu-id="9023c-256">Set the value.</span></span>  |

<span data-ttu-id="9023c-257">Следующий код представляет собой пример адаптивных карточек с действием `invoke`:</span><span class="sxs-lookup"><span data-stu-id="9023c-257">The following code shows an example of Adaptive Cards with `invoke` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit",
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

<span data-ttu-id="9023c-258">Следующий код представляет собой пример адаптивных карточек с действием `invoke` и дополнительными полезными данными:</span><span class="sxs-lookup"><span data-stu-id="9023c-258">The following code shows an example of Adaptive Cards with `invoke` action with additional payload data:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```

## <a name="see-also"></a><span data-ttu-id="9023c-259">См. также</span><span class="sxs-lookup"><span data-stu-id="9023c-259">See also</span></span>

[<span data-ttu-id="9023c-260">Справочные материалы о карточках</span><span class="sxs-lookup"><span data-stu-id="9023c-260">Cards reference</span></span>](./cards-reference.md)

## <a name="next-step"></a><span data-ttu-id="9023c-261">Следующее действие</span><span class="sxs-lookup"><span data-stu-id="9023c-261">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9023c-262">Универсальные действия для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="9023c-262">Universal Actions for Adaptive Cards</span></span>](../cards/Universal-actions-for-adaptive-cards/Overview.md)
