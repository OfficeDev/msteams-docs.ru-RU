---
title: Основы разговора
author: clearab
description: Беседа с ботом Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f7e7a4d1be08126c96dff07ddbc3e1156700a90
ms.sourcegitcommit: 94ad961ecd002805b4e0424601d1c0ec191ff376
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2021
ms.locfileid: "50075695"
---
# <a name="conversation-basics"></a><span data-ttu-id="6eaa7-103">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="6eaa7-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="6eaa7-104">Беседа — это серия сообщений, отправленных между ботом и одним или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="6eaa7-105">Существует три типа бесед (также называемых областью) в Teams:</span><span class="sxs-lookup"><span data-stu-id="6eaa7-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="6eaa7-106">`teams` Также называется беседами канала, которые видны всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="6eaa7-107">`personal` Беседы между ботами и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="6eaa7-108">`groupChat` Чат между ботом и двумя или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="6eaa7-109">Также включает бота в чатах собраний.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="6eaa7-110">Бот ведет себя немного по-разному в зависимости от типа беседы, в которых он участвует:</span><span class="sxs-lookup"><span data-stu-id="6eaa7-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="6eaa7-111">Боты в беседах в канале и групповом чате требуют от пользователя @упоминания бота, чтобы вызвать его в канале.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="6eaa7-112">Боты в беседе "один к одному" не требуют @упоминания.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="6eaa7-113">Все сообщения, отправленные пользователем, будут направлены вашему боту.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="6eaa7-114">Чтобы включить бота в определенной области, добавьте эту область в манифест [приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="6eaa7-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="6eaa7-115">Действия</span><span class="sxs-lookup"><span data-stu-id="6eaa7-115">Activities</span></span>

<span data-ttu-id="6eaa7-116">Каждое сообщение является `Activity` объектом типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="6eaa7-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="6eaa7-117">Когда пользователь отправляет сообщение, Teams отправляет его вашему боту; В частности, он отправляет объект JSON в конечную точку обмена сообщениями бота.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="6eaa7-118">Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="6eaa7-119">Базовая беседа обрабатывается через соединители Bot Framework, один API REST, позволяющий боту взаимодействовать с Teams и другими каналами.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="6eaa7-120">SDK построитель ботов предоставляет простой доступ к этому API, дополнительные функции для управления потоком беседы и состоянием, а также простые способы включения функций распознавания, таких как обработка естественного языка (NLP).</span><span class="sxs-lookup"><span data-stu-id="6eaa7-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="6eaa7-121">Получение сообщения</span><span class="sxs-lookup"><span data-stu-id="6eaa7-121">Receive a message</span></span>

<span data-ttu-id="6eaa7-122">Чтобы получить текстовое сообщение, используйте `Text` свойство `Activity` объекта.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="6eaa7-123">В обработнике действий бота используйте объект контекста turn для чтения `Activity` одного запроса сообщения.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="6eaa7-124">Ниже приведен пример кода.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6eaa7-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6eaa7-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6eaa7-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6eaa7-126">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[<span data-ttu-id="6eaa7-127">Python</span><span class="sxs-lookup"><span data-stu-id="6eaa7-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="6eaa7-128">JSON</span><span class="sxs-lookup"><span data-stu-id="6eaa7-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a><span data-ttu-id="6eaa7-129">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="6eaa7-129">Send a message</span></span>

<span data-ttu-id="6eaa7-130">Чтобы отправить текстовое сообщение, укажите строку, отправляемую в качестве действия.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="6eaa7-131">В обработчике действий бота используйте метод объекта контекста turn для отправки `SendActivityAsync` одного ответа на сообщение.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="6eaa7-132">Вы также можете использовать метод объекта `SendActivitiesAsync` для отправки нескольких ответов одновременно.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="6eaa7-133">В приведенном ниже коде показан пример отправки сообщения при добавлении кого-либо в беседу</span><span class="sxs-lookup"><span data-stu-id="6eaa7-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="6eaa7-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6eaa7-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6eaa7-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6eaa7-135">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="6eaa7-136">Python</span><span class="sxs-lookup"><span data-stu-id="6eaa7-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="6eaa7-137">JSON</span><span class="sxs-lookup"><span data-stu-id="6eaa7-137">JSON</span></span>](#tab/json)

```json
{
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
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
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="teams-channel-data"></a><span data-ttu-id="6eaa7-138">Данные канала Teams</span><span class="sxs-lookup"><span data-stu-id="6eaa7-138">Teams channel data</span></span>

<span data-ttu-id="6eaa7-139">Объект `channelData` содержит сведения, специфичная для Teams, и является окончательным источником для кодов команды и канала.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="6eaa7-140">Возможно, потребуется кэширования и использовать эти ids в качестве ключей для локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="6eaa7-141">Как правило, SDK извлекет важные сведения из объекта, чтобы сделать его более доступным, однако вы всегда можете получить доступ к исходной информации `TeamsActivityHandler` `channelData` из `turnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="6eaa7-142">Объект не включается в сообщения в личных беседах, так как они проходят `channelData` за пределами любого канала.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="6eaa7-143">Типичный объект channelData в действии, отправленный вашему боту, содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="6eaa7-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="6eaa7-144">`eventType` Тип события Teams; передается только в случае событий [изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="6eaa7-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="6eaa7-145">`tenant.id` ИД клиента Azure Active Directory; передается во всех контекстах</span><span class="sxs-lookup"><span data-stu-id="6eaa7-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="6eaa7-146">`team` Передается только в контекстах канала, а не в личном чате.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="6eaa7-147">`id` GUID для канала</span><span class="sxs-lookup"><span data-stu-id="6eaa7-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="6eaa7-148">`name` Имя команды; передается только в случае [переименования команд](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="6eaa7-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="6eaa7-149">`channel` Передается только в контекстах канала, когда упоминается бот, или для событий в каналах в командах, в которые был добавлен бот</span><span class="sxs-lookup"><span data-stu-id="6eaa7-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="6eaa7-150">`id` GUID для канала</span><span class="sxs-lookup"><span data-stu-id="6eaa7-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="6eaa7-151">`name`Имя канала; передается только в случае событий [изменения канала.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="6eaa7-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="6eaa7-152">`channelData.teamsTeamId` Неподготовлено.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="6eaa7-153">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="6eaa7-154">`channelData.teamsChannelId` Неподготовлено.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="6eaa7-155">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="6eaa7-156">Пример объекта channelData (событие channelCreated)</span><span class="sxs-lookup"><span data-stu-id="6eaa7-156">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## <a name="message-content"></a><span data-ttu-id="6eaa7-157">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="6eaa7-157">Message content</span></span>

<span data-ttu-id="6eaa7-158">Бот может отправлять текст, изображения и карточки.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="6eaa7-159">Пользователи могут отправлять вашему боту текст и изображения.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="6eaa7-160">Format</span><span class="sxs-lookup"><span data-stu-id="6eaa7-160">Format</span></span>    | <span data-ttu-id="6eaa7-161">От пользователя к боту</span><span class="sxs-lookup"><span data-stu-id="6eaa7-161">From user to bot</span></span> | <span data-ttu-id="6eaa7-162">От бота к пользователю</span><span class="sxs-lookup"><span data-stu-id="6eaa7-162">From bot to user</span></span> | <span data-ttu-id="6eaa7-163">Примечания</span><span class="sxs-lookup"><span data-stu-id="6eaa7-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="6eaa7-164">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="6eaa7-164">Rich text</span></span> | <span data-ttu-id="6eaa7-165">✔</span><span class="sxs-lookup"><span data-stu-id="6eaa7-165">✔</span></span>                | <span data-ttu-id="6eaa7-166">✔</span><span class="sxs-lookup"><span data-stu-id="6eaa7-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="6eaa7-167">Изображения</span><span class="sxs-lookup"><span data-stu-id="6eaa7-167">Pictures</span></span>  | <span data-ttu-id="6eaa7-168">✔</span><span class="sxs-lookup"><span data-stu-id="6eaa7-168">✔</span></span>                | <span data-ttu-id="6eaa7-169">✔</span><span class="sxs-lookup"><span data-stu-id="6eaa7-169">✔</span></span>                | <span data-ttu-id="6eaa7-170">Не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается</span><span class="sxs-lookup"><span data-stu-id="6eaa7-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="6eaa7-171">Карточки</span><span class="sxs-lookup"><span data-stu-id="6eaa7-171">Cards</span></span>     | <span data-ttu-id="6eaa7-172">✖</span><span class="sxs-lookup"><span data-stu-id="6eaa7-172">✖</span></span>                | <span data-ttu-id="6eaa7-173">✔</span><span class="sxs-lookup"><span data-stu-id="6eaa7-173">✔</span></span>                | <span data-ttu-id="6eaa7-174">См. справочник [по карточкам Teams для](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемых карточек</span><span class="sxs-lookup"><span data-stu-id="6eaa7-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="6eaa7-175">Emojis</span><span class="sxs-lookup"><span data-stu-id="6eaa7-175">Emojis</span></span>    | <span data-ttu-id="6eaa7-176">✖</span><span class="sxs-lookup"><span data-stu-id="6eaa7-176">✖</span></span>                | <span data-ttu-id="6eaa7-177">✔</span><span class="sxs-lookup"><span data-stu-id="6eaa7-177">✔</span></span>                | <span data-ttu-id="6eaa7-178">В настоящее время Teams поддерживает эмодзи через UTF-16 (например, U+1F600 для ухмылки)</span><span class="sxs-lookup"><span data-stu-id="6eaa7-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="6eaa7-179">Добавление уведомлений в сообщение</span><span class="sxs-lookup"><span data-stu-id="6eaa7-179">Adding notifications to your message</span></span>

<span data-ttu-id="6eaa7-180">Уведомления оповещают пользователей о новых задачах, упоминаниях и примечаниях, связанных с тем, над чем они работают, или о том, что им нужно посмотреть, вставив уведомление в веб-канал активности.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="6eaa7-181">Вы можете настроить уведомления для запуска из сообщения бота, установив для свойства `TeamsChannelData` `Notification.Alert` объектов true.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="6eaa7-182">В конечном счете, будет зависеть от параметров Teams отдельного пользователя, и вы не сможете программным образом переопределять эти параметры.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="6eaa7-183">Тип уведомления будет баннером или баннером и сообщением электронной почты.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6eaa7-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6eaa7-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6eaa7-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6eaa7-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="6eaa7-186">Python</span><span class="sxs-lookup"><span data-stu-id="6eaa7-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="6eaa7-187">JSON</span><span class="sxs-lookup"><span data-stu-id="6eaa7-187">JSON</span></span>](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

## <a name="picture-messages"></a><span data-ttu-id="6eaa7-188">Сообщения с рисунками</span><span class="sxs-lookup"><span data-stu-id="6eaa7-188">Picture messages</span></span>

<span data-ttu-id="6eaa7-189">Изображения отправляются путем добавления вложений в сообщение.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="6eaa7-190">Дополнительные сведения о вложениях можно найти в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="6eaa7-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="6eaa7-191">Изображения могут иметь не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="6eaa7-192">Рекомендуется указать высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="6eaa7-193">Если вы используете Markdown, размер изображения по умолчанию составляет 256×256.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="6eaa7-194">Например:</span><span class="sxs-lookup"><span data-stu-id="6eaa7-194">For example:</span></span>

* <span data-ttu-id="6eaa7-195">Использование — `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="6eaa7-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="6eaa7-196">Не используйте — `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="6eaa7-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="code-sample"></a><span data-ttu-id="6eaa7-197">Пример кода</span><span class="sxs-lookup"><span data-stu-id="6eaa7-197">Code sample</span></span>
|<span data-ttu-id="6eaa7-198">**Имя примера**</span><span class="sxs-lookup"><span data-stu-id="6eaa7-198">**Sample name**</span></span> | <span data-ttu-id="6eaa7-199">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6eaa7-199">**Description**</span></span> | <span data-ttu-id="6eaa7-200">**. NETCore**</span><span class="sxs-lookup"><span data-stu-id="6eaa7-200">**.NETCore**</span></span> | <span data-ttu-id="6eaa7-201">**Javascript**</span><span class="sxs-lookup"><span data-stu-id="6eaa7-201">**Javascript**</span></span> | <span data-ttu-id="6eaa7-202">**Python**</span><span class="sxs-lookup"><span data-stu-id="6eaa7-202">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="6eaa7-203">Бот беседы Teams</span><span class="sxs-lookup"><span data-stu-id="6eaa7-203">Teams Conversation Bot</span></span> | <span data-ttu-id="6eaa7-204">Обработка событий обмена сообщениями и бесед.</span><span class="sxs-lookup"><span data-stu-id="6eaa7-204">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="6eaa7-205">View</span><span class="sxs-lookup"><span data-stu-id="6eaa7-205">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="6eaa7-206">View</span><span class="sxs-lookup"><span data-stu-id="6eaa7-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="6eaa7-207">View</span><span class="sxs-lookup"><span data-stu-id="6eaa7-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="6eaa7-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6eaa7-208">Next steps</span></span>

* [<span data-ttu-id="6eaa7-209">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="6eaa7-209">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="6eaa7-210">Подписка на события беседы</span><span class="sxs-lookup"><span data-stu-id="6eaa7-210">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
