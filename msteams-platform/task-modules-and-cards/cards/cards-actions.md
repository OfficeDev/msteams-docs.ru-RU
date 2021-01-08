---
title: Добавление действий карточки в бота
description: Описание действий карт в Microsoft Teams и их использования в ботах
keywords: действия карточек ботов teams
ms.openlocfilehash: 2bee1072405d91cd29d1aa227884516a87d10bde
ms.sourcegitcommit: b9771f8f4be9ac1ff8c85c2d7bd8d5c5408bc653
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "49768076"
---
# <a name="card-actions"></a><span data-ttu-id="bc6d7-104">Действия с карточками</span><span class="sxs-lookup"><span data-stu-id="bc6d7-104">Card actions</span></span>

<span data-ttu-id="bc6d7-105">Карточки, используемые ботами и расширениями обмена сообщениями в Teams, поддерживают следующие типы действий ( [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ).</span><span class="sxs-lookup"><span data-stu-id="bc6d7-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="bc6d7-106">Обратите внимание, что эти действия отличаются от действий для карт соединители `potentialActions` Office 365 при их использования.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="bc6d7-107">Тип</span><span class="sxs-lookup"><span data-stu-id="bc6d7-107">Type</span></span> | <span data-ttu-id="bc6d7-108">Действие</span><span class="sxs-lookup"><span data-stu-id="bc6d7-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="bc6d7-109">Открывает URL-адрес в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="bc6d7-110">Отправляет сообщение и полезное сообщение боту (от пользователя, нажавшего кнопку или нажавшего карточку) и отправляет отдельное сообщение в поток чата.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="bc6d7-111">Отправляет сообщение боту (от пользователя, нажавшего кнопку или нажавшего карточку).</span><span class="sxs-lookup"><span data-stu-id="bc6d7-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="bc6d7-112">Это сообщение (от пользователя к боту) отображается всем участникам беседы.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="bc6d7-113">Отправляет сообщение и полезное сообщение боту (от пользователя, нажавшего кнопку или нажавшего карточку).</span><span class="sxs-lookup"><span data-stu-id="bc6d7-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="bc6d7-114">Это сообщение не отображается.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="bc6d7-115">Инициирует поток OAuth, позволяя ботам подключаться к защищенным службам.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="bc6d7-116">Teams не поддерживает `CardAction` типы, не указанные в предыдущей таблице.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="bc6d7-117">Teams не поддерживает `potentialActions` свойство.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="bc6d7-118">Действия с карточками отличаются [от предлагаемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в Bot Framework или службе ботов Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="bc6d7-119">Рекомендуемые действия не поддерживаются в Microsoft Teams: если вы хотите, чтобы кнопки появлялись в сообщении бота Teams, используйте карточку.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="bc6d7-120">Если вы используете действие карточки в составе расширения обмена сообщениями, действия не будут работать, пока карточка не будет отправлена в канал (они не будут работать, пока карточка находится в окне сообщения составить).</span><span class="sxs-lookup"><span data-stu-id="bc6d7-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="bc6d7-121">Teams также поддерживает [действия адаптивных карточек,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)которые используются только адаптивными карточками.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="bc6d7-122">Эти действия перечислены в собственном разделе в конце этой ссылки.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="bc6d7-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="bc6d7-123">openUrl</span></span>

<span data-ttu-id="bc6d7-124">Этот тип действия указывает URL-адрес для запуска в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="bc6d7-125">Обратите внимание, что бот не получает уведомления о нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="bc6d7-126">Поле должно содержать полный и `value` правильно сформированный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="bc6d7-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="bc6d7-127">messageBack</span></span>

<span data-ttu-id="bc6d7-128">С помощью этого параметра можно `messageBack` создать полностью настроенную действие со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="bc6d7-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="bc6d7-129">Свойство</span><span class="sxs-lookup"><span data-stu-id="bc6d7-129">Property</span></span> | <span data-ttu-id="bc6d7-130">Описание</span><span class="sxs-lookup"><span data-stu-id="bc6d7-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="bc6d7-131">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="bc6d7-132">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-132">Optional.</span></span> <span data-ttu-id="bc6d7-133">Эхо от пользователя в потоке чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="bc6d7-134">Этот текст не *отправляется* вашему боту.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="bc6d7-135">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="bc6d7-136">Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="bc6d7-137">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="bc6d7-138">Используйте это свойство для упрощения разработки ботов: код может проверять одно свойство верхнего уровня для отправки логики бота.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="bc6d7-139">Гибкость означает, что код может не оставлять видимое сообщение пользователя в истории, `messageBack` просто не используя `displayText` .</span><span class="sxs-lookup"><span data-stu-id="bc6d7-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="bc6d7-140">Свойство `value` может быть сериализованной строкой JSON или объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="bc6d7-141">Пример входящие сообщения</span><span class="sxs-lookup"><span data-stu-id="bc6d7-141">Inbound message example</span></span>

<span data-ttu-id="bc6d7-142">`replyToId` содержит ИД сообщения, из которое поступило действие карточки.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="bc6d7-143">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="bc6d7-144">imBack</span><span class="sxs-lookup"><span data-stu-id="bc6d7-144">imBack</span></span>

<span data-ttu-id="bc6d7-145">Это действие инициирует возврат сообщения боту, как если бы пользователь ввести его в обычном сообщении чата.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="bc6d7-146">Ваш пользователь и все остальные пользователи, если они есть в канале, увидят этот ответ кнопки.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="bc6d7-147">Поле должно содержать текстовую строку, которая эхом повторяется в чате и, следовательно, `value` отправляется боту.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="bc6d7-148">Это текст сообщения, который будет обрабатываться в боте для выполнения нужной логики.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="bc6d7-149">Примечание. Это поле является простой строкой. Форматирование или скрытые символы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="bc6d7-150">invoke</span><span class="sxs-lookup"><span data-stu-id="bc6d7-150">invoke</span></span>

<span data-ttu-id="bc6d7-151">Это `invoke` действие используется для вызова [модулей задач.](~/task-modules-and-cards/task-modules/task-modules-bots.md)</span><span class="sxs-lookup"><span data-stu-id="bc6d7-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="bc6d7-152">Действие `invoke` содержит три свойства: , и `type` `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="bc6d7-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="bc6d7-153">Свойство `value` может содержать строку, строковый объект JSON или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="bc6d7-154">Когда пользователь нажимает кнопку, бот получает `value` объект с дополнительной информацией.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="bc6d7-155">Обратите внимание, что тип действия будет вместо `invoke` `message` ( `activity.Type == "invoke"` ).</span><span class="sxs-lookup"><span data-stu-id="bc6d7-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="bc6d7-156">Пример: определение кнопки вызова (.NET)</span><span class="sxs-lookup"><span data-stu-id="bc6d7-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="bc6d7-157">Пример: входящий вызов сообщения</span><span class="sxs-lookup"><span data-stu-id="bc6d7-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="bc6d7-158">Свойство верхнего уровня содержит ИД сообщения, от которое `replyToId` поступило действие карточки.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="bc6d7-159">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="bc6d7-160">signin</span><span class="sxs-lookup"><span data-stu-id="bc6d7-160">signin</span></span>

<span data-ttu-id="bc6d7-161">Инициирует поток OAuth, позволяя ботам подключаться к защищенным службам, как описано ниже: поток проверки подлинности [в ботах.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="bc6d7-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="bc6d7-162">Действия адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="bc6d7-162">Adaptive Cards actions</span></span>

<span data-ttu-id="bc6d7-163">Адаптивные карточки поддерживают три типа действий:</span><span class="sxs-lookup"><span data-stu-id="bc6d7-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="bc6d7-164">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="bc6d7-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="bc6d7-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="bc6d7-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="bc6d7-166">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="bc6d7-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="bc6d7-167">В дополнение к вышеперечисленным действиям можно изменить полезной нагрузки адаптивной карточки для поддержки существующих действий Bot Framework с помощью свойства `Action.Submit` `msteams` в `data` объекте `Action.Submit` .</span><span class="sxs-lookup"><span data-stu-id="bc6d7-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="bc6d7-168">В разделах ниже подробно поется, как использовать существующие действия Bot Framework с адаптивными карточками.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="bc6d7-169">Добавление данных с помощью действия Bot Framework не работает с модулем задачи `msteams` адаптивной карточки.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-169">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="bc6d7-170">Адаптивные карточки с действием messageBack</span><span class="sxs-lookup"><span data-stu-id="bc6d7-170">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="bc6d7-171">Чтобы включить действие `messageBack` с адаптивной карточкой, включаем в объект следующие `msteams` сведения.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-171">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="bc6d7-172">Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-172">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="bc6d7-173">Свойство</span><span class="sxs-lookup"><span data-stu-id="bc6d7-173">Property</span></span> | <span data-ttu-id="bc6d7-174">Описание</span><span class="sxs-lookup"><span data-stu-id="bc6d7-174">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="bc6d7-175">За установлено `messageBack`</span><span class="sxs-lookup"><span data-stu-id="bc6d7-175">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="bc6d7-176">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-176">Optional.</span></span> <span data-ttu-id="bc6d7-177">Эхо от пользователя в потоке чата при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-177">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="bc6d7-178">Этот текст не *отправляется* вашему боту.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-178">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="bc6d7-179">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-179">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="bc6d7-180">Вы можете закодировать контекст для действия, например уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-180">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="bc6d7-181">Отправляется боту при выполнении действия.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-181">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="bc6d7-182">Используйте это свойство для упрощения разработки ботов: код может проверять одно свойство верхнего уровня для отправки логики бота.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-182">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="bc6d7-183">Пример</span><span class="sxs-lookup"><span data-stu-id="bc6d7-183">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="bc6d7-184">Адаптивные карточки с действием imBack</span><span class="sxs-lookup"><span data-stu-id="bc6d7-184">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="bc6d7-185">Чтобы включить действие `imBack` с адаптивной карточкой, включаем в объект следующие `msteams` сведения.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-185">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="bc6d7-186">Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-186">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="bc6d7-187">Свойство</span><span class="sxs-lookup"><span data-stu-id="bc6d7-187">Property</span></span> | <span data-ttu-id="bc6d7-188">Описание</span><span class="sxs-lookup"><span data-stu-id="bc6d7-188">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="bc6d7-189">За установлено `imBack`</span><span class="sxs-lookup"><span data-stu-id="bc6d7-189">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="bc6d7-190">Строка, которая должна быть повторяема в чате</span><span class="sxs-lookup"><span data-stu-id="bc6d7-190">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="bc6d7-191">Пример</span><span class="sxs-lookup"><span data-stu-id="bc6d7-191">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="bc6d7-192">Адаптивные карточки с действием для регистрации</span><span class="sxs-lookup"><span data-stu-id="bc6d7-192">Adaptive Cards with signin action</span></span>

<span data-ttu-id="bc6d7-193">Чтобы включить действие `signin` с адаптивной карточкой, включаем в объект следующие `msteams` сведения.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-193">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="bc6d7-194">Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-194">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="bc6d7-195">Свойство</span><span class="sxs-lookup"><span data-stu-id="bc6d7-195">Property</span></span> | <span data-ttu-id="bc6d7-196">Описание</span><span class="sxs-lookup"><span data-stu-id="bc6d7-196">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="bc6d7-197">За установлено `signin`</span><span class="sxs-lookup"><span data-stu-id="bc6d7-197">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="bc6d7-198">Установите URL-адрес, на который нужно перенаправить</span><span class="sxs-lookup"><span data-stu-id="bc6d7-198">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="bc6d7-199">Пример</span><span class="sxs-lookup"><span data-stu-id="bc6d7-199">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="bc6d7-200">Адаптивные карточки с действием вызова</span><span class="sxs-lookup"><span data-stu-id="bc6d7-200">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="bc6d7-201">Чтобы включить действие `invoke` с адаптивной карточкой, включаем в объект следующие `msteams` сведения.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-201">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="bc6d7-202">Обратите внимание, что при необходимости в объект можно включить дополнительные `data` скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="bc6d7-202">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="bc6d7-203">Свойство</span><span class="sxs-lookup"><span data-stu-id="bc6d7-203">Property</span></span> | <span data-ttu-id="bc6d7-204">Описание</span><span class="sxs-lookup"><span data-stu-id="bc6d7-204">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="bc6d7-205">За установлено `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="bc6d7-205">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="bc6d7-206">Установить значение</span><span class="sxs-lookup"><span data-stu-id="bc6d7-206">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="bc6d7-207">Пример</span><span class="sxs-lookup"><span data-stu-id="bc6d7-207">Example</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="bc6d7-208">Пример 2 (с дополнительными данными полезной нагрузки)</span><span class="sxs-lookup"><span data-stu-id="bc6d7-208">Example 2 (with additional payload data)</span></span>

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
