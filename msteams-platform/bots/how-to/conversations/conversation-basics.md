---
title: Основы разговора
description: описывает способы беседы с ботом Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 4eba22e9b29f5378dc03480ba5f6ba421f816eb3
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449509"
---
# <a name="conversation-basics"></a><span data-ttu-id="341eb-103">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="341eb-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="341eb-104">Беседа — это серия сообщений, отправленных между ботом и одним или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="341eb-104">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="341eb-105">Существует три типа бесед, которые также называются области в Teams:</span><span class="sxs-lookup"><span data-stu-id="341eb-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="341eb-106">Тип беседы</span><span class="sxs-lookup"><span data-stu-id="341eb-106">Conversation type</span></span> | <span data-ttu-id="341eb-107">Описание</span><span class="sxs-lookup"><span data-stu-id="341eb-107">Description</span></span> |
| ------- | ----------- |
|  `teams` | <span data-ttu-id="341eb-108">Также называются телефонные беседы, видимые всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="341eb-108">Also called channel conversations, visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="341eb-109">Беседы между ботами и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="341eb-109">Conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="341eb-110">Чат между ботом и двумя или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="341eb-110">Chat between a bot and two or more users.</span></span> <span data-ttu-id="341eb-111">Также включает бота в чаты собраний.</span><span class="sxs-lookup"><span data-stu-id="341eb-111">Also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="341eb-112">Бот ведет себя немного по-другому в зависимости от того, в какой беседе он участвует:</span><span class="sxs-lookup"><span data-stu-id="341eb-112">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="341eb-113">Боты в беседах с каналами и групповыми чатами требуют от пользователя @ упоминания бота, чтобы вызвать его в канале.</span><span class="sxs-lookup"><span data-stu-id="341eb-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="341eb-114">Боты в беседе один к одному не требуют упоминания @.</span><span class="sxs-lookup"><span data-stu-id="341eb-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="341eb-115">Все сообщения, отправленные пользователем по маршрутам к боту.</span><span class="sxs-lookup"><span data-stu-id="341eb-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="341eb-116">Чтобы включить бот в определенной области, добавьте эту область в [манифест приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="341eb-116">To enable your bot in a particular scope, add that scope to your [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="activities"></a><span data-ttu-id="341eb-117">Действия</span><span class="sxs-lookup"><span data-stu-id="341eb-117">Activities</span></span>

<span data-ttu-id="341eb-118">Каждое сообщение — `Activity` это объект типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="341eb-118">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="341eb-119">Когда пользователь отправляет сообщение, Teams отправляет сообщение вашему боту; В частности, он отправляет объект JSON в конечную точку обмена сообщениями вашего бота.</span><span class="sxs-lookup"><span data-stu-id="341eb-119">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="341eb-120">Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="341eb-120">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="341eb-121">Основные беседы обрабатываются с помощью соединиттеля Bot Framework, единого API REST.</span><span class="sxs-lookup"><span data-stu-id="341eb-121">Basic conversations are handled through the Bot Framework Connector, a single REST API.</span></span> <span data-ttu-id="341eb-122">Этот API позволяет боту взаимодействовать с Teams и другими каналами.</span><span class="sxs-lookup"><span data-stu-id="341eb-122">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="341eb-123">SDK Bot Builder предоставляет простой доступ к этому API, дополнительные функции для управления потоком беседы и состоянием, а также простые способы включения когнитивных служб, таких как обработка естественного языка (NLP).</span><span class="sxs-lookup"><span data-stu-id="341eb-123">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="341eb-124">Получение сообщения</span><span class="sxs-lookup"><span data-stu-id="341eb-124">Receive a message</span></span>

<span data-ttu-id="341eb-125">Чтобы получить текстовое сообщение, используйте `Text` свойство `Activity` объекта.</span><span class="sxs-lookup"><span data-stu-id="341eb-125">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="341eb-126">В обработнике действий бота используйте объект контекста поворота для чтения `Activity` одного запроса сообщения.</span><span class="sxs-lookup"><span data-stu-id="341eb-126">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="341eb-127">Ниже приводится пример кода.</span><span class="sxs-lookup"><span data-stu-id="341eb-127">The following code shows an example.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="341eb-128">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="341eb-128">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="341eb-129">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="341eb-129">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="341eb-130">Python</span><span class="sxs-lookup"><span data-stu-id="341eb-130">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="341eb-131">JSON</span><span class="sxs-lookup"><span data-stu-id="341eb-131">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="341eb-132">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="341eb-132">Send a message</span></span>

<span data-ttu-id="341eb-133">Чтобы отправить текстовое сообщение, укажите строку, которая будет отправляться в качестве действия.</span><span class="sxs-lookup"><span data-stu-id="341eb-133">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="341eb-134">В обработнике действий бота используйте метод объекта контекста поворота для `SendActivityAsync` отправки единого ответа сообщения.</span><span class="sxs-lookup"><span data-stu-id="341eb-134">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="341eb-135">Используйте метод объекта `SendActivitiesAsync` для отправки сразу нескольких ответов.</span><span class="sxs-lookup"><span data-stu-id="341eb-135">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="341eb-136">В следующем коде показан пример отправки сообщения при добавлении в беседу.</span><span class="sxs-lookup"><span data-stu-id="341eb-136">The following code shows an example of sending a message when someone is added to a conversation.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="341eb-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="341eb-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="341eb-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="341eb-138">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="341eb-139">Python</span><span class="sxs-lookup"><span data-stu-id="341eb-139">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="341eb-140">JSON</span><span class="sxs-lookup"><span data-stu-id="341eb-140">JSON</span></span>](#tab/json)

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

> [!NOTE]
> <span data-ttu-id="341eb-141">Разделение сообщений происходит, когда текстовое сообщение и вложение отправляются в той же полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="341eb-141">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="341eb-142">Это действие разделено на отдельные действия Microsoft Teams, одно действие с только текстовым сообщением, а другое с вложением.</span><span class="sxs-lookup"><span data-stu-id="341eb-142">This activity is split into separate activities by Microsoft Teams, one activity with just a text message and the other with an attachment.</span></span> <span data-ttu-id="341eb-143">При разделении действия в ответ не получается ID сообщения, [](~/bots/how-to/update-and-delete-bot-messages.md) который используется для обновления или удаления сообщения.</span><span class="sxs-lookup"><span data-stu-id="341eb-143">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="341eb-144">Рекомендуется отправлять отдельные действия, а не в зависимости от разделения сообщений.</span><span class="sxs-lookup"><span data-stu-id="341eb-144">It is recommended to send separate activities instead of depending on message splitting.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="341eb-145">Данные канала teams</span><span class="sxs-lookup"><span data-stu-id="341eb-145">Teams channel data</span></span>

<span data-ttu-id="341eb-146">Объект содержит сведения, определенные для Teams, и является окончательным источником для кодов `channelData` групп и каналов.</span><span class="sxs-lookup"><span data-stu-id="341eb-146">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="341eb-147">Может потребоваться кэширования и использования этих ID-данных в качестве ключей для локального хранения.</span><span class="sxs-lookup"><span data-stu-id="341eb-147">You may need to cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="341eb-148">В SDK обычно извлекаются важные сведения из объекта, чтобы сделать `TeamsActivityHandler` `channelData` его доступным.</span><span class="sxs-lookup"><span data-stu-id="341eb-148">The `TeamsActivityHandler` in the SDK, typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="341eb-149">Однако вы всегда можете получить доступ к исходным данным `turnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="341eb-149">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="341eb-150">Объект не входит в сообщения в личных беседах, так как они проходят `channelData` за пределами любого канала.</span><span class="sxs-lookup"><span data-stu-id="341eb-150">The `channelData` object is not included in messages in personal conversations, as these take place outside of any channel.</span></span>

<span data-ttu-id="341eb-151">Типичный объект channelData в действии, отправленный боту, содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="341eb-151">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="341eb-152">`eventType`Тип событий Teams; передается только в случаях [событий изменения канала.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="341eb-152">`eventType` Teams event type; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="341eb-153">`tenant.id` ID клиента Azure Active Directory, переданный во всех контекстах.</span><span class="sxs-lookup"><span data-stu-id="341eb-153">`tenant.id` Azure Active Directory tenant ID, passed in all contexts.</span></span>
* <span data-ttu-id="341eb-154">`team` Передается только в контекстах каналов, а не в личном чате.</span><span class="sxs-lookup"><span data-stu-id="341eb-154">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="341eb-155">`id` GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="341eb-155">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="341eb-156">`name`Имя команды; передается только в случаях [переименования событий команды.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="341eb-156">`name` Name of the team; passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="341eb-157">`channel` Передается только в контекстах каналов, когда бот упоминается или для событий в каналах в командах, где был добавлен бот.</span><span class="sxs-lookup"><span data-stu-id="341eb-157">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="341eb-158">`id` GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="341eb-158">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="341eb-159">`name`Имя канала; передается только в случаях [событий изменения канала.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="341eb-159">`name` Channel name; passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="341eb-160">`channelData.teamsTeamId` Обесценилось.</span><span class="sxs-lookup"><span data-stu-id="341eb-160">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="341eb-161">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="341eb-161">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="341eb-162">`channelData.teamsChannelId` Обесценилось.</span><span class="sxs-lookup"><span data-stu-id="341eb-162">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="341eb-163">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="341eb-163">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="341eb-164">Пример объекта channelData (событие channelCreated)</span><span class="sxs-lookup"><span data-stu-id="341eb-164">Example channelData object (channelCreated event)</span></span>

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

## <a name="message-content"></a><span data-ttu-id="341eb-165">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="341eb-165">Message content</span></span>

<span data-ttu-id="341eb-166">Бот может отправлять богатый текст, изображения и карточки.</span><span class="sxs-lookup"><span data-stu-id="341eb-166">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="341eb-167">Пользователи могут отправлять богатый текст и изображения в бот.</span><span class="sxs-lookup"><span data-stu-id="341eb-167">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="341eb-168">Format</span><span class="sxs-lookup"><span data-stu-id="341eb-168">Format</span></span>    | <span data-ttu-id="341eb-169">От пользователя к боту</span><span class="sxs-lookup"><span data-stu-id="341eb-169">From user to bot</span></span> | <span data-ttu-id="341eb-170">От бота к пользователю</span><span class="sxs-lookup"><span data-stu-id="341eb-170">From bot to user</span></span> | <span data-ttu-id="341eb-171">Примечания</span><span class="sxs-lookup"><span data-stu-id="341eb-171">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="341eb-172">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="341eb-172">Rich text</span></span> | <span data-ttu-id="341eb-173">✔</span><span class="sxs-lookup"><span data-stu-id="341eb-173">✔</span></span>                | <span data-ttu-id="341eb-174">✔</span><span class="sxs-lookup"><span data-stu-id="341eb-174">✔</span></span>                |                                                                                         |
| <span data-ttu-id="341eb-175">Изображения</span><span class="sxs-lookup"><span data-stu-id="341eb-175">Pictures</span></span>  | <span data-ttu-id="341eb-176">✔</span><span class="sxs-lookup"><span data-stu-id="341eb-176">✔</span></span>                | <span data-ttu-id="341eb-177">✔</span><span class="sxs-lookup"><span data-stu-id="341eb-177">✔</span></span>                | <span data-ttu-id="341eb-178">Максимальный размер 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF не поддерживается</span><span class="sxs-lookup"><span data-stu-id="341eb-178">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span>  |
| <span data-ttu-id="341eb-179">Карточки</span><span class="sxs-lookup"><span data-stu-id="341eb-179">Cards</span></span>     | <span data-ttu-id="341eb-180">✖</span><span class="sxs-lookup"><span data-stu-id="341eb-180">✖</span></span>                | <span data-ttu-id="341eb-181">✔</span><span class="sxs-lookup"><span data-stu-id="341eb-181">✔</span></span>                | <span data-ttu-id="341eb-182">См. [ссылку на карточки Teams для](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемых карт</span><span class="sxs-lookup"><span data-stu-id="341eb-182">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="341eb-183">Emojis</span><span class="sxs-lookup"><span data-stu-id="341eb-183">Emojis</span></span>    | <span data-ttu-id="341eb-184">✖</span><span class="sxs-lookup"><span data-stu-id="341eb-184">✖</span></span>                | <span data-ttu-id="341eb-185">✔</span><span class="sxs-lookup"><span data-stu-id="341eb-185">✔</span></span>                | <span data-ttu-id="341eb-186">Teams currently supports emojis through UTF-16 (such as U+1F600 for grinning face)</span><span class="sxs-lookup"><span data-stu-id="341eb-186">Teams currently supports emojis through UTF-16 (such as U+1F600 for grinning face)</span></span>          |

## <a name="adding-notifications-to-your-message"></a><span data-ttu-id="341eb-187">Добавление уведомлений в сообщение</span><span class="sxs-lookup"><span data-stu-id="341eb-187">Adding notifications to your message</span></span>

<span data-ttu-id="341eb-188">Уведомления оповещают пользователей о новых задачах, упоминаниях и комментариях, связанных с тем, над чем они работают или на которые необходимо смотреть, вставив уведомление в канал активности.</span><span class="sxs-lookup"><span data-stu-id="341eb-188">Notifications alert users about new tasks, mentions, and comments related to what they are working on or need to look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="341eb-189">Вы можете настроить уведомления для запуска бот-сообщения, установив свойство `TeamsChannelData` `Notification.Alert` объектов до true.</span><span class="sxs-lookup"><span data-stu-id="341eb-189">You can set notifications to trigger from your bot-message by setting the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="341eb-190">В конечном счете, вопрос о том, будет ли поднято уведомление, зависит от параметров teams отдельного пользователя, и программным образом переопреять эти параметры невозможно.</span><span class="sxs-lookup"><span data-stu-id="341eb-190">Whether or not a notification is raised ultimately depends on the individual user's Teams settings and you cannot programmatically override these settings.</span></span> <span data-ttu-id="341eb-191">Тип уведомления — это баннер или баннер и электронная почта.</span><span class="sxs-lookup"><span data-stu-id="341eb-191">The type of notification is either a banner or both a banner and an email.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="341eb-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="341eb-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="341eb-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="341eb-193">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="341eb-194">Python</span><span class="sxs-lookup"><span data-stu-id="341eb-194">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="341eb-195">JSON</span><span class="sxs-lookup"><span data-stu-id="341eb-195">JSON</span></span>](#tab/json)

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

## <a name="picture-messages"></a><span data-ttu-id="341eb-196">Сообщения изображений</span><span class="sxs-lookup"><span data-stu-id="341eb-196">Picture messages</span></span>

<span data-ttu-id="341eb-197">Изображения отправляются путем добавления вложений в сообщение.</span><span class="sxs-lookup"><span data-stu-id="341eb-197">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="341eb-198">Дополнительные сведения о вложениях можно найти в документации [Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)</span><span class="sxs-lookup"><span data-stu-id="341eb-198">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="341eb-199">Изображения могут быть не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF.</span><span class="sxs-lookup"><span data-stu-id="341eb-199">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="341eb-200">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="341eb-200">Animated GIF is not supported.</span></span>

<span data-ttu-id="341eb-201">Всегда укажите высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="341eb-201">Always specify the height and width of each image by using XML.</span></span> <span data-ttu-id="341eb-202">В Markdown размер изображения по умолчанию составляет 256×256.</span><span class="sxs-lookup"><span data-stu-id="341eb-202">In Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="341eb-203">Например:</span><span class="sxs-lookup"><span data-stu-id="341eb-203">For example:</span></span>

* <span data-ttu-id="341eb-204">Использование - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="341eb-204">Use - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="341eb-205">Не используйте - `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="341eb-205">Don't use - `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="341eb-206">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="341eb-206">Adaptive cards</span></span>

<span data-ttu-id="341eb-207">Для отправки простой адаптивной карты используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="341eb-207">Use the following code to send a simple adaptive card:</span></span>

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

<span data-ttu-id="341eb-208">Дополнительные информацию о картах и картах в ботах см. в [документации по картам.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="341eb-208">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="341eb-209">Пример кода</span><span class="sxs-lookup"><span data-stu-id="341eb-209">Code sample</span></span>

|<span data-ttu-id="341eb-210">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="341eb-210">**Sample name**</span></span> | <span data-ttu-id="341eb-211">**Описание**</span><span class="sxs-lookup"><span data-stu-id="341eb-211">**Description**</span></span> | <span data-ttu-id="341eb-212">**. NETCore**</span><span class="sxs-lookup"><span data-stu-id="341eb-212">**.NETCore**</span></span> | <span data-ttu-id="341eb-213">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="341eb-213">**JavaScript**</span></span> | <span data-ttu-id="341eb-214">**Python**</span><span class="sxs-lookup"><span data-stu-id="341eb-214">**Python**</span></span>|
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="341eb-215">Командный бот беседы</span><span class="sxs-lookup"><span data-stu-id="341eb-215">Teams Conversation Bot</span></span> | <span data-ttu-id="341eb-216">Обработка событий обмена сообщениями и бесед.</span><span class="sxs-lookup"><span data-stu-id="341eb-216">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="341eb-217">View</span><span class="sxs-lookup"><span data-stu-id="341eb-217">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="341eb-218">View</span><span class="sxs-lookup"><span data-stu-id="341eb-218">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="341eb-219">View</span><span class="sxs-lookup"><span data-stu-id="341eb-219">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a><span data-ttu-id="341eb-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="341eb-220">Next steps</span></span>

* [<span data-ttu-id="341eb-221">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="341eb-221">Sending proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
* [<span data-ttu-id="341eb-222">Подписка на события беседы</span><span class="sxs-lookup"><span data-stu-id="341eb-222">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
