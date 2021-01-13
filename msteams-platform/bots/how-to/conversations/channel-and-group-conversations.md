---
title: Каналы и групповые беседы с ботом
author: clearab
description: Отправка, получение и обработка сообщений для бота в канале или групповом чате.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797843"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="7f22a-103">Беседы в каналах и групповых чатах с помощью бота Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7f22a-103">Channel and group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="7f22a-104">Добавляя область или область в бот, ее можно установить в групповом или `teams` `groupchat` командном чате.</span><span class="sxs-lookup"><span data-stu-id="7f22a-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="7f22a-105">Это позволяет всем участникам беседы взаимодействовать с ботом.</span><span class="sxs-lookup"><span data-stu-id="7f22a-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="7f22a-106">После установки он также получит доступ к метаданным беседы, например к списку участников беседы, а также при установке в команде сведений о команде и полного списка каналов.</span><span class="sxs-lookup"><span data-stu-id="7f22a-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="7f22a-107">Боты в группе или канале получают сообщения, только когда они упоминаются (@botname), они не получают других сообщений, отправленных в беседу.</span><span class="sxs-lookup"><span data-stu-id="7f22a-107">Bots in a group or channel only receive messages when they are mentioned (@botname), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="7f22a-108">Бот должен быть @mentioned непосредственно.</span><span class="sxs-lookup"><span data-stu-id="7f22a-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="7f22a-109">Бот не получит сообщение, если команда или канал упомянуты, или когда кто-то отвечает на сообщение от вашего бота, не @mentioning его.</span><span class="sxs-lookup"><span data-stu-id="7f22a-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="7f22a-110">Рекомендации по дизайну</span><span class="sxs-lookup"><span data-stu-id="7f22a-110">Design guidelines</span></span>

<span data-ttu-id="7f22a-111">Узнайте, как [разработать беседы ботов в каналах и чатах.](~/bots/design/bots.md)</span><span class="sxs-lookup"><span data-stu-id="7f22a-111">See how to [design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="7f22a-112">Создание новых потоков беседы</span><span class="sxs-lookup"><span data-stu-id="7f22a-112">Creating new conversation threads</span></span>

<span data-ttu-id="7f22a-113">При установке бота в команде иногда может быть необходимо создать цепочку бесед, а не отвечать на существующий.</span><span class="sxs-lookup"><span data-stu-id="7f22a-113">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="7f22a-114">Это форма упреждающего [обмена сообщениями.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="7f22a-114">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="7f22a-115">Работа с упоминаниями</span><span class="sxs-lookup"><span data-stu-id="7f22a-115">Working with mentions</span></span>

<span data-ttu-id="7f22a-116">Каждое сообщение, отобратое боту из группы или канала, будет содержать @mention с собственным именем в тексте сообщения, поэтому вам потребуется убедиться, что личные работки обработки сообщений обрабатываются таким образом.</span><span class="sxs-lookup"><span data-stu-id="7f22a-116">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="7f22a-117">Бот также может получить других пользователей, упомянутых в сообщении, и добавить упоминания в любые отправляемые сообщения.</span><span class="sxs-lookup"><span data-stu-id="7f22a-117">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="7f22a-118">Замещение упоминаний из текста сообщения</span><span class="sxs-lookup"><span data-stu-id="7f22a-118">Stripping mentions from message text</span></span>

<span data-ttu-id="7f22a-119">Возможно, вам потребуется @mentions из текста сообщения, которое получает бот.</span><span class="sxs-lookup"><span data-stu-id="7f22a-119">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="7f22a-120">Искомые упоминания</span><span class="sxs-lookup"><span data-stu-id="7f22a-120">Retrieving mentions</span></span>

<span data-ttu-id="7f22a-121">Упоминания возвращаются в объекте в полезной нагрузке и содержат как уникальный ИД пользователя, так и, в большинстве случаев, имя `entities` упомянутого пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f22a-121">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="7f22a-122">Текст сообщения также будет включать упоминание, например `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="7f22a-122">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="7f22a-123">Однако не следует полагаться на текст в сообщении для получения каких-либо сведений о пользователе; отправляя сообщение, он может изменить его.</span><span class="sxs-lookup"><span data-stu-id="7f22a-123">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="7f22a-124">Вместо этого используйте `entities` объект.</span><span class="sxs-lookup"><span data-stu-id="7f22a-124">Instead, use the `entities` object.</span></span>

<span data-ttu-id="7f22a-125">Вы можете получить все упоминания в сообщении, вызывая функцию в SDK построитель ботов, которая возвращает `GetMentions` массив `Mention` объектов.</span><span class="sxs-lookup"><span data-stu-id="7f22a-125">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f22a-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f22a-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7f22a-127">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7f22a-127">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="7f22a-128">JSON</span><span class="sxs-lookup"><span data-stu-id="7f22a-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="7f22a-129">Python</span><span class="sxs-lookup"><span data-stu-id="7f22a-129">Python</span></span>](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="7f22a-130">Добавление упоминаний в сообщения</span><span class="sxs-lookup"><span data-stu-id="7f22a-130">Adding mentions to your messages</span></span>

<span data-ttu-id="7f22a-131">Бот может упоминать других пользователей в сообщениях, которые были опубликованы в каналах.</span><span class="sxs-lookup"><span data-stu-id="7f22a-131">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="7f22a-132">Для этого ваше сообщение должно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="7f22a-132">To do this, your message must do the following:</span></span>

<span data-ttu-id="7f22a-133">У `Mention` объекта есть два свойства, которые необходимо настроить:</span><span class="sxs-lookup"><span data-stu-id="7f22a-133">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="7f22a-134">Включить <at>@username</at> в текст сообщения</span><span class="sxs-lookup"><span data-stu-id="7f22a-134">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="7f22a-135">Включить объект упоминания в коллекцию сущностями</span><span class="sxs-lookup"><span data-stu-id="7f22a-135">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="7f22a-136">SDK Bot Framework предоставляет дополнительные методы и объекты, упрощающие создание упоминания.</span><span class="sxs-lookup"><span data-stu-id="7f22a-136">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f22a-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f22a-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7f22a-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7f22a-138">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="7f22a-139">JSON</span><span class="sxs-lookup"><span data-stu-id="7f22a-139">JSON</span></span>](#tab/json)

<span data-ttu-id="7f22a-140">Поле в объекте массива должно точно `text` `entities` соответствовать части поля  `text` сообщения.</span><span class="sxs-lookup"><span data-stu-id="7f22a-140">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="7f22a-141">Если этого не сделать, упоминание будет проигнорировано.</span><span class="sxs-lookup"><span data-stu-id="7f22a-141">If it does not, the mention will be ignored.</span></span>

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

# <a name="python"></a>[<span data-ttu-id="7f22a-142">Python</span><span class="sxs-lookup"><span data-stu-id="7f22a-142">Python</span></span>](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="7f22a-143">Отправка сообщения при установке</span><span class="sxs-lookup"><span data-stu-id="7f22a-143">Sending a message on installation</span></span>

<span data-ttu-id="7f22a-144">При первом добавлении бота в группу или команду может быть полезно отправить сообщение с его введением.</span><span class="sxs-lookup"><span data-stu-id="7f22a-144">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="7f22a-145">В сообщении должно быть краткое описание функций бота и их использования.</span><span class="sxs-lookup"><span data-stu-id="7f22a-145">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="7f22a-146">Вы захотите подписаться на `conversationUpdate` событие с помощью `teamMemberAdded` eventType.</span><span class="sxs-lookup"><span data-stu-id="7f22a-146">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="7f22a-147">Так как событие отправляется при добавлении нового участника группы, необходимо проверить, является ли новый участник ботом.</span><span class="sxs-lookup"><span data-stu-id="7f22a-147">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="7f22a-148">Дополнительные [сведения см.](~/bots/how-to/conversations/send-proactive-messages.md) в сообщении о том, как отправить приветствие новому участнику группы.</span><span class="sxs-lookup"><span data-stu-id="7f22a-148">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="7f22a-149">Вы также можете отправить личное сообщение каждому участнику команды при добавлении бота.</span><span class="sxs-lookup"><span data-stu-id="7f22a-149">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="7f22a-150">Для этого можно получить список команд и отправить каждому пользователю прямое сообщение.</span><span class="sxs-lookup"><span data-stu-id="7f22a-150">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="7f22a-151">Не рекомендуется отправлять сообщение в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="7f22a-151">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="7f22a-152">Команда большая (очевидно, что она субъективна, но, например, более 100 участников).</span><span class="sxs-lookup"><span data-stu-id="7f22a-152">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="7f22a-153">Ваш бот может быть виден как "спам", а добавлявший его пользователь может получить жалобы, если вы не ясно сообщаете о преимуществах вашего бота всем, кто видит приветствие.</span><span class="sxs-lookup"><span data-stu-id="7f22a-153">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="7f22a-154">Ваш бот впервые упоминается в группе или канале (по сравнению с первым добавлением в команду)</span><span class="sxs-lookup"><span data-stu-id="7f22a-154">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="7f22a-155">Группа или канал переименовываются</span><span class="sxs-lookup"><span data-stu-id="7f22a-155">A group or channel is renamed</span></span>
* <span data-ttu-id="7f22a-156">Участник команды добавляется в группу или канал</span><span class="sxs-lookup"><span data-stu-id="7f22a-156">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="7f22a-157">Подробнее</span><span class="sxs-lookup"><span data-stu-id="7f22a-157">Learn more</span></span>

<span data-ttu-id="7f22a-158">У бота есть доступ к дополнительным сведениям о групповом чате или команде, в которую он установлен.</span><span class="sxs-lookup"><span data-stu-id="7f22a-158">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="7f22a-159">Дополнительные [API,](~/bots/how-to/get-teams-context.md) доступные для бота, см. в контексте команды.</span><span class="sxs-lookup"><span data-stu-id="7f22a-159">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="7f22a-160">Кроме того, бот может подписаться на дополнительные события и ответить на них.</span><span class="sxs-lookup"><span data-stu-id="7f22a-160">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="7f22a-161">См. [подписку на события бесед,](~/bots/how-to/conversations/subscribe-to-conversation-events.md) чтобы узнать, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="7f22a-161">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
