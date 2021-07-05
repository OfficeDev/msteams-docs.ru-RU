---
title: Добавление действий карты в боте
description: Описывает действия карт в Microsoft Teams и их использование в ботах
localization_priority: Normal
ms.topic: conceptual
keywords: teams bots cards actions
ms.openlocfilehash: 4af152f6179785687d4fd7371d202c56e1aee170
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254204"
---
# <a name="card-actions"></a><span data-ttu-id="6bbb9-104">Действия карточек</span><span class="sxs-lookup"><span data-stu-id="6bbb9-104">Card actions</span></span>

<span data-ttu-id="6bbb9-105">Карты, используемые ботами и расширениями обмена сообщениями в Teams поддерживают следующие [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) типы действий:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-105">Cards used by bots and messaging extensions in Teams support the following activity [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) types:</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-106">Действия `CardAction` отличаются от `potentialActions` Office 365 соединители, когда используются соединители.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-106">The `CardAction` actions differ from `potentialActions` for Office 365 Connector cards when used from connectors.</span></span>

| <span data-ttu-id="6bbb9-107">Type</span><span class="sxs-lookup"><span data-stu-id="6bbb9-107">Type</span></span> | <span data-ttu-id="6bbb9-108">Action</span><span class="sxs-lookup"><span data-stu-id="6bbb9-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="6bbb9-109">Открывает URL-адрес в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="6bbb9-110">Отправляет сообщение и полезное сообщение боту от пользователя, который выбрал кнопку или постучал по карте.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-110">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="6bbb9-111">Отправляет отдельное сообщение в поток чата.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-111">Sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="6bbb9-112">Отправляет сообщение боту от пользователя, который выбрал кнопку или постучал по карте.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-112">Sends a message to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="6bbb9-113">Это сообщение от пользователя к боту видно всем участникам беседы.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-113">This message from user to bot is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="6bbb9-114">Отправляет сообщение и полезное сообщение боту от пользователя, который выбрал кнопку или постучал по карте.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-114">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="6bbb9-115">Это сообщение не отображается.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-115">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="6bbb9-116">Инициирует поток OAuth, позволяя ботам подключаться к безопасным службам.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-116">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="6bbb9-117">Teams не поддерживает `CardAction` типы, не указанные в предыдущей таблице.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-117">Teams does not support `CardAction` types not listed in the previous table.</span></span>
>* <span data-ttu-id="6bbb9-118">Teams не поддерживает `potentialActions` свойство.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-118">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="6bbb9-119">Действия карт отличаются от [предлагаемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в Bot Framework или Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-119">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework or Azure Bot Service.</span></span> <span data-ttu-id="6bbb9-120">Предлагаемые действия не поддерживаются в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-120">Suggested actions are not supported in Microsoft Teams.</span></span> <span data-ttu-id="6bbb9-121">Если вы хотите, чтобы в сообщении бота Teams кнопки, используйте карточку.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-121">If you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="6bbb9-122">Если вы используете действие карты в рамках расширения обмена сообщениями, эти действия не будут работать до отправки карты в канал.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-122">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="6bbb9-123">Действия не работают, пока карта находится в поле составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-123">The actions do not work while the card is in the compose message box.</span></span>

## <a name="action-type-openurl"></a><span data-ttu-id="6bbb9-124">Тип действия openUrl</span><span class="sxs-lookup"><span data-stu-id="6bbb9-124">Action type openUrl</span></span>

<span data-ttu-id="6bbb9-125">`openUrl` Тип действия указывает URL-адрес для запуска в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-125">`openUrl` action type specifies a URL to launch in the default browser.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-126">Ваш бот не получает уведомления о выборе кнопки.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-126">Your bot does not receive any notice on which button was selected.</span></span>

<span data-ttu-id="6bbb9-127">С помощью этого действия можно `openUrl` создать действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-127">With `openUrl`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="6bbb9-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-128">Property</span></span> | <span data-ttu-id="6bbb9-129">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-129">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6bbb9-130">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-130">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="6bbb9-131">Это поле должно содержать полный и правильно сформированный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-131">This field must contain a full and properly formed URL.</span></span> |

# <a name="json"></a>[<span data-ttu-id="6bbb9-132">JSON</span><span class="sxs-lookup"><span data-stu-id="6bbb9-132">JSON</span></span>](#tab/json)

<span data-ttu-id="6bbb9-133">В следующем коде показан пример `openUrl` типа действия в JSON:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-133">The following code shows an example of `openUrl` action type in JSON:</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[<span data-ttu-id="6bbb9-134">C#</span><span class="sxs-lookup"><span data-stu-id="6bbb9-134">C#</span></span>](#tab/csharp)

<span data-ttu-id="6bbb9-135">В следующем коде показан пример типа действия `openUrl` в C#:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-135">The following code shows an example of `openUrl` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6bbb9-136">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bbb9-136">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6bbb9-137">В следующем коде показан пример типа `openUrl` действий в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-137">The following code shows an example of `openUrl` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a><span data-ttu-id="6bbb9-138">MessageBack типа действия</span><span class="sxs-lookup"><span data-stu-id="6bbb9-138">Action type messageBack</span></span>

<span data-ttu-id="6bbb9-139">С `messageBack` помощью этого параметра можно создать полностью настраиваемые действия со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-139">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="6bbb9-140">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-140">Property</span></span> | <span data-ttu-id="6bbb9-141">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-141">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6bbb9-142">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-142">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="6bbb9-143">Необязательно.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-143">Optional.</span></span> <span data-ttu-id="6bbb9-144">Используется пользователем в потоке чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-144">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="6bbb9-145">Этот текст не отправляется в бот.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-145">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="6bbb9-146">Отправляется в бот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-146">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6bbb9-147">Вы можете кодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-147">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="6bbb9-148">Отправляется в бот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-148">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6bbb9-149">Используйте это свойство для упрощения разработки ботов.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-149">Use this property to simplify bot development.</span></span> <span data-ttu-id="6bbb9-150">Код может проверить одно свойство верхнего уровня для отправки логики бота.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-150">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="6bbb9-151">Гибкость означает, что код не может оставить видимое сообщение пользователя в истории, просто `messageBack` не используя `displayText` .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-151">The flexibility of `messageBack` means that your code cannot leave a visible user message in the history simply by not using `displayText`.</span></span>

# <a name="json"></a>[<span data-ttu-id="6bbb9-152">JSON</span><span class="sxs-lookup"><span data-stu-id="6bbb9-152">JSON</span></span>](#tab/json)

<span data-ttu-id="6bbb9-153">В следующем коде показан пример `messageBack` типа действия в JSON:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-153">The following code shows an example of `messageBack` action type in JSON:</span></span>

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

<span data-ttu-id="6bbb9-154">Свойство `value` может быть как сериализированной строкой JSON, так и объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-154">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

# <a name="c"></a>[<span data-ttu-id="6bbb9-155">C#</span><span class="sxs-lookup"><span data-stu-id="6bbb9-155">C#</span></span>](#tab/csharp)

<span data-ttu-id="6bbb9-156">В следующем коде показан пример типа действия `messageBack` в C#:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-156">The following code shows an example of `messageBack` action type in C#:</span></span>

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6bbb9-157">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bbb9-157">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6bbb9-158">В следующем коде показан пример типа `messageBack` действий в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-158">The following code shows an example of `messageBack` action type in JavaScript:</span></span>

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

### <a name="inbound-message-example"></a><span data-ttu-id="6bbb9-159">Пример входящие сообщения</span><span class="sxs-lookup"><span data-stu-id="6bbb9-159">Inbound message example</span></span>

<span data-ttu-id="6bbb9-160">`replyToId` содержит ID сообщения, из которое пришло действие карты.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-160">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="6bbb9-161">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-161">Use it if you want to update the message.</span></span>

<span data-ttu-id="6bbb9-162">В следующем коде показан пример входящие сообщения:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-162">The following code shows an example of inbound message:</span></span>

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

## <a name="action-type-imback"></a><span data-ttu-id="6bbb9-163">Тип действия imBack</span><span class="sxs-lookup"><span data-stu-id="6bbb9-163">Action type imBack</span></span>

<span data-ttu-id="6bbb9-164">Действие вызывает возвращение сообщения в бот, как если бы пользователь впечатлл `imBack` его в обычном сообщении чата.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-164">The `imBack` action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="6bbb9-165">Пользователь и все другие пользователи канала могут видеть отклик кнопки.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-165">Your user and all other users in a channel can see the button response.</span></span>

<span data-ttu-id="6bbb9-166">С помощью этого действия можно `imBack` создать действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-166">With `imBack`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="6bbb9-167">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-167">Property</span></span> | <span data-ttu-id="6bbb9-168">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-168">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6bbb9-169">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-169">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="6bbb9-170">Это поле должно содержать текстовую строку, используемую в чате, и поэтому отправляется обратно в бот.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-170">This field must contain the text string used in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="6bbb9-171">Это текст сообщения, который вы обрабатываете в боте для выполнения нужной логики.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-171">This is the message text you process in your bot to perform the desired logic.</span></span> |

> [!NOTE]
> <span data-ttu-id="6bbb9-172">Поле `value` — это простая строка.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-172">The `value` field is a simple string.</span></span> <span data-ttu-id="6bbb9-173">Нет поддержки форматирования или скрытых символов.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-173">There is no support for formatting or hidden characters.</span></span>

# <a name="json"></a>[<span data-ttu-id="6bbb9-174">JSON</span><span class="sxs-lookup"><span data-stu-id="6bbb9-174">JSON</span></span>](#tab/json)

<span data-ttu-id="6bbb9-175">В следующем коде показан пример `imBack` типа действия в JSON:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-175">The following code shows an example of `imBack` action type in JSON:</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[<span data-ttu-id="6bbb9-176">C#</span><span class="sxs-lookup"><span data-stu-id="6bbb9-176">C#</span></span>](#tab/csharp)

<span data-ttu-id="6bbb9-177">В следующем коде показан пример типа действия `imBack` в C#:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-177">The following code shows an example of `imBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6bbb9-178">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bbb9-178">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6bbb9-179">В следующем коде показан пример типа `imBack` действий в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-179">The following code shows an example of `imBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a><span data-ttu-id="6bbb9-180">Вызов типа действия</span><span class="sxs-lookup"><span data-stu-id="6bbb9-180">Action type invoke</span></span>

<span data-ttu-id="6bbb9-181">Действие `invoke` используется для наводки [модулей задач.](~/task-modules-and-cards/task-modules/task-modules-bots.md)</span><span class="sxs-lookup"><span data-stu-id="6bbb9-181">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="6bbb9-182">Действие `invoke` содержит три `type` свойства, и `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-182">The `invoke` action contains three properties, `type`, `title`, and `value`.</span></span>

<span data-ttu-id="6bbb9-183">С помощью этого действия можно `invoke` создать действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-183">With `invoke`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="6bbb9-184">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-184">Property</span></span> | <span data-ttu-id="6bbb9-185">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-185">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="6bbb9-186">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-186">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="6bbb9-187">Это свойство может содержать строку, объект JSON или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-187">This property can contain a string, a stringified JSON object, or a JSON object.</span></span> |

# <a name="json"></a>[<span data-ttu-id="6bbb9-188">JSON</span><span class="sxs-lookup"><span data-stu-id="6bbb9-188">JSON</span></span>](#tab/json)

<span data-ttu-id="6bbb9-189">В следующем коде показан пример `invoke` типа действия в JSON:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-189">The following code shows an example of `invoke` action type in JSON:</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="6bbb9-190">Когда пользователь выбирает кнопку, бот получает объект `value` с некоторыми дополнительными сведениями.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-190">When a user selects the button, your bot receives the `value` object with some additional information.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-191">Вместо этого тип действия `invoke` `message` `activity.Type == "invoke"` .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-191">The activity type is `invoke` instead of `message` that is `activity.Type == "invoke"`.</span></span>

# <a name="c"></a>[<span data-ttu-id="6bbb9-192">C#</span><span class="sxs-lookup"><span data-stu-id="6bbb9-192">C#</span></span>](#tab/csharp)

<span data-ttu-id="6bbb9-193">В следующем коде показан пример типа действия `invoke` в C#:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-193">The following code shows an example of `invoke` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6bbb9-194">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bbb9-194">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6bbb9-195">В следующем коде показан пример типа действия `invoke` в Node.js:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-195">The following code shows an example of `invoke` action type in Node.js:</span></span>

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

### <a name="example-of-incoming-invoke-message"></a><span data-ttu-id="6bbb9-196">Пример входящих сообщений вызова</span><span class="sxs-lookup"><span data-stu-id="6bbb9-196">Example of incoming invoke message</span></span>

<span data-ttu-id="6bbb9-197">Свойство верхнего уровня содержит ID сообщения, из которое `replyToId` пришло действие карты.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-197">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="6bbb9-198">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-198">Use it if you want to update the message.</span></span>

<span data-ttu-id="6bbb9-199">В следующем коде показан пример входящих сообщений вызова:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-199">The following code shows an example of incoming invoke message:</span></span>

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

## <a name="action-type-signin"></a><span data-ttu-id="6bbb9-200">Знак типа действия</span><span class="sxs-lookup"><span data-stu-id="6bbb9-200">Action type signin</span></span>

<span data-ttu-id="6bbb9-201">`signin` Тип действия инициирует поток OAuth, который позволяет ботам подключаться к безопасным службам.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-201">`signin` action type initiates an OAuth flow that permits bots to connect with secure services.</span></span> <span data-ttu-id="6bbb9-202">Дополнительные сведения см. в [потоке проверки подлинности в ботах.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="6bbb9-202">For more information, see [authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="6bbb9-203">Teams также поддерживает действия [адаптивных карт,](#adaptive-cards-actions) которые используются только адаптивными картами.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-203">Teams also supports [Adaptive Cards actions](#adaptive-cards-actions) that are only used by Adaptive Cards.</span></span>

# <a name="json"></a>[<span data-ttu-id="6bbb9-204">JSON</span><span class="sxs-lookup"><span data-stu-id="6bbb9-204">JSON</span></span>](#tab/json)

<span data-ttu-id="6bbb9-205">В следующем коде показан пример `signin` типа действия в JSON:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-205">The following code shows an example of `signin` action type in JSON:</span></span>

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[<span data-ttu-id="6bbb9-206">C#</span><span class="sxs-lookup"><span data-stu-id="6bbb9-206">C#</span></span>](#tab/csharp)

<span data-ttu-id="6bbb9-207">В следующем коде показан пример типа действия `signin` в C#:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-207">The following code shows an example of `signin` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="6bbb9-208">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bbb9-208">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="6bbb9-209">В следующем коде показан пример типа `signin` действий в JavaScript:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-209">The following code shows an example of `signin` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a><span data-ttu-id="6bbb9-210">Действия адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="6bbb9-210">Adaptive Cards actions</span></span>

<span data-ttu-id="6bbb9-211">Адаптивные карты поддерживают четыре типа действий:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-211">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="6bbb9-212">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="6bbb9-212">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="6bbb9-213">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="6bbb9-213">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="6bbb9-214">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="6bbb9-214">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="6bbb9-215">Action.Exeмило</span><span class="sxs-lookup"><span data-stu-id="6bbb9-215">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="6bbb9-216">Вы также можете изменить полезной нагрузки адаптивной карты для поддержки существующих действий Bot Framework с помощью свойства `Action.Submit` `msteams` в `data` объекте `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-216">You can also modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using an `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="6bbb9-217">В следующем разделе вы можете узнать, как использовать существующие действия Bot Framework с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-217">The next section provide details on how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-218">Добавление к данным с помощью действия Bot Framework не работает с модулем адаптивной `msteams` карты.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-218">Adding `msteams` to data with a Bot Framework action does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="6bbb9-219">Адаптивные карты с действием messageBack</span><span class="sxs-lookup"><span data-stu-id="6bbb9-219">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="6bbb9-220">Чтобы включить `messageBack` действие с адаптивной картой, включим в объект следующие `msteams` сведения:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-220">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-221">При необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-221">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6bbb9-222">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-222">Property</span></span> | <span data-ttu-id="6bbb9-223">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-223">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6bbb9-224">Установите `messageBack` для .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-224">Set to `messageBack`.</span></span> |
| `displayText` | <span data-ttu-id="6bbb9-225">Необязательно.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-225">Optional.</span></span> <span data-ttu-id="6bbb9-226">Используется пользователем в потоке чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-226">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="6bbb9-227">Этот текст не отправляется в бот.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-227">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="6bbb9-228">Отправляется в бот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-228">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6bbb9-229">Вы можете кодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-229">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="6bbb9-230">Отправляется в бот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-230">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="6bbb9-231">Используйте это свойство для упрощения разработки ботов.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-231">Use this property to simplify bot development.</span></span> <span data-ttu-id="6bbb9-232">Код может проверить одно свойство верхнего уровня для отправки логики бота.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-232">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="6bbb9-233">В следующем коде показан пример адаптивных карт с `messageBack` действием:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-233">The following code shows an example of Adaptive Cards with `messageBack` action:</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="6bbb9-234">Адаптивные карты с действием imBack</span><span class="sxs-lookup"><span data-stu-id="6bbb9-234">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="6bbb9-235">Чтобы включить `imBack` действие с адаптивной картой, включив в объект следующие `msteams` сведения:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-235">To include an `imBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-236">При необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-236">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6bbb9-237">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-237">Property</span></span> | <span data-ttu-id="6bbb9-238">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-238">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6bbb9-239">Установите `imBack` для .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-239">Set to `imBack`.</span></span> |
| `value` | <span data-ttu-id="6bbb9-240">Строка, которую необходимо повторить в чате.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-240">String that needs to be echoed back in the chat.</span></span> |

<span data-ttu-id="6bbb9-241">В следующем коде показан пример адаптивных карт с `imBack` действием:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-241">The following code shows an example of Adaptive Cards with `imBack` action:</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="6bbb9-242">Адаптивные карты с действием signin</span><span class="sxs-lookup"><span data-stu-id="6bbb9-242">Adaptive Cards with signin action</span></span>

<span data-ttu-id="6bbb9-243">Чтобы включить `signin` действие с адаптивной картой, включим в объект следующие `msteams` сведения:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-243">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-244">При необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-244">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6bbb9-245">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-245">Property</span></span> | <span data-ttu-id="6bbb9-246">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-246">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6bbb9-247">Установите `signin` для .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-247">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="6bbb9-248">Установите URL-адрес, в котором необходимо перенаправить.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-248">Set to the URL where you want to redirect.</span></span>  |

<span data-ttu-id="6bbb9-249">В следующем коде показан пример адаптивных карт с `signin` действием:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-249">The following code shows an example of Adaptive Cards with `signin` action:</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="6bbb9-250">Адаптивные карты с действием вызова</span><span class="sxs-lookup"><span data-stu-id="6bbb9-250">Adaptive Cards with invoke action</span></span>

<span data-ttu-id="6bbb9-251">Чтобы включить `invoke` действие с адаптивной картой, включив в объект следующие `msteams` сведения:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-251">To include an `invoke` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="6bbb9-252">При необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-252">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="6bbb9-253">Свойство</span><span class="sxs-lookup"><span data-stu-id="6bbb9-253">Property</span></span> | <span data-ttu-id="6bbb9-254">Описание</span><span class="sxs-lookup"><span data-stu-id="6bbb9-254">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="6bbb9-255">Установите `task/fetch` для .</span><span class="sxs-lookup"><span data-stu-id="6bbb9-255">Set to `task/fetch`.</span></span> |
| `data` | <span data-ttu-id="6bbb9-256">Установите значение.</span><span class="sxs-lookup"><span data-stu-id="6bbb9-256">Set the value.</span></span>  |

<span data-ttu-id="6bbb9-257">В следующем коде показан пример адаптивных карт с `invoke` действием:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-257">The following code shows an example of Adaptive Cards with `invoke` action:</span></span>

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

<span data-ttu-id="6bbb9-258">В следующем коде показан пример адаптивных карт с действием `invoke` с дополнительными данными полезной нагрузки:</span><span class="sxs-lookup"><span data-stu-id="6bbb9-258">The following code shows an example of Adaptive Cards with `invoke` action with additional payload data:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="6bbb9-259">См. также</span><span class="sxs-lookup"><span data-stu-id="6bbb9-259">See also</span></span>

[<span data-ttu-id="6bbb9-260">Ссылки на карточки</span><span class="sxs-lookup"><span data-stu-id="6bbb9-260">Cards reference</span></span>](./cards-reference.md)

## <a name="next-step"></a><span data-ttu-id="6bbb9-261">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="6bbb9-261">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6bbb9-262">Универсальные действия для адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="6bbb9-262">Universal Actions for Adaptive Cards</span></span>](../cards/Universal-actions-for-adaptive-cards/Overview.md)
