---
title: Добавление действий карточки в Bot
description: Описывает действия с карточками в Microsoft Teams и способы их использования в Боты.
keywords: действия карточек Боты Teams
ms.openlocfilehash: e0b050cde9adf5bd811d5d95ce1c6f1bf60546a1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675373"
---
# <a name="card-actions"></a><span data-ttu-id="0a0da-104">Действия с картой</span><span class="sxs-lookup"><span data-stu-id="0a0da-104">Card actions</span></span>

<span data-ttu-id="0a0da-105">Карты, используемые Боты и расширениями обмена сообщениями в Teams,[`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)поддерживают следующие типы действий ().</span><span class="sxs-lookup"><span data-stu-id="0a0da-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="0a0da-106">Обратите внимание, что эти `potentialActions` действия отличаются для соединителей карт Office 365 при их использовании от соединителей.</span><span class="sxs-lookup"><span data-stu-id="0a0da-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="0a0da-107">Тип</span><span class="sxs-lookup"><span data-stu-id="0a0da-107">Type</span></span> | <span data-ttu-id="0a0da-108">Action</span><span class="sxs-lookup"><span data-stu-id="0a0da-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="0a0da-109">Открывает URL-адрес в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0a0da-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="0a0da-110">Отправляет сообщение и полезные данные в Bot (от пользователя, который нанажали кнопку или выделяют карточку) и отправляет отдельное сообщение в поток чата.</span><span class="sxs-lookup"><span data-stu-id="0a0da-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="0a0da-111">Отправляет сообщение на Bot (от пользователя, который нанажали кнопку или нанажали карточку).</span><span class="sxs-lookup"><span data-stu-id="0a0da-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="0a0da-112">Это сообщение (от пользователя к Bot) видимо всем участникам беседы.</span><span class="sxs-lookup"><span data-stu-id="0a0da-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="0a0da-113">Отправляет сообщение и полезные данные в Bot (от пользователя, который нанажали кнопку или нанажали карточку).</span><span class="sxs-lookup"><span data-stu-id="0a0da-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="0a0da-114">Это сообщение не отображается.</span><span class="sxs-lookup"><span data-stu-id="0a0da-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="0a0da-115">Инициирует процесс OAuth, позволяя Боты подключаться к защищенным службам.</span><span class="sxs-lookup"><span data-stu-id="0a0da-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="0a0da-116">Teams не поддерживает `CardAction` типы, не указанные в предыдущей таблице.</span><span class="sxs-lookup"><span data-stu-id="0a0da-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="0a0da-117">Teams не поддерживает это `potentialActions` свойство.</span><span class="sxs-lookup"><span data-stu-id="0a0da-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="0a0da-118">Действия с картой отличаются от [предлагаемых действий](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button) в службе Bot Framework/Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="0a0da-118">Card actions are different than [suggested actions](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="0a0da-119">Предлагаемые действия не поддерживаются в Microsoft teams: Если вы хотите, чтобы кнопки отображались в сообщении ленты Teams, используйте карточку.</span><span class="sxs-lookup"><span data-stu-id="0a0da-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="0a0da-120">Если вы используете действие карточки в составе расширения для обмена сообщениями, действия не будут работать до тех пор, пока карточка не будет отправлена в канал (они не будут работать, пока карточка находится в окне сообщения создания).</span><span class="sxs-lookup"><span data-stu-id="0a0da-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="0a0da-121">Teams также поддерживает [действия со адаптивными карточками](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), которые используются только адаптивными картами.</span><span class="sxs-lookup"><span data-stu-id="0a0da-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="0a0da-122">Эти действия перечислены в отдельном разделе в конце этой ссылки.</span><span class="sxs-lookup"><span data-stu-id="0a0da-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="0a0da-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="0a0da-123">openUrl</span></span>

<span data-ttu-id="0a0da-124">Этот тип действия задает URL-адрес, который будет запускаться в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0a0da-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="0a0da-125">Обратите внимание, что для ленты не отображается уведомление о нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="0a0da-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="0a0da-126">`value` Поле должно содержать полный и правильно сформированный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0a0da-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="0a0da-127">мессажебакк</span><span class="sxs-lookup"><span data-stu-id="0a0da-127">messageBack</span></span>

<span data-ttu-id="0a0da-128">С `messageBack`помощью можно создать полностью настраиваемое действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="0a0da-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="0a0da-129">Свойство</span><span class="sxs-lookup"><span data-stu-id="0a0da-129">Property</span></span> | <span data-ttu-id="0a0da-130">Описание</span><span class="sxs-lookup"><span data-stu-id="0a0da-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="0a0da-131">Отображается в виде подписи кнопки.</span><span class="sxs-lookup"><span data-stu-id="0a0da-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="0a0da-132">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="0a0da-132">Optional.</span></span> <span data-ttu-id="0a0da-133">Подается пользователю в поток чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="0a0da-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="0a0da-134">Этот текст *не* отправляется в робот.</span><span class="sxs-lookup"><span data-stu-id="0a0da-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="0a0da-135">Отправляется на ваш робот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="0a0da-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="0a0da-136">Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="0a0da-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="0a0da-137">Отправляется на ваш робот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="0a0da-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="0a0da-138">Используйте это свойство для упрощения разработки в Bot: ваш код может проверять одно свойство верхнего уровня для обработки логики Bot.</span><span class="sxs-lookup"><span data-stu-id="0a0da-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="0a0da-139">Гибкость `messageBack` заключается в том, что ваш код может не оставлять видимое пользовательское сообщение в истории простым, не используя `displayText`.</span><span class="sxs-lookup"><span data-stu-id="0a0da-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="0a0da-140">`value` Свойство может быть либо сериализованной СТРОКой JSON, либо объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="0a0da-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="0a0da-141">Пример входящего сообщения</span><span class="sxs-lookup"><span data-stu-id="0a0da-141">Inbound message example</span></span>

<span data-ttu-id="0a0da-142">`replyToId`содержит идентификатор сообщения, из которого поступило действие карточки.</span><span class="sxs-lookup"><span data-stu-id="0a0da-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="0a0da-143">Используйте его, если хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="0a0da-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="0a0da-144">Обратное воспроизведение</span><span class="sxs-lookup"><span data-stu-id="0a0da-144">imBack</span></span>

<span data-ttu-id="0a0da-145">Это действие вызывает возврат сообщения для ленты, как если бы пользователь ввел его в обычном сообщении чата.</span><span class="sxs-lookup"><span data-stu-id="0a0da-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="0a0da-146">Пользователь и все остальные пользователи, если они находятся в канале, увидят этот ответ на эту кнопку.</span><span class="sxs-lookup"><span data-stu-id="0a0da-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="0a0da-147">`value` Поле должно содержать текстовую строку, которая помещается в чат и, следовательно, отправляется обратно в Bot.</span><span class="sxs-lookup"><span data-stu-id="0a0da-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="0a0da-148">Это текст сообщения, которое будет обрабатываться в Bot, чтобы выполнить нужную логику.</span><span class="sxs-lookup"><span data-stu-id="0a0da-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="0a0da-149">Note: это поле представляет собой простую строку — поддержка форматирования и скрытых символов отсутствует.</span><span class="sxs-lookup"><span data-stu-id="0a0da-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="0a0da-150">метода</span><span class="sxs-lookup"><span data-stu-id="0a0da-150">invoke</span></span>

<span data-ttu-id="0a0da-151">`invoke` Действие используется для вызова [модулей задач](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span><span class="sxs-lookup"><span data-stu-id="0a0da-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="0a0da-152">`invoke` Действие содержит три свойства: `type`, `title`и `value`.</span><span class="sxs-lookup"><span data-stu-id="0a0da-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="0a0da-153">`value` Свойство может содержать строку, объект преобразованного JSON или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="0a0da-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="0a0da-154">Когда пользователь нажимает кнопку, ваш `value` объект Bot будет получать объект с дополнительными сведениями.</span><span class="sxs-lookup"><span data-stu-id="0a0da-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="0a0da-155">Обратите внимание, что вместо него будет `invoke` использоваться тип `message` действия`activity.Type == "invoke"`().</span><span class="sxs-lookup"><span data-stu-id="0a0da-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="0a0da-156">Пример: вызов определения кнопки (.NET)</span><span class="sxs-lookup"><span data-stu-id="0a0da-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="0a0da-157">Пример: сообщение входящего вызова</span><span class="sxs-lookup"><span data-stu-id="0a0da-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="0a0da-158">Свойство верхнего уровня `replyToId` содержит идентификатор сообщения, из которого поступило действие карточки.</span><span class="sxs-lookup"><span data-stu-id="0a0da-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="0a0da-159">Используйте его, если хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="0a0da-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="0a0da-160">SignIn</span><span class="sxs-lookup"><span data-stu-id="0a0da-160">signin</span></span>

<span data-ttu-id="0a0da-161">Инициирует процесс OAuth, позволяя Боты подключаться к защищенным службам, как описано ниже. [процесс проверки подлинности в Боты](~/bots/how-to/authentication/auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="0a0da-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="0a0da-162">Действия с адаптивными карточками</span><span class="sxs-lookup"><span data-stu-id="0a0da-162">Adaptive Cards actions</span></span>

<span data-ttu-id="0a0da-163">Адаптивные карты поддерживают три типа действий:</span><span class="sxs-lookup"><span data-stu-id="0a0da-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="0a0da-164">Action. OpenUrl</span><span class="sxs-lookup"><span data-stu-id="0a0da-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="0a0da-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="0a0da-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="0a0da-166">Action. ShowCard</span><span class="sxs-lookup"><span data-stu-id="0a0da-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="0a0da-167">В дополнение к приведенным выше действиям можно изменить данные адаптивной карточки `Action.Submit` , чтобы поддерживать существующие действия с помощью ленты с `msteams` помощью свойства в `data` объекте `Action.Submit`.</span><span class="sxs-lookup"><span data-stu-id="0a0da-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="0a0da-168">В следующих разделах подробно описано, как использовать существующие действия с использованием ленты с адаптивными картами.</span><span class="sxs-lookup"><span data-stu-id="0a0da-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="0a0da-169">Адаптивные карты с действием Мессажебакк</span><span class="sxs-lookup"><span data-stu-id="0a0da-169">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="0a0da-170">Чтобы включить `messageBack` действие с помощью адаптивной карточки, добавьте следующие сведения в `msteams` объект.</span><span class="sxs-lookup"><span data-stu-id="0a0da-170">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="0a0da-171">Обратите внимание, что при необходимости вы можете добавить `data` в объект дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="0a0da-171">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="0a0da-172">Свойство</span><span class="sxs-lookup"><span data-stu-id="0a0da-172">Property</span></span> | <span data-ttu-id="0a0da-173">Описание</span><span class="sxs-lookup"><span data-stu-id="0a0da-173">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="0a0da-174">Значение`messageBack`</span><span class="sxs-lookup"><span data-stu-id="0a0da-174">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="0a0da-175">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="0a0da-175">Optional.</span></span> <span data-ttu-id="0a0da-176">Подается пользователю в поток чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="0a0da-176">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="0a0da-177">Этот текст *не* отправляется в робот.</span><span class="sxs-lookup"><span data-stu-id="0a0da-177">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="0a0da-178">Отправляется на ваш робот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="0a0da-178">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="0a0da-179">Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="0a0da-179">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="0a0da-180">Отправляется на ваш робот при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="0a0da-180">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="0a0da-181">Используйте это свойство для упрощения разработки в Bot: ваш код может проверять одно свойство верхнего уровня для обработки логики Bot.</span><span class="sxs-lookup"><span data-stu-id="0a0da-181">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="0a0da-182">Пример</span><span class="sxs-lookup"><span data-stu-id="0a0da-182">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="0a0da-183">Адаптивные карты с действием при обратной передаче</span><span class="sxs-lookup"><span data-stu-id="0a0da-183">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="0a0da-184">Чтобы включить `imBack` действие с помощью адаптивной карточки, добавьте следующие сведения в `msteams` объект.</span><span class="sxs-lookup"><span data-stu-id="0a0da-184">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="0a0da-185">Обратите внимание, что при необходимости вы можете добавить `data` в объект дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="0a0da-185">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="0a0da-186">Свойство</span><span class="sxs-lookup"><span data-stu-id="0a0da-186">Property</span></span> | <span data-ttu-id="0a0da-187">Описание</span><span class="sxs-lookup"><span data-stu-id="0a0da-187">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="0a0da-188">Значение`imBack`</span><span class="sxs-lookup"><span data-stu-id="0a0da-188">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="0a0da-189">Строка, которая должна быть возвращена в чате</span><span class="sxs-lookup"><span data-stu-id="0a0da-189">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="0a0da-190">Пример</span><span class="sxs-lookup"><span data-stu-id="0a0da-190">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="0a0da-191">Адаптивные карточки с действием SignIn</span><span class="sxs-lookup"><span data-stu-id="0a0da-191">Adaptive Cards with signin action</span></span>

<span data-ttu-id="0a0da-192">Чтобы включить `signin` действие с помощью адаптивной карточки, добавьте следующие сведения в `msteams` объект.</span><span class="sxs-lookup"><span data-stu-id="0a0da-192">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="0a0da-193">Обратите внимание, что при необходимости вы можете добавить `data` в объект дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="0a0da-193">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="0a0da-194">Свойство</span><span class="sxs-lookup"><span data-stu-id="0a0da-194">Property</span></span> | <span data-ttu-id="0a0da-195">Описание</span><span class="sxs-lookup"><span data-stu-id="0a0da-195">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="0a0da-196">Значение`signin`</span><span class="sxs-lookup"><span data-stu-id="0a0da-196">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="0a0da-197">Укажите URL-адрес, на который требуется перенаправить</span><span class="sxs-lookup"><span data-stu-id="0a0da-197">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="0a0da-198">Пример</span><span class="sxs-lookup"><span data-stu-id="0a0da-198">Example</span></span>

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