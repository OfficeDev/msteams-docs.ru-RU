---
title: Добавление действий карты в бота
description: Описывает действия карты в Microsoft Teams и как их использовать в ботах
localization_priority: Normal
ms.topic: conceptual
keywords: команды ботов карты действия
ms.openlocfilehash: b9276c7197070df43ba447707e6fa4d3d4098591
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566854"
---
# <a name="card-actions"></a><span data-ttu-id="18708-104">Действия карты</span><span class="sxs-lookup"><span data-stu-id="18708-104">Card actions</span></span>

<span data-ttu-id="18708-105">Карты, используемые ботами и расширениями обмена сообщениями Teams для поддержки следующих типов [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) активности () .</span><span class="sxs-lookup"><span data-stu-id="18708-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="18708-106">Обратите внимание, что эти действия `potentialActions` отличаются от Office 365 connector при использовании из Connectors.</span><span class="sxs-lookup"><span data-stu-id="18708-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="18708-107">Тип</span><span class="sxs-lookup"><span data-stu-id="18708-107">Type</span></span> | <span data-ttu-id="18708-108">Действие</span><span class="sxs-lookup"><span data-stu-id="18708-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="18708-109">Открывает URL-адрес в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="18708-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="18708-110">Отправляет сообщение и полезную нагрузку боту от пользователя, который нажал на кнопку или нажал на карту и отправил отдельное сообщение в поток чата.</span><span class="sxs-lookup"><span data-stu-id="18708-110">Sends a message and payload to the bot from the user who clicked the button or tapped the card and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="18708-111">Отправляет сообщение боту от пользователя, который нажал на кнопку или нажал на карту.</span><span class="sxs-lookup"><span data-stu-id="18708-111">Sends a message to the bot from the user who clicked the button or tapped the card.</span></span> <span data-ttu-id="18708-112">Это сообщение (от пользователя к боту) видно всем участникам беседы.</span><span class="sxs-lookup"><span data-stu-id="18708-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="18708-113">Отправляет сообщение и полезную нагрузку боту от пользователя, который нажал на кнопку или нажал на карту.</span><span class="sxs-lookup"><span data-stu-id="18708-113">Sends a message and payload to the bot from the user who clicked the button or tapped the card.</span></span> <span data-ttu-id="18708-114">Это сообщение не видно.</span><span class="sxs-lookup"><span data-stu-id="18708-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="18708-115">Инициирует поток OAuth, позволяя ботам подключаться к безопасным службам.</span><span class="sxs-lookup"><span data-stu-id="18708-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="18708-116">Teams не поддерживает `CardAction` типы, не перечисленные в предыдущей таблице.</span><span class="sxs-lookup"><span data-stu-id="18708-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="18708-117">Teams не поддерживает `potentialActions` свойство.</span><span class="sxs-lookup"><span data-stu-id="18708-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="18708-118">Действия карты отличаются от [предлагаемых действий](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) в службе Bot Framework/Azure Bot.</span><span class="sxs-lookup"><span data-stu-id="18708-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="18708-119">Предлагаемые действия не поддерживаются в Microsoft Teams: если вы хотите, чтобы кнопки Teams сообщении бота, используйте карту.</span><span class="sxs-lookup"><span data-stu-id="18708-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="18708-120">Если вы используете действие карты в рамках расширения обмена сообщениями, действия не работают до тех пор, пока карта не будет отправлена каналу.</span><span class="sxs-lookup"><span data-stu-id="18708-120">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="18708-121">Они не работают, пока карта находится в поле для составления сообщений.</span><span class="sxs-lookup"><span data-stu-id="18708-121">They do not work while the card is in the compose message box.</span></span>

<span data-ttu-id="18708-122">Teams поддерживает действия [Adaptive Cards,](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)которые используются только адаптивными картами.</span><span class="sxs-lookup"><span data-stu-id="18708-122">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="18708-123">Эти действия перечислены в их собственном разделе в конце этой ссылки.</span><span class="sxs-lookup"><span data-stu-id="18708-123">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="18708-124">openUrl</span><span class="sxs-lookup"><span data-stu-id="18708-124">openUrl</span></span>

<span data-ttu-id="18708-125">Этот тип действия определяет URL для запуска в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="18708-125">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="18708-126">Обратите внимание, что ваш бот не получает никакого уведомления о том, какая кнопка была нажата.</span><span class="sxs-lookup"><span data-stu-id="18708-126">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="18708-127">Поле `value` должно содержать полный и правильно сформированный URL.</span><span class="sxs-lookup"><span data-stu-id="18708-127">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="18708-128">messageBack</span><span class="sxs-lookup"><span data-stu-id="18708-128">messageBack</span></span>

<span data-ttu-id="18708-129">С `messageBack` помощью, вы можете создать полностью настроенные действия со следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="18708-129">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="18708-130">Свойство</span><span class="sxs-lookup"><span data-stu-id="18708-130">Property</span></span> | <span data-ttu-id="18708-131">Описание</span><span class="sxs-lookup"><span data-stu-id="18708-131">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="18708-132">Отображается как метка кнопки.</span><span class="sxs-lookup"><span data-stu-id="18708-132">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="18708-133">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="18708-133">Optional.</span></span> <span data-ttu-id="18708-134">Вторит пользователю в поток чата, когда действие выполняется.</span><span class="sxs-lookup"><span data-stu-id="18708-134">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="18708-135">Этот текст не *отправляется* вашему боту.</span><span class="sxs-lookup"><span data-stu-id="18708-135">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="18708-136">Отправлено вашему боту, когда действие выполняется.</span><span class="sxs-lookup"><span data-stu-id="18708-136">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="18708-137">Контекст для действия можно кодировать, например, уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="18708-137">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="18708-138">Отправлено вашему боту, когда действие выполняется.</span><span class="sxs-lookup"><span data-stu-id="18708-138">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="18708-139">Используйте это свойство для упрощения разработки бота: ваш код может проверить одно свойство верхнего уровня для отправки логики бота.</span><span class="sxs-lookup"><span data-stu-id="18708-139">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="18708-140">Гибкость средств, `messageBack` которые ваш код может выбрать, чтобы не оставлять видимое сообщение пользователя в истории, просто не используя `displayText` .</span><span class="sxs-lookup"><span data-stu-id="18708-140">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="18708-141">Свойство `value` может быть либо сериализованной строкой JSON, либо объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="18708-141">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="18708-142">Пример входящих сообщений</span><span class="sxs-lookup"><span data-stu-id="18708-142">Inbound message example</span></span>

<span data-ttu-id="18708-143">`replyToId` содержит идентификатор сообщения, от которого пришло действие карты.</span><span class="sxs-lookup"><span data-stu-id="18708-143">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="18708-144">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="18708-144">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="18708-145">imBack</span><span class="sxs-lookup"><span data-stu-id="18708-145">imBack</span></span>

<span data-ttu-id="18708-146">Это действие запускает возврат сообщения для вашего бота, как если бы пользователь набрал его в обычном сообщении чата.</span><span class="sxs-lookup"><span data-stu-id="18708-146">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="18708-147">Ваш пользователь, и все другие пользователи, если в канале, увидите, что кнопка ответа.</span><span class="sxs-lookup"><span data-stu-id="18708-147">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="18708-148">Поле `value` должно содержать текстовую строку, вторя в чате, и поэтому отправлено обратно боту.</span><span class="sxs-lookup"><span data-stu-id="18708-148">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="18708-149">Это текст сообщения, который вы обработать в вашем боте для выполнения желаемой логики.</span><span class="sxs-lookup"><span data-stu-id="18708-149">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="18708-150">Примечание: это поле является простой строкой - нет поддержки для форматирования или скрытых символов.</span><span class="sxs-lookup"><span data-stu-id="18708-150">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="18708-151">взывать</span><span class="sxs-lookup"><span data-stu-id="18708-151">invoke</span></span>

<span data-ttu-id="18708-152">Действие `invoke` используется для вызова [модулей задач.](~/task-modules-and-cards/task-modules/task-modules-bots.md)</span><span class="sxs-lookup"><span data-stu-id="18708-152">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="18708-153">Действие `invoke` содержит три свойства: , и `type` `title` `value` .</span><span class="sxs-lookup"><span data-stu-id="18708-153">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="18708-154">Свойство `value` может содержать строку, струнный объект JSON или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="18708-154">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="18708-155">Когда пользователь нажимает на кнопку, ваш бот получит объект с `value` некоторой дополнительной информацией.</span><span class="sxs-lookup"><span data-stu-id="18708-155">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="18708-156">Пожалуйста, обратите внимание, что тип действия `invoke` будет вместо `message` ( `activity.Type == "invoke"` ).</span><span class="sxs-lookup"><span data-stu-id="18708-156">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="18708-157">Пример: Определение кнопки вызова (.NET)</span><span class="sxs-lookup"><span data-stu-id="18708-157">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="18708-158">Пример: Входящее сообщение вызова</span><span class="sxs-lookup"><span data-stu-id="18708-158">Example: Incoming invoke message</span></span>

<span data-ttu-id="18708-159">Свойство верхнего `replyToId` уровня содержит идентификатор сообщения, откуда пришло действие карты.</span><span class="sxs-lookup"><span data-stu-id="18708-159">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="18708-160">Используйте его, если вы хотите обновить сообщение.</span><span class="sxs-lookup"><span data-stu-id="18708-160">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="18708-161">signin</span><span class="sxs-lookup"><span data-stu-id="18708-161">signin</span></span>

<span data-ttu-id="18708-162">Инициирует поток OAuth, позволяя ботам связаться с безопасными службами, как описано более подробно здесь: [Поток аутентификации в ботах.](~/bots/how-to/authentication/auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="18708-162">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="18708-163">Действия адаптивных карт</span><span class="sxs-lookup"><span data-stu-id="18708-163">Adaptive Cards actions</span></span>

<span data-ttu-id="18708-164">Адаптивные карты поддерживают четыре типа действий:</span><span class="sxs-lookup"><span data-stu-id="18708-164">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="18708-165">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="18708-165">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="18708-166">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="18708-166">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="18708-167">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="18708-167">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="18708-168">Action.Exeмило</span><span class="sxs-lookup"><span data-stu-id="18708-168">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="18708-169">В дополнение к действиям, упомянутым выше, вы можете изменить полезную нагрузку Adaptive Card `Action.Submit` для поддержки существующих действий Bot `msteams` Framework, используя `data` свойство в `Action.Submit` объекте.</span><span class="sxs-lookup"><span data-stu-id="18708-169">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="18708-170">В нижесемейных разделах подробно описано, как использовать существующие действия Bot Framework с помощью адаптивных карт.</span><span class="sxs-lookup"><span data-stu-id="18708-170">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="18708-171">Добавление `msteams` к данным с действием Bot Framework не работает с модулем задач Adaptive Card.</span><span class="sxs-lookup"><span data-stu-id="18708-171">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="18708-172">Адаптивные карты с действием messageBack</span><span class="sxs-lookup"><span data-stu-id="18708-172">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="18708-173">Чтобы включить действие `messageBack` с адаптивной картой, включите в объект следующие `msteams` детали.</span><span class="sxs-lookup"><span data-stu-id="18708-173">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="18708-174">Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="18708-174">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="18708-175">Свойство</span><span class="sxs-lookup"><span data-stu-id="18708-175">Property</span></span> | <span data-ttu-id="18708-176">Описание</span><span class="sxs-lookup"><span data-stu-id="18708-176">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="18708-177">Установить для `messageBack`</span><span class="sxs-lookup"><span data-stu-id="18708-177">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="18708-178">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="18708-178">Optional.</span></span> <span data-ttu-id="18708-179">Вторит пользователю в поток чата, когда действие выполняется.</span><span class="sxs-lookup"><span data-stu-id="18708-179">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="18708-180">Этот текст не *отправляется* вашему боту.</span><span class="sxs-lookup"><span data-stu-id="18708-180">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="18708-181">Отправлено вашему боту, когда действие выполняется.</span><span class="sxs-lookup"><span data-stu-id="18708-181">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="18708-182">Контекст для действия можно кодировать, например, уникальные идентификаторы или объект JSON.</span><span class="sxs-lookup"><span data-stu-id="18708-182">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="18708-183">Отправлено вашему боту, когда действие выполняется.</span><span class="sxs-lookup"><span data-stu-id="18708-183">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="18708-184">Используйте это свойство для упрощения разработки бота: ваш код может проверить одно свойство верхнего уровня для отправки логики бота.</span><span class="sxs-lookup"><span data-stu-id="18708-184">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="18708-185">Пример</span><span class="sxs-lookup"><span data-stu-id="18708-185">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="18708-186">Адаптивные карты с действием imBack</span><span class="sxs-lookup"><span data-stu-id="18708-186">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="18708-187">Чтобы включить действие `imBack` с адаптивной картой, включите в объект следующие `msteams` детали.</span><span class="sxs-lookup"><span data-stu-id="18708-187">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="18708-188">Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="18708-188">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="18708-189">Свойство</span><span class="sxs-lookup"><span data-stu-id="18708-189">Property</span></span> | <span data-ttu-id="18708-190">Описание</span><span class="sxs-lookup"><span data-stu-id="18708-190">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="18708-191">Установить для `imBack`</span><span class="sxs-lookup"><span data-stu-id="18708-191">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="18708-192">Строка, которая должна быть повторена обратно в чате</span><span class="sxs-lookup"><span data-stu-id="18708-192">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="18708-193">Пример</span><span class="sxs-lookup"><span data-stu-id="18708-193">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="18708-194">Адаптивные карты с сигнином действий</span><span class="sxs-lookup"><span data-stu-id="18708-194">Adaptive Cards with signin action</span></span>

<span data-ttu-id="18708-195">Чтобы включить действие `signin` с адаптивной картой, включите в объект следующие `msteams` детали.</span><span class="sxs-lookup"><span data-stu-id="18708-195">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="18708-196">Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="18708-196">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="18708-197">Свойство</span><span class="sxs-lookup"><span data-stu-id="18708-197">Property</span></span> | <span data-ttu-id="18708-198">Описание</span><span class="sxs-lookup"><span data-stu-id="18708-198">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="18708-199">Установить на `signin` .</span><span class="sxs-lookup"><span data-stu-id="18708-199">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="18708-200">Установите URL-адрес, на который вы хотите перенаправить.</span><span class="sxs-lookup"><span data-stu-id="18708-200">Set to the URL that you want to redirect to.</span></span>  |

#### <a name="example"></a><span data-ttu-id="18708-201">Пример</span><span class="sxs-lookup"><span data-stu-id="18708-201">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="18708-202">Адаптивные карты с действием вызова</span><span class="sxs-lookup"><span data-stu-id="18708-202">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="18708-203">Чтобы включить действие `invoke` с адаптивной картой, включите в объект следующие `msteams` детали.</span><span class="sxs-lookup"><span data-stu-id="18708-203">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="18708-204">Обратите внимание, что при необходимости в объект могут быть включены `data` дополнительные скрытые свойства.</span><span class="sxs-lookup"><span data-stu-id="18708-204">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="18708-205">Свойство</span><span class="sxs-lookup"><span data-stu-id="18708-205">Property</span></span> | <span data-ttu-id="18708-206">Описание</span><span class="sxs-lookup"><span data-stu-id="18708-206">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="18708-207">Установить для `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="18708-207">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="18708-208">Установить значение</span><span class="sxs-lookup"><span data-stu-id="18708-208">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="18708-209">Пример</span><span class="sxs-lookup"><span data-stu-id="18708-209">Example</span></span>

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

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="18708-210">Пример 2 (с дополнительными данными полезной нагрузки)</span><span class="sxs-lookup"><span data-stu-id="18708-210">Example 2 (with additional payload data)</span></span>

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
