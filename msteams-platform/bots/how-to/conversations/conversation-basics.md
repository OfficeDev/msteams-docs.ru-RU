---
title: Основы разговора
author: clearab
description: Как создать беседу с роботом Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bc016a8f0dcce474f80898dc93e309692ba20471
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819055"
---
# <a name="conversation-basics"></a><span data-ttu-id="7a385-103">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="7a385-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="7a385-104">Беседа — это серия сообщений, отправляемых между Bot и одним или несколькими пользователями.</span><span class="sxs-lookup"><span data-stu-id="7a385-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="7a385-105">В Teams существует три вида бесед (также называемых областями):</span><span class="sxs-lookup"><span data-stu-id="7a385-105">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="7a385-106">`teams` Также называется каналы каналов, видимых всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="7a385-106">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="7a385-107">`personal` Беседы между Боты и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="7a385-107">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="7a385-108">`groupChat` Чат между Bot и двумя или несколькими пользователями.</span><span class="sxs-lookup"><span data-stu-id="7a385-108">`groupChat` Chat between a bot and two or more users.</span></span> <span data-ttu-id="7a385-109">Кроме того, в конференциях можно включить робота.</span><span class="sxs-lookup"><span data-stu-id="7a385-109">Also enables your bot in meeting chats.</span></span>

<span data-ttu-id="7a385-110">В зависимости от типа беседы, в которой она участвует, программа-робота немного ведет себя по-разному.</span><span class="sxs-lookup"><span data-stu-id="7a385-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="7a385-111">Для боты в беседах в канале и группе необходимо, чтобы пользователь "@" привызывал его в канале.</span><span class="sxs-lookup"><span data-stu-id="7a385-111">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="7a385-112">Для боты в беседе "один к одному" не требуется указать @ упоминание.</span><span class="sxs-lookup"><span data-stu-id="7a385-112">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="7a385-113">Все сообщения, отправленные пользователем, будут перенаправляться в робот.</span><span class="sxs-lookup"><span data-stu-id="7a385-113">All messages sent by the user will be routed to your bot.</span></span>

<span data-ttu-id="7a385-114">Чтобы включить Bot в определенной области, добавьте эту область в [манифест приложения](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="7a385-114">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="7a385-115">Действия</span><span class="sxs-lookup"><span data-stu-id="7a385-115">Activities</span></span>

<span data-ttu-id="7a385-116">Каждое сообщение является `Activity` объектом типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="7a385-116">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="7a385-117">Когда пользователь отправляет сообщение, Teams отправляет сообщение на сервер почтовых роботов; в частности, он отправляет объект JSON в конечную точку обмена сообщениями ленты.</span><span class="sxs-lookup"><span data-stu-id="7a385-117">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="7a385-118">Ваш почтовый робот просматривает сообщение, чтобы определить его тип и ответить соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="7a385-118">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="7a385-119">Основная беседа обрабатывается через соединитель Bot Framework, один REST API, позволяющий роботам общаться с Teams и другими каналами.</span><span class="sxs-lookup"><span data-stu-id="7a385-119">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="7a385-120">Пакет SDK построителя позволяет легко получить доступ к этому API, дополнительные функции для управления движением и состоянием беседы, а также простые способы внедрения таких служб, как естественный язык (НЛП).</span><span class="sxs-lookup"><span data-stu-id="7a385-120">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="7a385-121">Получение сообщения</span><span class="sxs-lookup"><span data-stu-id="7a385-121">Receive a message</span></span>

<span data-ttu-id="7a385-122">Для получения текстового сообщения используйте `Text` свойство `Activity` объекта.</span><span class="sxs-lookup"><span data-stu-id="7a385-122">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="7a385-123">В обработчике действий Bot используйте объект "переключить контекст", `Activity` чтобы считать один запрос сообщения.</span><span class="sxs-lookup"><span data-stu-id="7a385-123">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="7a385-124">Ниже приведен пример кода.</span><span class="sxs-lookup"><span data-stu-id="7a385-124">The code below shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a385-125">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a385-125">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a385-126">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a385-126">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="7a385-127">Python</span><span class="sxs-lookup"><span data-stu-id="7a385-127">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="7a385-128">JSON</span><span class="sxs-lookup"><span data-stu-id="7a385-128">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="7a385-129">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="7a385-129">Send a message</span></span>

<span data-ttu-id="7a385-130">Чтобы отправить текстовое сообщение, укажите строку, которую необходимо отправить как действие.</span><span class="sxs-lookup"><span data-stu-id="7a385-130">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="7a385-131">В обработчиках действий Bot используйте метод "переключить контекстный объект" `SendActivityAsync` для отправки одного ответа на сообщение.</span><span class="sxs-lookup"><span data-stu-id="7a385-131">In the bot's activity handlers, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="7a385-132">Кроме того, можно использовать метод объекта `SendActivitiesAsync` для отправки нескольких ответов одновременно.</span><span class="sxs-lookup"><span data-stu-id="7a385-132">You can also use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="7a385-133">В приведенном ниже коде показан пример отправки сообщения, когда кто-то добавляется в беседу.</span><span class="sxs-lookup"><span data-stu-id="7a385-133">The code below shows an example of sending a message when someone is added to a conversation</span></span>  

# <a name="cnet"></a>[<span data-ttu-id="7a385-134">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a385-134">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a385-135">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a385-135">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="7a385-136">Python</span><span class="sxs-lookup"><span data-stu-id="7a385-136">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="7a385-137">JSON</span><span class="sxs-lookup"><span data-stu-id="7a385-137">JSON</span></span>](#tab/json)

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

## <a name="teams-channel-data"></a><span data-ttu-id="7a385-138">Данные канала Teams</span><span class="sxs-lookup"><span data-stu-id="7a385-138">Teams channel data</span></span>

<span data-ttu-id="7a385-139">`channelData`Объект содержит сведения, зависящие от команды, и является основным источником для идентификаторов команд и каналов.</span><span class="sxs-lookup"><span data-stu-id="7a385-139">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="7a385-140">Возможно, вам потребуется кэшировать и использовать эти идентификаторы в качестве ключей для локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="7a385-140">You may need to cache and use these ids as keys for local storage.</span></span> <span data-ttu-id="7a385-141">`TeamsActivityHandler`В пакете SDK обычно запрашиваются важные сведения из `channelData` объекта, чтобы сделать его более легко доступным, но вы всегда можете получить доступ к исходным данным из `turnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="7a385-141">The `TeamsActivityHandler` in the SDK will typically pull out important information from the `channelData` object to make it more easily accessible, however you can always access the original information from the `turnContext` object.</span></span>

<span data-ttu-id="7a385-142">Этот `channelData` объект не включается в сообщения в личных беседах, так как они выполняются вне какого-либо канала.</span><span class="sxs-lookup"><span data-stu-id="7a385-142">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="7a385-143">Типичный объект Чаннелдата в действии, отправляемом на почтовый робот, содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="7a385-143">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="7a385-144">`eventType` Тип события Teams; передается только в случае [событий изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="7a385-144">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="7a385-145">`tenant.id` Идентификатор клиента Azure Active Directory; передается во всех контекстах</span><span class="sxs-lookup"><span data-stu-id="7a385-145">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="7a385-146">`team` Передается только в контекстах канала, а не в личном сеансе чата.</span><span class="sxs-lookup"><span data-stu-id="7a385-146">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="7a385-147">`id` GUID для канала</span><span class="sxs-lookup"><span data-stu-id="7a385-147">`id` GUID for the channel</span></span>
  * <span data-ttu-id="7a385-148">`name` Имя команды; передается только в случае [событий переименования команды](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="7a385-148">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span></span>
* <span data-ttu-id="7a385-149">`channel` Передается только в контекстах канала при упоминании Bot или для событий в каналах в Microsoft Teams, где добавлен Bot</span><span class="sxs-lookup"><span data-stu-id="7a385-149">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="7a385-150">`id` GUID для канала</span><span class="sxs-lookup"><span data-stu-id="7a385-150">`id` GUID for the channel</span></span>
  * <span data-ttu-id="7a385-151">`name` Имя канала; передается только в случае [событий изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="7a385-151">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="7a385-152">`channelData.teamsTeamId` Устаревшие.</span><span class="sxs-lookup"><span data-stu-id="7a385-152">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="7a385-153">Это свойство включено только для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="7a385-153">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="7a385-154">`channelData.teamsChannelId` Устаревшие.</span><span class="sxs-lookup"><span data-stu-id="7a385-154">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="7a385-155">Это свойство включено только для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="7a385-155">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="7a385-156">Пример объекта Чаннелдата (событие Чаннелкреатед)</span><span class="sxs-lookup"><span data-stu-id="7a385-156">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="7a385-157">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="7a385-157">Message content</span></span>

<span data-ttu-id="7a385-158">Ваш робот может отправлять форматированный текст, изображения и карточки.</span><span class="sxs-lookup"><span data-stu-id="7a385-158">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="7a385-159">Пользователи могут отправлять форматированный текст и изображения в Bot.</span><span class="sxs-lookup"><span data-stu-id="7a385-159">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="7a385-160">Format</span><span class="sxs-lookup"><span data-stu-id="7a385-160">Format</span></span>    | <span data-ttu-id="7a385-161">От пользователя к Bot</span><span class="sxs-lookup"><span data-stu-id="7a385-161">From user to bot</span></span> | <span data-ttu-id="7a385-162">От Bot к пользователю</span><span class="sxs-lookup"><span data-stu-id="7a385-162">From bot to user</span></span> | <span data-ttu-id="7a385-163">Примечания</span><span class="sxs-lookup"><span data-stu-id="7a385-163">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="7a385-164">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="7a385-164">Rich text</span></span> | <span data-ttu-id="7a385-165">✔</span><span class="sxs-lookup"><span data-stu-id="7a385-165">✔</span></span>                | <span data-ttu-id="7a385-166">✔</span><span class="sxs-lookup"><span data-stu-id="7a385-166">✔</span></span>                |                                                                                         |
| <span data-ttu-id="7a385-167">Изображения</span><span class="sxs-lookup"><span data-stu-id="7a385-167">Pictures</span></span>  | <span data-ttu-id="7a385-168">✔</span><span class="sxs-lookup"><span data-stu-id="7a385-168">✔</span></span>                | <span data-ttu-id="7a385-169">✔</span><span class="sxs-lookup"><span data-stu-id="7a385-169">✔</span></span>                | <span data-ttu-id="7a385-170">Не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается</span><span class="sxs-lookup"><span data-stu-id="7a385-170">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="7a385-171">Карточки</span><span class="sxs-lookup"><span data-stu-id="7a385-171">Cards</span></span>     | <span data-ttu-id="7a385-172">✖</span><span class="sxs-lookup"><span data-stu-id="7a385-172">✖</span></span>                | <span data-ttu-id="7a385-173">✔</span><span class="sxs-lookup"><span data-stu-id="7a385-173">✔</span></span>                | <span data-ttu-id="7a385-174">Поддерживаемые карточки представлены в [справочнике по карточке Teams](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="7a385-174">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="7a385-175">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="7a385-175">Emojis</span></span>    | <span data-ttu-id="7a385-176">✖</span><span class="sxs-lookup"><span data-stu-id="7a385-176">✖</span></span>                | <span data-ttu-id="7a385-177">✔</span><span class="sxs-lookup"><span data-stu-id="7a385-177">✔</span></span>                | <span data-ttu-id="7a385-178">В настоящее время Teams поддерживает эмодзи, используя кодировку UTF-16 (например, U + 1F600 для гриннинг Face)</span><span class="sxs-lookup"><span data-stu-id="7a385-178">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="7a385-179">Добавление уведомлений в сообщение</span><span class="sxs-lookup"><span data-stu-id="7a385-179">Adding notifications to your message</span></span>

<span data-ttu-id="7a385-180">Уведомления уведомляют пользователей о новых задачах, упоминании и комментариях, связанных с тем, над чем они работают, или необходимо просмотреть, вставив уведомление в свой канал активности.</span><span class="sxs-lookup"><span data-stu-id="7a385-180">Notifications alert users about new tasks, mentions and comments related to what they are working on, or need to look at by inserting a notice into their Activity Feed.</span></span> <span data-ttu-id="7a385-181">Вы можете настроить уведомления для запуска из сообщения Bot, задав `TeamsChannelData` `Notification.Alert` для свойства Objects значение true.</span><span class="sxs-lookup"><span data-stu-id="7a385-181">You can set notifications to trigger from your bot message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="7a385-182">Если уведомление не будет вызвано, в конечном итоге зависит от параметров Teams отдельного пользователя, и вы не сможете программно переопределить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="7a385-182">Whether or not a notification is raised will ultimately depend on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="7a385-183">Типом уведомления будет либо баннер, либо баннер и электронная почта.</span><span class="sxs-lookup"><span data-stu-id="7a385-183">The type of notification will be either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7a385-184">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7a385-184">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7a385-185">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7a385-185">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="7a385-186">Python</span><span class="sxs-lookup"><span data-stu-id="7a385-186">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="7a385-187">JSON</span><span class="sxs-lookup"><span data-stu-id="7a385-187">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="7a385-188">Графические сообщения</span><span class="sxs-lookup"><span data-stu-id="7a385-188">Picture messages</span></span>

<span data-ttu-id="7a385-189">Изображения отправляются путем добавления вложений к сообщению.</span><span class="sxs-lookup"><span data-stu-id="7a385-189">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="7a385-190">Дополнительные сведения о вложениях можно найти в [документации по среде Bot](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span><span class="sxs-lookup"><span data-stu-id="7a385-190">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="7a385-191">Рисунки могут иметь не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7a385-191">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="7a385-192">Рекомендуем указать высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="7a385-192">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="7a385-193">Если вы используете Markdown, размер изображения по умолчанию равен 256 × 256.</span><span class="sxs-lookup"><span data-stu-id="7a385-193">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="7a385-194">Например:</span><span class="sxs-lookup"><span data-stu-id="7a385-194">For example:</span></span>

* <span data-ttu-id="7a385-195">Используйте `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="7a385-195">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="7a385-196">Не используйте — `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="7a385-196">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a385-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a385-197">Next steps</span></span>

* [<span data-ttu-id="7a385-198">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="7a385-198">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="7a385-199">Подписка на события беседы</span><span class="sxs-lookup"><span data-stu-id="7a385-199">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
