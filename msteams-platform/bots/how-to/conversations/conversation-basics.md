---
title: Основы разговора
description: описывает способы беседы с ботом Microsoft Teams
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 193a93dbf775389383e0385207fa4112440bffe5
ms.sourcegitcommit: 82bda0599ba2676ab9348c2f4284f73c7dad0838
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596676"
---
# <a name="conversation-basics"></a><span data-ttu-id="6aa89-103">Основы разговора</span><span class="sxs-lookup"><span data-stu-id="6aa89-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="6aa89-104">Беседа — это серия сообщений, отправленных между ботом Microsoft Teams и одним или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="6aa89-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="6aa89-105">Существует три типа бесед, которые также называются области в Teams:</span><span class="sxs-lookup"><span data-stu-id="6aa89-105">There are three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="6aa89-106">Тип беседы</span><span class="sxs-lookup"><span data-stu-id="6aa89-106">Conversation type</span></span> | <span data-ttu-id="6aa89-107">Описание</span><span class="sxs-lookup"><span data-stu-id="6aa89-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="6aa89-108">Этот тип беседы виден всем участникам канала.</span><span class="sxs-lookup"><span data-stu-id="6aa89-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="6aa89-109">Этот тип беседы включает беседы между ботами и одним пользователем.</span><span class="sxs-lookup"><span data-stu-id="6aa89-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="6aa89-110">Этот тип беседы включает чат между ботом и двумя или более пользователями.</span><span class="sxs-lookup"><span data-stu-id="6aa89-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="6aa89-111">Он также позволяет вашему боту в чатах собраний.</span><span class="sxs-lookup"><span data-stu-id="6aa89-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="6aa89-112">Бот ведет себя по-разному в зависимости от разговора, в который он вовлечен:</span><span class="sxs-lookup"><span data-stu-id="6aa89-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="6aa89-113">Боты в беседах с каналами и групповыми чатами требуют от пользователя @ упоминания бота, чтобы вызвать его в канале.</span><span class="sxs-lookup"><span data-stu-id="6aa89-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="6aa89-114">Боты в беседе один к одному не требуют упоминания @.</span><span class="sxs-lookup"><span data-stu-id="6aa89-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="6aa89-115">Все сообщения, отправленные пользователем по маршрутам к боту.</span><span class="sxs-lookup"><span data-stu-id="6aa89-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="6aa89-116">Чтобы бот работал в определенной беседе или области, добавьте поддержку к этой области в [манифесте приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="6aa89-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

## <a name="messages-in-bot-conversations"></a><span data-ttu-id="6aa89-117">Сообщения в беседах с ботами</span><span class="sxs-lookup"><span data-stu-id="6aa89-117">Messages in bot conversations</span></span>

<span data-ttu-id="6aa89-118">Каждое сообщение в беседе является `Activity` объектом типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="6aa89-118">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="6aa89-119">Когда пользователь отправляет сообщение, Teams отправляет сообщение вашему боту.</span><span class="sxs-lookup"><span data-stu-id="6aa89-119">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="6aa89-120">Teams отправляет объект JSON в конечную точку обмена сообщениями вашего бота.</span><span class="sxs-lookup"><span data-stu-id="6aa89-120">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="6aa89-121">Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="6aa89-121">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="6aa89-122">Основные беседы обрабатываются через соединители Bot Framework, единый API REST.</span><span class="sxs-lookup"><span data-stu-id="6aa89-122">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="6aa89-123">Этот API позволяет боту взаимодействовать с Teams и другими каналами.</span><span class="sxs-lookup"><span data-stu-id="6aa89-123">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="6aa89-124">В SDK-конструкторе ботов приводится следующее:</span><span class="sxs-lookup"><span data-stu-id="6aa89-124">The Bot Builder SDK provides the following:</span></span>

* <span data-ttu-id="6aa89-125">Простой доступ к соединители Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="6aa89-125">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="6aa89-126">Дополнительные функции для управления потоком и состоянием беседы.</span><span class="sxs-lookup"><span data-stu-id="6aa89-126">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="6aa89-127">Простые способы включения когнитивных служб, таких как обработка естественного языка (NLP).</span><span class="sxs-lookup"><span data-stu-id="6aa89-127">Simple ways to incorporate cognitive services such as Natural Language Processing (NLP).</span></span>

<span data-ttu-id="6aa89-128">Бот получает сообщения от Teams с помощью свойства и отправляет пользователям одиночные или несколько `Text` ответов на сообщения.</span><span class="sxs-lookup"><span data-stu-id="6aa89-128">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="6aa89-129">Получение сообщения</span><span class="sxs-lookup"><span data-stu-id="6aa89-129">Receive a message</span></span>

<span data-ttu-id="6aa89-130">Чтобы получить текстовое сообщение, используйте свойство `Text` объекта `Activity`.</span><span class="sxs-lookup"><span data-stu-id="6aa89-130">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="6aa89-131">В обработчике активности бота используйте объект контекста поворота `Activity` для чтения одного запроса сообщения.</span><span class="sxs-lookup"><span data-stu-id="6aa89-131">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="6aa89-132">В следующем коде показан пример получения сообщения:</span><span class="sxs-lookup"><span data-stu-id="6aa89-132">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="6aa89-133">C#</span><span class="sxs-lookup"><span data-stu-id="6aa89-133">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="6aa89-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="6aa89-134">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="6aa89-135">Python</span><span class="sxs-lookup"><span data-stu-id="6aa89-135">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="6aa89-136">JSON</span><span class="sxs-lookup"><span data-stu-id="6aa89-136">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="6aa89-137">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="6aa89-137">Send a message</span></span>

<span data-ttu-id="6aa89-138">Чтобы отправить текстовое сообщение, укажите строку, которая будет отправляться в качестве действия.</span><span class="sxs-lookup"><span data-stu-id="6aa89-138">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="6aa89-139">В обработнике действий бота используйте метод объекта контекста поворота для `SendActivityAsync` отправки единого ответа сообщения.</span><span class="sxs-lookup"><span data-stu-id="6aa89-139">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="6aa89-140">Используйте метод объекта `SendActivitiesAsync` для отправки сразу нескольких ответов.</span><span class="sxs-lookup"><span data-stu-id="6aa89-140">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span> <span data-ttu-id="6aa89-141">В следующем коде показан пример отправки сообщения при добавлении пользователя в беседу:</span><span class="sxs-lookup"><span data-stu-id="6aa89-141">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

<span data-ttu-id="6aa89-142">В следующем коде показан пример отправки сообщения:</span><span class="sxs-lookup"><span data-stu-id="6aa89-142">The following code shows an example of sending a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="6aa89-143">C#</span><span class="sxs-lookup"><span data-stu-id="6aa89-143">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="6aa89-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="6aa89-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="6aa89-145">Python</span><span class="sxs-lookup"><span data-stu-id="6aa89-145">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="6aa89-146">JSON</span><span class="sxs-lookup"><span data-stu-id="6aa89-146">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="6aa89-147">Разделение сообщений происходит, когда текстовое сообщение и вложение отправляются в той же полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="6aa89-147">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="6aa89-148">Это действие разделено на отдельные действия Microsoft Teams, одно из них имеет только текстовое сообщение, а другое — с вложением.</span><span class="sxs-lookup"><span data-stu-id="6aa89-148">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="6aa89-149">При разделении действия в ответ не получается ID сообщения, [](~/bots/how-to/update-and-delete-bot-messages.md) который используется для обновления или удаления сообщения.</span><span class="sxs-lookup"><span data-stu-id="6aa89-149">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="6aa89-150">Рекомендуется отправлять отдельные действия, а не в зависимости от разделения сообщений.</span><span class="sxs-lookup"><span data-stu-id="6aa89-150">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="6aa89-151">Сообщения, отправленные между пользователями и ботами, включают внутренние данные канала в сообщении.</span><span class="sxs-lookup"><span data-stu-id="6aa89-151">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="6aa89-152">Эти данные позволяют боту правильно общаться на этом канале.</span><span class="sxs-lookup"><span data-stu-id="6aa89-152">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="6aa89-153">SDK bot Builder позволяет изменять структуру сообщений.</span><span class="sxs-lookup"><span data-stu-id="6aa89-153">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="6aa89-154">Данные канала teams</span><span class="sxs-lookup"><span data-stu-id="6aa89-154">Teams channel data</span></span>

<span data-ttu-id="6aa89-155">Объект содержит сведения, определенные для Teams, и является окончательным источником для кодов `channelData` групп и каналов.</span><span class="sxs-lookup"><span data-stu-id="6aa89-155">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="6aa89-156">Дополнительно можно кэширования и использования этих ID в качестве ключей для локального хранения.</span><span class="sxs-lookup"><span data-stu-id="6aa89-156">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="6aa89-157">В SDK обычно извлекаются важные сведения из объекта, чтобы сделать `TeamsActivityHandler` `channelData` его доступным.</span><span class="sxs-lookup"><span data-stu-id="6aa89-157">The `TeamsActivityHandler` in the SDK typically pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="6aa89-158">Однако вы всегда можете получить доступ к исходным данным `turnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="6aa89-158">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="6aa89-159">Объект не входит в сообщения в личных беседах, так как они проходят за `channelData` пределами канала.</span><span class="sxs-lookup"><span data-stu-id="6aa89-159">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="6aa89-160">Типичный `channelData` объект в действии, отправленного боту, содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="6aa89-160">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="6aa89-161">`eventType`: Тип события Teams передается только в случаях [событий изменения канала.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="6aa89-161">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="6aa89-162">`tenant.id`: ID клиента Azure Active Directory передается во всех контекстах.</span><span class="sxs-lookup"><span data-stu-id="6aa89-162">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="6aa89-163">`team`: Передается только в контекстах каналов, а не в личном чате.</span><span class="sxs-lookup"><span data-stu-id="6aa89-163">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="6aa89-164">`id`: GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="6aa89-164">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="6aa89-165">`name`: Имя команды передается только в случаях [переименования событий команды.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="6aa89-165">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="6aa89-166">`channel`. Передается только в контекстах каналов, когда бот упоминается или для событий в каналах в командах, где был добавлен бот.</span><span class="sxs-lookup"><span data-stu-id="6aa89-166">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="6aa89-167">`id`: GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="6aa89-167">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="6aa89-168">`name`: Имя канала передается только в случаях событий [изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="6aa89-168">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="6aa89-169">`channelData.teamsTeamId`: Обесценилось.</span><span class="sxs-lookup"><span data-stu-id="6aa89-169">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="6aa89-170">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="6aa89-170">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="6aa89-171">`channelData.teamsChannelId`: Обесценилось.</span><span class="sxs-lookup"><span data-stu-id="6aa89-171">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="6aa89-172">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="6aa89-172">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="6aa89-173">Пример объекта channelData (событие channelCreated)</span><span class="sxs-lookup"><span data-stu-id="6aa89-173">Example channelData object (channelCreated event)</span></span>

<span data-ttu-id="6aa89-174">В следующем коде показан пример объекта channelData:</span><span class="sxs-lookup"><span data-stu-id="6aa89-174">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="6aa89-175">Сообщения, полученные от или отправленные боту, могут включать различные типы контента сообщений.</span><span class="sxs-lookup"><span data-stu-id="6aa89-175">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="6aa89-176">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="6aa89-176">Message content</span></span>

<span data-ttu-id="6aa89-177">Бот может отправлять богатый текст, изображения и карточки.</span><span class="sxs-lookup"><span data-stu-id="6aa89-177">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="6aa89-178">Пользователи могут отправлять богатый текст и изображения в бот.</span><span class="sxs-lookup"><span data-stu-id="6aa89-178">Users can send rich text and pictures to your bot.</span></span>

| <span data-ttu-id="6aa89-179">Формат</span><span class="sxs-lookup"><span data-stu-id="6aa89-179">Format</span></span>    | <span data-ttu-id="6aa89-180">От пользователя к боту</span><span class="sxs-lookup"><span data-stu-id="6aa89-180">From user to bot</span></span> | <span data-ttu-id="6aa89-181">От бота к пользователю</span><span class="sxs-lookup"><span data-stu-id="6aa89-181">From bot to user</span></span> | <span data-ttu-id="6aa89-182">Примечания</span><span class="sxs-lookup"><span data-stu-id="6aa89-182">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="6aa89-183">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="6aa89-183">Rich text</span></span> | <span data-ttu-id="6aa89-184">✔</span><span class="sxs-lookup"><span data-stu-id="6aa89-184">✔</span></span>                | <span data-ttu-id="6aa89-185">✔</span><span class="sxs-lookup"><span data-stu-id="6aa89-185">✔</span></span>                |                                                                                         |
| <span data-ttu-id="6aa89-186">Изображения</span><span class="sxs-lookup"><span data-stu-id="6aa89-186">Pictures</span></span>  | <span data-ttu-id="6aa89-187">✔</span><span class="sxs-lookup"><span data-stu-id="6aa89-187">✔</span></span>                | <span data-ttu-id="6aa89-188">✔</span><span class="sxs-lookup"><span data-stu-id="6aa89-188">✔</span></span>                | <span data-ttu-id="6aa89-189">Максимальная 1024×1024 и 1 МБ в формате PNG, JPEG или GIF.</span><span class="sxs-lookup"><span data-stu-id="6aa89-189">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="6aa89-190">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6aa89-190">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="6aa89-191">Карточки</span><span class="sxs-lookup"><span data-stu-id="6aa89-191">Cards</span></span>     | <span data-ttu-id="6aa89-192">✖</span><span class="sxs-lookup"><span data-stu-id="6aa89-192">✖</span></span>                | <span data-ttu-id="6aa89-193">✔</span><span class="sxs-lookup"><span data-stu-id="6aa89-193">✔</span></span>                | <span data-ttu-id="6aa89-194">См. [ссылку на карточку Teams](~/task-modules-and-cards/cards/cards-reference.md) для поддерживаемых карт.</span><span class="sxs-lookup"><span data-stu-id="6aa89-194">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="6aa89-195">Emojis</span><span class="sxs-lookup"><span data-stu-id="6aa89-195">Emojis</span></span>    | <span data-ttu-id="6aa89-196">✖</span><span class="sxs-lookup"><span data-stu-id="6aa89-196">✖</span></span>                | <span data-ttu-id="6aa89-197">✔</span><span class="sxs-lookup"><span data-stu-id="6aa89-197">✔</span></span>                | <span data-ttu-id="6aa89-198">В настоящее время teams поддерживает смайлики с помощью UTF-16, например U+1F600 для ухмыляясь.</span><span class="sxs-lookup"><span data-stu-id="6aa89-198">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="6aa89-199">Вы также можете добавить уведомления в сообщение с помощью `Notification.Alert` свойства.</span><span class="sxs-lookup"><span data-stu-id="6aa89-199">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="6aa89-200">Уведомления о вашем сообщении</span><span class="sxs-lookup"><span data-stu-id="6aa89-200">Notifications to your message</span></span>

<span data-ttu-id="6aa89-201">Уведомления предупреждают пользователей о новых задачах, упоминаниях и комментариях.</span><span class="sxs-lookup"><span data-stu-id="6aa89-201">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="6aa89-202">Эти оповещения связаны с тем, над чем работают пользователи или на что они должны смотреть, вставляя уведомление в канал активности.</span><span class="sxs-lookup"><span data-stu-id="6aa89-202">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="6aa89-203">Чтобы уведомления запускались из сообщения бота, установите свойство `TeamsChannelData` `Notification.Alert` объектов true.</span><span class="sxs-lookup"><span data-stu-id="6aa89-203">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to true.</span></span> <span data-ttu-id="6aa89-204">Вопрос о том, будет ли поднято уведомление, зависит от параметров teams отдельного пользователя, и переопределять эти параметры невозможно.</span><span class="sxs-lookup"><span data-stu-id="6aa89-204">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="6aa89-205">Тип уведомления — это баннер или баннер и электронная почта.</span><span class="sxs-lookup"><span data-stu-id="6aa89-205">The notification type is either a banner or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="6aa89-206">Поле **Сводка** отображает любой текст от пользователя в виде сообщения уведомления в канале.</span><span class="sxs-lookup"><span data-stu-id="6aa89-206">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="6aa89-207">В следующем коде показан пример добавления уведомлений в сообщение:</span><span class="sxs-lookup"><span data-stu-id="6aa89-207">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="6aa89-208">C#</span><span class="sxs-lookup"><span data-stu-id="6aa89-208">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="6aa89-209">TypeScript</span><span class="sxs-lookup"><span data-stu-id="6aa89-209">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="6aa89-210">Python</span><span class="sxs-lookup"><span data-stu-id="6aa89-210">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="6aa89-211">JSON</span><span class="sxs-lookup"><span data-stu-id="6aa89-211">JSON</span></span>](#tab/json)

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

<span data-ttu-id="6aa89-212">Чтобы улучшить сообщение, вы можете включить изображения в качестве вложений к этому сообщению.</span><span class="sxs-lookup"><span data-stu-id="6aa89-212">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="6aa89-213">Сообщения изображений</span><span class="sxs-lookup"><span data-stu-id="6aa89-213">Picture messages</span></span>

<span data-ttu-id="6aa89-214">Изображения отправляются путем добавления вложений в сообщение.</span><span class="sxs-lookup"><span data-stu-id="6aa89-214">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="6aa89-215">Дополнительные сведения о вложениях см. в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)</span><span class="sxs-lookup"><span data-stu-id="6aa89-215">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="6aa89-216">Изображения могут быть не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF.</span><span class="sxs-lookup"><span data-stu-id="6aa89-216">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="6aa89-217">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6aa89-217">Animated GIF is not supported.</span></span>

<span data-ttu-id="6aa89-218">Укажите высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="6aa89-218">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="6aa89-219">При разметки размер изображения по умолчанию составляет 256×256.</span><span class="sxs-lookup"><span data-stu-id="6aa89-219">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="6aa89-220">Например:</span><span class="sxs-lookup"><span data-stu-id="6aa89-220">For example:</span></span>

* <span data-ttu-id="6aa89-221">Использование: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="6aa89-221">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="6aa89-222">Не используйте: `![Duck on a rock](http://aka.ms/Fo983c)` .</span><span class="sxs-lookup"><span data-stu-id="6aa89-222">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="6aa89-223">Беседующий бот может включать адаптивные карты, упрощающие бизнес-процессы.</span><span class="sxs-lookup"><span data-stu-id="6aa89-223">A conversational bot can include adaptive cards that simplify business workflows.</span></span> <span data-ttu-id="6aa89-224">Адаптивные карты предлагают богатые настраиваемые тексты, речь, изображения, кнопки и поля ввода.</span><span class="sxs-lookup"><span data-stu-id="6aa89-224">Adaptive cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="6aa89-225">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="6aa89-225">Adaptive cards</span></span>

<span data-ttu-id="6aa89-226">Адаптивные карты можно авторить в боте и показывать в нескольких приложениях, таких как Teams, веб-сайт и так далее.</span><span class="sxs-lookup"><span data-stu-id="6aa89-226">Adaptive cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="6aa89-227">Дополнительные сведения см. [встраивляющие карточки.](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="6aa89-227">For more information, see [adaptive cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="6aa89-228">В следующем коде показан пример отправки простой адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="6aa89-228">The following code shows an example of sending a simple adaptive card:</span></span>

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

<span data-ttu-id="6aa89-229">Дополнительные информацию о картах и картах в ботах см. в [документации по картам.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="6aa89-229">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

<span data-ttu-id="6aa89-230">Следующий раздел содержит ответы кода состояния на ошибки, созданные из API ботов.</span><span class="sxs-lookup"><span data-stu-id="6aa89-230">The next section provides status code responses for errors generated from Bot APIs.</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="6aa89-231">Ответы на код состояния</span><span class="sxs-lookup"><span data-stu-id="6aa89-231">Status code responses</span></span>

<span data-ttu-id="6aa89-232">Ниже печатаются коды состояния и их код ошибок и значения сообщений:</span><span class="sxs-lookup"><span data-stu-id="6aa89-232">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="6aa89-233">Код состояния</span><span class="sxs-lookup"><span data-stu-id="6aa89-233">Status code</span></span> | <span data-ttu-id="6aa89-234">Код ошибки и значения сообщений</span><span class="sxs-lookup"><span data-stu-id="6aa89-234">Error code and message values</span></span> | <span data-ttu-id="6aa89-235">Описание</span><span class="sxs-lookup"><span data-stu-id="6aa89-235">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="6aa89-236">403</span><span class="sxs-lookup"><span data-stu-id="6aa89-236">403</span></span> | <span data-ttu-id="6aa89-237">**Код:**`ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="6aa89-237">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="6aa89-238">**Сообщение:**"Пользователь заблокировал беседу с ботом".</span><span class="sxs-lookup"><span data-stu-id="6aa89-238">**Message**: "User blocked the conversation with the bot."</span></span> | <span data-ttu-id="6aa89-239">Пользователь заблокировал бот в чате 1:1 или канале с помощью параметров модерации.</span><span class="sxs-lookup"><span data-stu-id="6aa89-239">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="6aa89-240">403</span><span class="sxs-lookup"><span data-stu-id="6aa89-240">403</span></span> | <span data-ttu-id="6aa89-241">**Код:**`BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="6aa89-241">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="6aa89-242">**Сообщение:**"Бот не входит в реестр разговоров".</span><span class="sxs-lookup"><span data-stu-id="6aa89-242">**Message**: "The bot is not part of the conversation roster."</span></span> | <span data-ttu-id="6aa89-243">Бот не является частью беседы.</span><span class="sxs-lookup"><span data-stu-id="6aa89-243">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="6aa89-244">403</span><span class="sxs-lookup"><span data-stu-id="6aa89-244">403</span></span> | <span data-ttu-id="6aa89-245">**Код:**`BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="6aa89-245">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="6aa89-246">**Сообщение:**"Администратор клиента отключил этот бот".</span><span class="sxs-lookup"><span data-stu-id="6aa89-246">**Message**: "The tenant admin disabled this bot."</span></span> | <span data-ttu-id="6aa89-247">Клиент заблокировал бот.</span><span class="sxs-lookup"><span data-stu-id="6aa89-247">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="6aa89-248">401</span><span class="sxs-lookup"><span data-stu-id="6aa89-248">401</span></span> | <span data-ttu-id="6aa89-249">**Код:**`BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="6aa89-249">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="6aa89-250">**Сообщение:**"Регистрация для этого бота не найдена".</span><span class="sxs-lookup"><span data-stu-id="6aa89-250">**Message**: “No registration found for this bot.”</span></span> | <span data-ttu-id="6aa89-251">Регистрация этого бота не была найдена.</span><span class="sxs-lookup"><span data-stu-id="6aa89-251">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="6aa89-252">412</span><span class="sxs-lookup"><span data-stu-id="6aa89-252">412</span></span> | <span data-ttu-id="6aa89-253">**Код:**`PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="6aa89-253">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="6aa89-254">**Сообщение:**"Предварительные условия не удалось, попробуйте еще раз".</span><span class="sxs-lookup"><span data-stu-id="6aa89-254">**Message**: “Precondition failed, please try again.”</span></span> | <span data-ttu-id="6aa89-255">В одной из зависимостей из-за нескольких одновечерных операций в одном разговоре не удалось предварительное условие.</span><span class="sxs-lookup"><span data-stu-id="6aa89-255">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="6aa89-256">404</span><span class="sxs-lookup"><span data-stu-id="6aa89-256">404</span></span> | <span data-ttu-id="6aa89-257">**Код:**`ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="6aa89-257">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="6aa89-258">**Сообщение:**"Беседа не найдена".</span><span class="sxs-lookup"><span data-stu-id="6aa89-258">**Message**: “Conversation not found.”</span></span> | <span data-ttu-id="6aa89-259">Беседа не найдена.</span><span class="sxs-lookup"><span data-stu-id="6aa89-259">The conversation was not found.</span></span> |
| <span data-ttu-id="6aa89-260">413</span><span class="sxs-lookup"><span data-stu-id="6aa89-260">413</span></span> | <span data-ttu-id="6aa89-261">**Код:**`MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="6aa89-261">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="6aa89-262">**Сообщение:**"Размер сообщения слишком большой".</span><span class="sxs-lookup"><span data-stu-id="6aa89-262">**Message**: “Message size too large.”</span></span> | <span data-ttu-id="6aa89-263">Размер входящих запросов был слишком велик.</span><span class="sxs-lookup"><span data-stu-id="6aa89-263">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="6aa89-264">429</span><span class="sxs-lookup"><span data-stu-id="6aa89-264">429</span></span> | <span data-ttu-id="6aa89-265">**Код:**`Throttled`</span><span class="sxs-lookup"><span data-stu-id="6aa89-265">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="6aa89-266">**Сообщение:**"Слишком много запросов".</span><span class="sxs-lookup"><span data-stu-id="6aa89-266">**Message**: “Too many requests.”</span></span> <span data-ttu-id="6aa89-267">Кроме того, возвращается, когда повторить после.</span><span class="sxs-lookup"><span data-stu-id="6aa89-267">Also returns when to retry after.</span></span> | <span data-ttu-id="6aa89-268">Слишком много запросов было отправлено ботом.</span><span class="sxs-lookup"><span data-stu-id="6aa89-268">Too many requests were sent by the bot.</span></span> <span data-ttu-id="6aa89-269">Дополнительные сведения см. в [лимите ставок.](~/bots/how-to/rate-limit.md)</span><span class="sxs-lookup"><span data-stu-id="6aa89-269">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

<span data-ttu-id="6aa89-270">В следующем разделе иллюстрирует простой пример кода, который включает основной поток разговоров в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="6aa89-270">The next section illustrates a simple code sample that incorporates basic conversational flow into a Teams application.</span></span>

## <a name="code-sample"></a><span data-ttu-id="6aa89-271">Пример кода</span><span class="sxs-lookup"><span data-stu-id="6aa89-271">Code sample</span></span>

<span data-ttu-id="6aa89-272">Ниже приводится пример кода для бота для беседы Teams:</span><span class="sxs-lookup"><span data-stu-id="6aa89-272">Following are the code samples for Teams conversation bot:</span></span>

|<span data-ttu-id="6aa89-273">Пример имени</span><span class="sxs-lookup"><span data-stu-id="6aa89-273">Sample name</span></span> | <span data-ttu-id="6aa89-274">Описание</span><span class="sxs-lookup"><span data-stu-id="6aa89-274">Description</span></span> | <span data-ttu-id="6aa89-275">. NETCore</span><span class="sxs-lookup"><span data-stu-id="6aa89-275">.NETCore</span></span> | <span data-ttu-id="6aa89-276">Node.js</span><span class="sxs-lookup"><span data-stu-id="6aa89-276">Node.js</span></span> | <span data-ttu-id="6aa89-277">Python</span><span class="sxs-lookup"><span data-stu-id="6aa89-277">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="6aa89-278">Бот для беседы в Teams</span><span class="sxs-lookup"><span data-stu-id="6aa89-278">Teams conversation bot</span></span> | <span data-ttu-id="6aa89-279">Обработка событий обмена сообщениями и бесед.</span><span class="sxs-lookup"><span data-stu-id="6aa89-279">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="6aa89-280">View</span><span class="sxs-lookup"><span data-stu-id="6aa89-280">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="6aa89-281">View</span><span class="sxs-lookup"><span data-stu-id="6aa89-281">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="6aa89-282">View</span><span class="sxs-lookup"><span data-stu-id="6aa89-282">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="6aa89-283">См. также</span><span class="sxs-lookup"><span data-stu-id="6aa89-283">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6aa89-284">Отправлять активные сообщения</span><span class="sxs-lookup"><span data-stu-id="6aa89-284">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="6aa89-285">Подписка на события беседы</span><span class="sxs-lookup"><span data-stu-id="6aa89-285">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="6aa89-286">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="6aa89-286">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6aa89-287">Меню команд бота</span><span class="sxs-lookup"><span data-stu-id="6aa89-287">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
