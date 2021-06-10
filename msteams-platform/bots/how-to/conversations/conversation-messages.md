---
title: Сообщения в беседах с ботами
description: Описывает способы беседы с Microsoft Teams ботом
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: 5b23e3b2548e3d0eab98fae73d37316063fe60c1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058602"
---
# <a name="messages-in-bot-conversations"></a><span data-ttu-id="44ed0-103">Сообщения в беседах с ботами</span><span class="sxs-lookup"><span data-stu-id="44ed0-103">Messages in bot conversations</span></span>

<span data-ttu-id="44ed0-104">Каждое сообщение в беседе является `Activity` объектом типа `messageType: message` .</span><span class="sxs-lookup"><span data-stu-id="44ed0-104">Each message in a conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="44ed0-105">Когда пользователь отправляет сообщение, Teams отправляет сообщение в бот.</span><span class="sxs-lookup"><span data-stu-id="44ed0-105">When a user sends a message, Teams posts the message to your bot.</span></span> <span data-ttu-id="44ed0-106">Teams отправляет объект JSON в конечную точку обмена сообщениями вашего бота.</span><span class="sxs-lookup"><span data-stu-id="44ed0-106">Teams sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="44ed0-107">Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="44ed0-107">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="44ed0-108">Основные беседы обрабатываются через соединители Bot Framework, единый API REST.</span><span class="sxs-lookup"><span data-stu-id="44ed0-108">Basic conversations are handled through the Bot Framework connector, a single REST API.</span></span> <span data-ttu-id="44ed0-109">Этот API позволяет боту общаться с Teams другими каналами.</span><span class="sxs-lookup"><span data-stu-id="44ed0-109">This API enables your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="44ed0-110">В SDK Bot Builder представлены следующие функции:</span><span class="sxs-lookup"><span data-stu-id="44ed0-110">The Bot Builder SDK provides the following features:</span></span>

* <span data-ttu-id="44ed0-111">Простой доступ к соединители Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="44ed0-111">Easy access to the Bot Framework connector.</span></span>
* <span data-ttu-id="44ed0-112">Дополнительные функции для управления потоком и состоянием беседы.</span><span class="sxs-lookup"><span data-stu-id="44ed0-112">Additional functionality to manage conversation flow and state.</span></span>
* <span data-ttu-id="44ed0-113">Простые способы включения когнитивных служб, таких как обработка естественного языка (NLP).</span><span class="sxs-lookup"><span data-stu-id="44ed0-113">Simple ways to incorporate cognitive services, such as natural language processing (NLP).</span></span>

<span data-ttu-id="44ed0-114">Ваш бот получает сообщения из Teams с помощью свойства и отправляет пользователям одиночные или несколько `Text` ответов на сообщения.</span><span class="sxs-lookup"><span data-stu-id="44ed0-114">Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.</span></span>

## <a name="receive-a-message"></a><span data-ttu-id="44ed0-115">Получение сообщения</span><span class="sxs-lookup"><span data-stu-id="44ed0-115">Receive a message</span></span>

<span data-ttu-id="44ed0-116">Чтобы получить текстовое сообщение, используйте свойство `Text` объекта `Activity`.</span><span class="sxs-lookup"><span data-stu-id="44ed0-116">To receive a text message, use the `Text` property of the `Activity` object.</span></span> <span data-ttu-id="44ed0-117">В обработчике активности бота используйте объект контекста поворота `Activity` для чтения одного запроса сообщения.</span><span class="sxs-lookup"><span data-stu-id="44ed0-117">In the bot's activity handler, use the turn context object's `Activity` to read a single message request.</span></span>

<span data-ttu-id="44ed0-118">В следующем коде показан пример получения сообщения:</span><span class="sxs-lookup"><span data-stu-id="44ed0-118">The following code shows an example of receiving a message:</span></span>

# <a name="c"></a>[<span data-ttu-id="44ed0-119">C#</span><span class="sxs-lookup"><span data-stu-id="44ed0-119">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="44ed0-120">TypeScript</span><span class="sxs-lookup"><span data-stu-id="44ed0-120">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="44ed0-121">Python</span><span class="sxs-lookup"><span data-stu-id="44ed0-121">Python</span></span>](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[<span data-ttu-id="44ed0-122">JSON</span><span class="sxs-lookup"><span data-stu-id="44ed0-122">JSON</span></span>](#tab/json)

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

## <a name="send-a-message"></a><span data-ttu-id="44ed0-123">Отправка сообщения</span><span class="sxs-lookup"><span data-stu-id="44ed0-123">Send a message</span></span>

<span data-ttu-id="44ed0-124">Чтобы отправить текстовое сообщение, укажите строку, которая будет отправляться в качестве действия.</span><span class="sxs-lookup"><span data-stu-id="44ed0-124">To send a text message, specify the string you want to send as the activity.</span></span> <span data-ttu-id="44ed0-125">В обработнике действий бота используйте метод объекта контекста поворота для `SendActivityAsync` отправки единого ответа сообщения.</span><span class="sxs-lookup"><span data-stu-id="44ed0-125">In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response.</span></span> <span data-ttu-id="44ed0-126">Используйте метод объекта `SendActivitiesAsync` для отправки сразу нескольких ответов.</span><span class="sxs-lookup"><span data-stu-id="44ed0-126">Use the object's `SendActivitiesAsync` method to send multiple responses at once.</span></span>

<span data-ttu-id="44ed0-127">В следующем коде показан пример отправки сообщения при добавлении пользователя в беседу:</span><span class="sxs-lookup"><span data-stu-id="44ed0-127">The following code shows an example of sending a message when a user is added to a conversation:</span></span>

# <a name="c"></a>[<span data-ttu-id="44ed0-128">C#</span><span class="sxs-lookup"><span data-stu-id="44ed0-128">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[<span data-ttu-id="44ed0-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="44ed0-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="44ed0-130">Python</span><span class="sxs-lookup"><span data-stu-id="44ed0-130">Python</span></span>](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[<span data-ttu-id="44ed0-131">JSON</span><span class="sxs-lookup"><span data-stu-id="44ed0-131">JSON</span></span>](#tab/json)

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
> <span data-ttu-id="44ed0-132">Разделение сообщений происходит, когда текстовое сообщение и вложение отправляются в той же полезной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="44ed0-132">Message splitting occurs when a text message and an attachment are sent in the same activity payload.</span></span> <span data-ttu-id="44ed0-133">Это действие делится на отдельные действия по Microsoft Teams, одно с текстовым сообщением, а другое с вложением.</span><span class="sxs-lookup"><span data-stu-id="44ed0-133">This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment.</span></span> <span data-ttu-id="44ed0-134">При разделении действия в ответ не получается ID сообщения, [](~/bots/how-to/update-and-delete-bot-messages.md) который используется для обновления или удаления сообщения.</span><span class="sxs-lookup"><span data-stu-id="44ed0-134">As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively.</span></span> <span data-ttu-id="44ed0-135">Рекомендуется отправлять отдельные действия, а не в зависимости от разделения сообщений.</span><span class="sxs-lookup"><span data-stu-id="44ed0-135">It is recommended to send separate activities instead of depending on message splitting.</span></span>

<span data-ttu-id="44ed0-136">Сообщения, отправленные между пользователями и ботами, включают внутренние данные канала в сообщении.</span><span class="sxs-lookup"><span data-stu-id="44ed0-136">Messages sent between users and bots include internal channel data within the message.</span></span> <span data-ttu-id="44ed0-137">Эти данные позволяют боту правильно общаться на этом канале.</span><span class="sxs-lookup"><span data-stu-id="44ed0-137">This data allows the bot to communicate properly on that channel.</span></span> <span data-ttu-id="44ed0-138">SDK bot Builder позволяет изменять структуру сообщений.</span><span class="sxs-lookup"><span data-stu-id="44ed0-138">The Bot Builder SDK allows you to modify the message structure.</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="44ed0-139">Teams каналов</span><span class="sxs-lookup"><span data-stu-id="44ed0-139">Teams channel data</span></span>

<span data-ttu-id="44ed0-140">Объект содержит Teams и является окончательным источником для кодов группы и `channelData` канала.</span><span class="sxs-lookup"><span data-stu-id="44ed0-140">The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs.</span></span> <span data-ttu-id="44ed0-141">Дополнительно можно кэширования и использования этих ID в качестве ключей для локального хранения.</span><span class="sxs-lookup"><span data-stu-id="44ed0-141">Optionally, you can cache and use these IDs as keys for local storage.</span></span> <span data-ttu-id="44ed0-142">SDK извлекет важные сведения из объекта, чтобы сделать его `TeamsActivityHandler` `channelData` доступным.</span><span class="sxs-lookup"><span data-stu-id="44ed0-142">The `TeamsActivityHandler` in the SDK pulls out important information from the `channelData` object to make it easily accessible.</span></span> <span data-ttu-id="44ed0-143">Однако вы всегда можете получить доступ к исходным данным `turnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="44ed0-143">However, you can always access the original data from the `turnContext` object.</span></span>

<span data-ttu-id="44ed0-144">Объект не входит в сообщения в личных беседах, так как они проходят за `channelData` пределами канала.</span><span class="sxs-lookup"><span data-stu-id="44ed0-144">The `channelData` object is not included in messages in personal conversations, as these take place outside of a channel.</span></span>

<span data-ttu-id="44ed0-145">Типичный `channelData` объект в действии, отправленного боту, содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="44ed0-145">A typical `channelData` object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="44ed0-146">`eventType`: Teams тип события передается только в случаях [событий изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="44ed0-146">`eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="44ed0-147">`tenant.id`: Azure Active Directory клиента, переданный во всех контекстах.</span><span class="sxs-lookup"><span data-stu-id="44ed0-147">`tenant.id`: Azure Active Directory tenant ID passed in all contexts.</span></span>
* <span data-ttu-id="44ed0-148">`team`: Передается только в контекстах каналов, а не в личном чате.</span><span class="sxs-lookup"><span data-stu-id="44ed0-148">`team`: Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="44ed0-149">`id`: GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="44ed0-149">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="44ed0-150">`name`: Имя команды передается только в случаях [переименования событий команды.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)</span><span class="sxs-lookup"><span data-stu-id="44ed0-150">`name`: Name of the team passed only in cases of [team rename events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="44ed0-151">`channel`. Передается только в контекстах каналов, когда бот упоминается или для событий в каналах в командах, где был добавлен бот.</span><span class="sxs-lookup"><span data-stu-id="44ed0-151">`channel`: Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="44ed0-152">`id`: GUID для канала.</span><span class="sxs-lookup"><span data-stu-id="44ed0-152">`id`: GUID for the channel.</span></span>
  * <span data-ttu-id="44ed0-153">`name`: Имя канала передается только в случаях событий [изменения канала](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span><span class="sxs-lookup"><span data-stu-id="44ed0-153">`name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).</span></span>
* <span data-ttu-id="44ed0-154">`channelData.teamsTeamId`: Обесценилось.</span><span class="sxs-lookup"><span data-stu-id="44ed0-154">`channelData.teamsTeamId`: Deprecated.</span></span> <span data-ttu-id="44ed0-155">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="44ed0-155">This property is only included for backward compatibility.</span></span>
* <span data-ttu-id="44ed0-156">`channelData.teamsChannelId`: Обесценилось.</span><span class="sxs-lookup"><span data-stu-id="44ed0-156">`channelData.teamsChannelId`: Deprecated.</span></span> <span data-ttu-id="44ed0-157">Это свойство включено только для обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="44ed0-157">This property is only included for backward compatibility.</span></span>

### <a name="example-channeldata-object-or-channelcreated-event"></a><span data-ttu-id="44ed0-158">Пример объекта channelData или события channelCreated</span><span class="sxs-lookup"><span data-stu-id="44ed0-158">Example channelData object or channelCreated event</span></span>

<span data-ttu-id="44ed0-159">В следующем коде показан пример объекта channelData:</span><span class="sxs-lookup"><span data-stu-id="44ed0-159">The following code shows an example of channelData object:</span></span>

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

<span data-ttu-id="44ed0-160">Сообщения, полученные от или отправленные боту, могут включать различные типы контента сообщений.</span><span class="sxs-lookup"><span data-stu-id="44ed0-160">Messages received from or sent to your bot can include different types of message content.</span></span>

## <a name="message-content"></a><span data-ttu-id="44ed0-161">Содержимое сообщения</span><span class="sxs-lookup"><span data-stu-id="44ed0-161">Message content</span></span>

| <span data-ttu-id="44ed0-162">Формат</span><span class="sxs-lookup"><span data-stu-id="44ed0-162">Format</span></span>    | <span data-ttu-id="44ed0-163">От пользователя к боту</span><span class="sxs-lookup"><span data-stu-id="44ed0-163">From user to bot</span></span> | <span data-ttu-id="44ed0-164">От бота к пользователю</span><span class="sxs-lookup"><span data-stu-id="44ed0-164">From bot to user</span></span> | <span data-ttu-id="44ed0-165">Примечания</span><span class="sxs-lookup"><span data-stu-id="44ed0-165">Notes</span></span>                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| <span data-ttu-id="44ed0-166">Форматированный текст </span><span class="sxs-lookup"><span data-stu-id="44ed0-166">Rich text</span></span> | <span data-ttu-id="44ed0-167">✔</span><span class="sxs-lookup"><span data-stu-id="44ed0-167">✔</span></span>                | <span data-ttu-id="44ed0-168">✔</span><span class="sxs-lookup"><span data-stu-id="44ed0-168">✔</span></span>                | <span data-ttu-id="44ed0-169">Бот может отправлять богатый текст, изображения и карточки.</span><span class="sxs-lookup"><span data-stu-id="44ed0-169">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="44ed0-170">Пользователи могут отправлять богатый текст и изображения в бот.</span><span class="sxs-lookup"><span data-stu-id="44ed0-170">Users can send rich text and pictures to your bot.</span></span>                                                                                        |
| <span data-ttu-id="44ed0-171">Изображения</span><span class="sxs-lookup"><span data-stu-id="44ed0-171">Pictures</span></span>  | <span data-ttu-id="44ed0-172">✔</span><span class="sxs-lookup"><span data-stu-id="44ed0-172">✔</span></span>                | <span data-ttu-id="44ed0-173">✔</span><span class="sxs-lookup"><span data-stu-id="44ed0-173">✔</span></span>                | <span data-ttu-id="44ed0-174">Максимальная 1024×1024 и 1 МБ в формате PNG, JPEG или GIF.</span><span class="sxs-lookup"><span data-stu-id="44ed0-174">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="44ed0-175">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="44ed0-175">Animated GIF is not supported.</span></span>  |
| <span data-ttu-id="44ed0-176">Карточки</span><span class="sxs-lookup"><span data-stu-id="44ed0-176">Cards</span></span>     | <span data-ttu-id="44ed0-177">✖</span><span class="sxs-lookup"><span data-stu-id="44ed0-177">✖</span></span>                | <span data-ttu-id="44ed0-178">✔</span><span class="sxs-lookup"><span data-stu-id="44ed0-178">✔</span></span>                | <span data-ttu-id="44ed0-179">См. [ссылку Teams для](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемых карт.</span><span class="sxs-lookup"><span data-stu-id="44ed0-179">See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="44ed0-180">Emojis</span><span class="sxs-lookup"><span data-stu-id="44ed0-180">Emojis</span></span>    | <span data-ttu-id="44ed0-181">✖</span><span class="sxs-lookup"><span data-stu-id="44ed0-181">✖</span></span>                | <span data-ttu-id="44ed0-182">✔</span><span class="sxs-lookup"><span data-stu-id="44ed0-182">✔</span></span>                | <span data-ttu-id="44ed0-183">Teams поддерживает смайлики через UTF-16, например U+1F600 для ухмыляясь.</span><span class="sxs-lookup"><span data-stu-id="44ed0-183">Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face.</span></span> |

<span data-ttu-id="44ed0-184">Вы также можете добавить уведомления в сообщение с помощью `Notification.Alert` свойства.</span><span class="sxs-lookup"><span data-stu-id="44ed0-184">You can also add notifications to your message using the `Notification.Alert` property.</span></span>

## <a name="notifications-to-your-message"></a><span data-ttu-id="44ed0-185">Уведомления о вашем сообщении</span><span class="sxs-lookup"><span data-stu-id="44ed0-185">Notifications to your message</span></span>

<span data-ttu-id="44ed0-186">Уведомления предупреждают пользователей о новых задачах, упоминаниях и комментариях.</span><span class="sxs-lookup"><span data-stu-id="44ed0-186">Notifications alert users about new tasks, mentions, and comments.</span></span> <span data-ttu-id="44ed0-187">Эти оповещения связаны с тем, над чем работают пользователи или на что они должны смотреть, вставляя уведомление в канал активности.</span><span class="sxs-lookup"><span data-stu-id="44ed0-187">These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed.</span></span> <span data-ttu-id="44ed0-188">Чтобы уведомления запускались из сообщения бота, установите свойство `TeamsChannelData` `Notification.Alert` объектов true . </span><span class="sxs-lookup"><span data-stu-id="44ed0-188">For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to *true*.</span></span> <span data-ttu-id="44ed0-189">Вопрос о том, будет ли поднято уведомление, зависит от параметров Teams пользователя, и переопределять эти параметры невозможно.</span><span class="sxs-lookup"><span data-stu-id="44ed0-189">Whether or not a notification is raised depends on the individual user's Teams settings and you cannot override these settings.</span></span> <span data-ttu-id="44ed0-190">Тип уведомления — это либо баннер, либо баннер и электронная почта.</span><span class="sxs-lookup"><span data-stu-id="44ed0-190">The notification type is either a banner, or both a banner and an email.</span></span>

> [!NOTE]
> <span data-ttu-id="44ed0-191">Поле **Сводка** отображает любой текст от пользователя в виде сообщения уведомления в канале.</span><span class="sxs-lookup"><span data-stu-id="44ed0-191">The **Summary** field displays any text from the user as a notification message in the feed.</span></span>

<span data-ttu-id="44ed0-192">В следующем коде показан пример добавления уведомлений в сообщение:</span><span class="sxs-lookup"><span data-stu-id="44ed0-192">The following code shows an example of adding notifications to your message:</span></span>

# <a name="c"></a>[<span data-ttu-id="44ed0-193">C#</span><span class="sxs-lookup"><span data-stu-id="44ed0-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[<span data-ttu-id="44ed0-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="44ed0-194">TypeScript</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[<span data-ttu-id="44ed0-195">Python</span><span class="sxs-lookup"><span data-stu-id="44ed0-195">Python</span></span>](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[<span data-ttu-id="44ed0-196">JSON</span><span class="sxs-lookup"><span data-stu-id="44ed0-196">JSON</span></span>](#tab/json)

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

<span data-ttu-id="44ed0-197">Чтобы улучшить сообщение, вы можете включить изображения в качестве вложений к этому сообщению.</span><span class="sxs-lookup"><span data-stu-id="44ed0-197">To enhance your message, you can include pictures as attachments to that message.</span></span>

## <a name="picture-messages"></a><span data-ttu-id="44ed0-198">Сообщения изображений</span><span class="sxs-lookup"><span data-stu-id="44ed0-198">Picture messages</span></span>

<span data-ttu-id="44ed0-199">Изображения отправляются путем добавления вложений в сообщение.</span><span class="sxs-lookup"><span data-stu-id="44ed0-199">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="44ed0-200">Дополнительные сведения о вложениях см. в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)</span><span class="sxs-lookup"><span data-stu-id="44ed0-200">For more information on attachments, see [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).</span></span>

<span data-ttu-id="44ed0-201">Изображения могут быть не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF.</span><span class="sxs-lookup"><span data-stu-id="44ed0-201">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="44ed0-202">Анимированный GIF не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="44ed0-202">Animated GIF is not supported.</span></span>

<span data-ttu-id="44ed0-203">Укажите высоту и ширину каждого изображения с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="44ed0-203">Specify the height and width of each image by using XML.</span></span> <span data-ttu-id="44ed0-204">При разметки размер изображения по умолчанию составляет 256×256.</span><span class="sxs-lookup"><span data-stu-id="44ed0-204">In markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="44ed0-205">Пример.</span><span class="sxs-lookup"><span data-stu-id="44ed0-205">For example:</span></span>

* <span data-ttu-id="44ed0-206">Использование: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` .</span><span class="sxs-lookup"><span data-stu-id="44ed0-206">Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.</span></span>
* <span data-ttu-id="44ed0-207">Не используйте: `![Duck on a rock](http://aka.ms/Fo983c)` .</span><span class="sxs-lookup"><span data-stu-id="44ed0-207">Do not use: `![Duck on a rock](http://aka.ms/Fo983c)`.</span></span>

<span data-ttu-id="44ed0-208">Разговорный бот может включать адаптивные карты, упрощающие бизнес-процессы.</span><span class="sxs-lookup"><span data-stu-id="44ed0-208">A conversational bot can include Adaptive Cards that simplify business workflows.</span></span> <span data-ttu-id="44ed0-209">Адаптивные карты предлагают богатые настраиваемые тексты, речь, изображения, кнопки и поля ввода.</span><span class="sxs-lookup"><span data-stu-id="44ed0-209">Adaptive Cards offer rich customizable text, speech, images, buttons, and input fields.</span></span>

## <a name="adaptive-cards"></a><span data-ttu-id="44ed0-210">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="44ed0-210">Adaptive Cards</span></span>

<span data-ttu-id="44ed0-211">Адаптивные карты можно авторить в боте и показывать в нескольких приложениях, таких как Teams, веб-сайт и так далее.</span><span class="sxs-lookup"><span data-stu-id="44ed0-211">Adaptive Cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on.</span></span> <span data-ttu-id="44ed0-212">Дополнительные сведения см. в [дополнительных сведениях в адаптивных картах.](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)</span><span class="sxs-lookup"><span data-stu-id="44ed0-212">For more information, see [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>

<span data-ttu-id="44ed0-213">В следующем коде показан пример отправки простой адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="44ed0-213">The following code shows an example of sending a simple Adaptive Card:</span></span>

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

<span data-ttu-id="44ed0-214">Дополнительные информацию о картах и картах в ботах см. в [документации по картам.](~/task-modules-and-cards/what-are-cards.md)</span><span class="sxs-lookup"><span data-stu-id="44ed0-214">To know more about cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="status-code-responses"></a><span data-ttu-id="44ed0-215">Ответы на код состояния</span><span class="sxs-lookup"><span data-stu-id="44ed0-215">Status code responses</span></span>

<span data-ttu-id="44ed0-216">Ниже печатаются коды состояния и их код ошибок и значения сообщений:</span><span class="sxs-lookup"><span data-stu-id="44ed0-216">Following are the status codes and their error code and message values:</span></span>

| <span data-ttu-id="44ed0-217">Код состояния</span><span class="sxs-lookup"><span data-stu-id="44ed0-217">Status code</span></span> | <span data-ttu-id="44ed0-218">Код ошибки и значения сообщений</span><span class="sxs-lookup"><span data-stu-id="44ed0-218">Error code and message values</span></span> | <span data-ttu-id="44ed0-219">Описание</span><span class="sxs-lookup"><span data-stu-id="44ed0-219">Description</span></span> |
|----------------|-----------------|-----------------|
| <span data-ttu-id="44ed0-220">403</span><span class="sxs-lookup"><span data-stu-id="44ed0-220">403</span></span> | <span data-ttu-id="44ed0-221">**Код:**`ConversationBlockedByUser`</span><span class="sxs-lookup"><span data-stu-id="44ed0-221">**Code**: `ConversationBlockedByUser`</span></span> <br/> <span data-ttu-id="44ed0-222">**Сообщение.** Пользователь заблокировал беседу с ботом.</span><span class="sxs-lookup"><span data-stu-id="44ed0-222">**Message**: User blocked the conversation with the bot.</span></span> | <span data-ttu-id="44ed0-223">Пользователь заблокировал бот в чате 1:1 или канале с помощью параметров модерации.</span><span class="sxs-lookup"><span data-stu-id="44ed0-223">User blocked the bot in 1:1 chat or a channel through moderation settings.</span></span> |
| <span data-ttu-id="44ed0-224">403</span><span class="sxs-lookup"><span data-stu-id="44ed0-224">403</span></span> | <span data-ttu-id="44ed0-225">**Код:**`BotNotInConversationRoster`</span><span class="sxs-lookup"><span data-stu-id="44ed0-225">**Code**: `BotNotInConversationRoster`</span></span> <br/> <span data-ttu-id="44ed0-226">**Сообщение.** Бот не является частью реестра беседы.</span><span class="sxs-lookup"><span data-stu-id="44ed0-226">**Message**: The bot is not part of the conversation roster.</span></span> | <span data-ttu-id="44ed0-227">Бот не является частью беседы.</span><span class="sxs-lookup"><span data-stu-id="44ed0-227">The bot is not part of the conversation.</span></span> |
| <span data-ttu-id="44ed0-228">403</span><span class="sxs-lookup"><span data-stu-id="44ed0-228">403</span></span> | <span data-ttu-id="44ed0-229">**Код:**`BotDisabledByAdmin`</span><span class="sxs-lookup"><span data-stu-id="44ed0-229">**Code**: `BotDisabledByAdmin`</span></span> <br/> <span data-ttu-id="44ed0-230">**Сообщение.** Администратор клиента отключил этот бот.</span><span class="sxs-lookup"><span data-stu-id="44ed0-230">**Message**: The tenant admin disabled this bot.</span></span> | <span data-ttu-id="44ed0-231">Клиент заблокировал бот.</span><span class="sxs-lookup"><span data-stu-id="44ed0-231">Tenant blocked the bot.</span></span> |
| <span data-ttu-id="44ed0-232">401</span><span class="sxs-lookup"><span data-stu-id="44ed0-232">401</span></span> | <span data-ttu-id="44ed0-233">**Код:**`BotNotRegistered`</span><span class="sxs-lookup"><span data-stu-id="44ed0-233">**Code**: `BotNotRegistered`</span></span> <br/> <span data-ttu-id="44ed0-234">**Сообщение.** Регистрация для этого бота не найдена.</span><span class="sxs-lookup"><span data-stu-id="44ed0-234">**Message**: No registration found for this bot.</span></span> | <span data-ttu-id="44ed0-235">Регистрация этого бота не была найдена.</span><span class="sxs-lookup"><span data-stu-id="44ed0-235">The registration for this bot was not found.</span></span> |
| <span data-ttu-id="44ed0-236">412</span><span class="sxs-lookup"><span data-stu-id="44ed0-236">412</span></span> | <span data-ttu-id="44ed0-237">**Код:**`PreconditionFailed`</span><span class="sxs-lookup"><span data-stu-id="44ed0-237">**Code**: `PreconditionFailed`</span></span> <br/> <span data-ttu-id="44ed0-238">**Сообщение.** Предварительные условия не удалось, попробуйте еще раз.</span><span class="sxs-lookup"><span data-stu-id="44ed0-238">**Message**: Precondition failed, please try again.</span></span> | <span data-ttu-id="44ed0-239">В одной из зависимостей из-за нескольких одновечерных операций в одном разговоре не удалось предварительное условие.</span><span class="sxs-lookup"><span data-stu-id="44ed0-239">A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation.</span></span> |
| <span data-ttu-id="44ed0-240">404</span><span class="sxs-lookup"><span data-stu-id="44ed0-240">404</span></span> | <span data-ttu-id="44ed0-241">**Код:**`ConversationNotFound`</span><span class="sxs-lookup"><span data-stu-id="44ed0-241">**Code**: `ConversationNotFound`</span></span> <br/> <span data-ttu-id="44ed0-242">**Сообщение.** Беседа не найдена.</span><span class="sxs-lookup"><span data-stu-id="44ed0-242">**Message**: Conversation not found.</span></span> | <span data-ttu-id="44ed0-243">Беседа не найдена.</span><span class="sxs-lookup"><span data-stu-id="44ed0-243">The conversation was not found.</span></span> |
| <span data-ttu-id="44ed0-244">413</span><span class="sxs-lookup"><span data-stu-id="44ed0-244">413</span></span> | <span data-ttu-id="44ed0-245">**Код:**`MessageSizeTooBig`</span><span class="sxs-lookup"><span data-stu-id="44ed0-245">**Code**: `MessageSizeTooBig`</span></span> <br/> <span data-ttu-id="44ed0-246">**Сообщение.** Слишком большой размер сообщения.</span><span class="sxs-lookup"><span data-stu-id="44ed0-246">**Message**: Message size too large.</span></span> | <span data-ttu-id="44ed0-247">Размер входящих запросов был слишком велик.</span><span class="sxs-lookup"><span data-stu-id="44ed0-247">The size on the incoming request was too large.</span></span> |
| <span data-ttu-id="44ed0-248">429</span><span class="sxs-lookup"><span data-stu-id="44ed0-248">429</span></span> | <span data-ttu-id="44ed0-249">**Код:**`Throttled`</span><span class="sxs-lookup"><span data-stu-id="44ed0-249">**Code**: `Throttled`</span></span> <br/> <span data-ttu-id="44ed0-250">**Сообщение.** Слишком много запросов.</span><span class="sxs-lookup"><span data-stu-id="44ed0-250">**Message**: Too many requests.</span></span> <span data-ttu-id="44ed0-251">Кроме того, возвращается, когда повторить после.</span><span class="sxs-lookup"><span data-stu-id="44ed0-251">Also returns when to retry after.</span></span> | <span data-ttu-id="44ed0-252">Слишком много запросов было отправлено ботом.</span><span class="sxs-lookup"><span data-stu-id="44ed0-252">Too many requests were sent by the bot.</span></span> <span data-ttu-id="44ed0-253">Дополнительные сведения см. в [лимите ставок.](~/bots/how-to/rate-limit.md)</span><span class="sxs-lookup"><span data-stu-id="44ed0-253">For more information, see [rate limit](~/bots/how-to/rate-limit.md).</span></span> |

## <a name="code-sample"></a><span data-ttu-id="44ed0-254">Пример кода</span><span class="sxs-lookup"><span data-stu-id="44ed0-254">Code sample</span></span>

|<span data-ttu-id="44ed0-255">Пример имени</span><span class="sxs-lookup"><span data-stu-id="44ed0-255">Sample name</span></span> | <span data-ttu-id="44ed0-256">Описание</span><span class="sxs-lookup"><span data-stu-id="44ed0-256">Description</span></span> | <span data-ttu-id="44ed0-257">. NETCore</span><span class="sxs-lookup"><span data-stu-id="44ed0-257">.NETCore</span></span> | <span data-ttu-id="44ed0-258">Node.js</span><span class="sxs-lookup"><span data-stu-id="44ed0-258">Node.js</span></span> | <span data-ttu-id="44ed0-259">Python</span><span class="sxs-lookup"><span data-stu-id="44ed0-259">Python</span></span> |
|----------------|-----------------|--------------|----------------|-----------|
| <span data-ttu-id="44ed0-260">Бот для беседы в Teams</span><span class="sxs-lookup"><span data-stu-id="44ed0-260">Teams conversation bot</span></span> | <span data-ttu-id="44ed0-261">Обработка событий обмена сообщениями и бесед.</span><span class="sxs-lookup"><span data-stu-id="44ed0-261">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="44ed0-262">View</span><span class="sxs-lookup"><span data-stu-id="44ed0-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="44ed0-263">View</span><span class="sxs-lookup"><span data-stu-id="44ed0-263">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [<span data-ttu-id="44ed0-264">View</span><span class="sxs-lookup"><span data-stu-id="44ed0-264">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="see-also"></a><span data-ttu-id="44ed0-265">См. также</span><span class="sxs-lookup"><span data-stu-id="44ed0-265">See also</span></span>

- [<span data-ttu-id="44ed0-266">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="44ed0-266">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)

- [<span data-ttu-id="44ed0-267">Подписка на события беседы</span><span class="sxs-lookup"><span data-stu-id="44ed0-267">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="next-step"></a><span data-ttu-id="44ed0-268">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="44ed0-268">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="44ed0-269">Меню команд бота</span><span class="sxs-lookup"><span data-stu-id="44ed0-269">Bot command menus</span></span>](~/bots/how-to/create-a-bot-commands-menu.md)
