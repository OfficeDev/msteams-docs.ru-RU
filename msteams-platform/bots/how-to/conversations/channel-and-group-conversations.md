---
title: Телефонные и групповые беседы с ботом
author: clearab
description: Отправка, получение и обработка сообщений для бота в канале или групповом чате.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: ef5cf8464fa0e93d5ea3840003a2b0c04a4a5ef5
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631001"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a><span data-ttu-id="791c9-103">Телефонные и групповые беседы в чате с ботом</span><span class="sxs-lookup"><span data-stu-id="791c9-103">Channel and group chat conversations with a bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="791c9-104">Чтобы установить Microsoft Teams в командном или групповом чате, добавьте область или область `teams` `groupchat` в бот.</span><span class="sxs-lookup"><span data-stu-id="791c9-104">To install the Microsoft Teams bot in a team or group chat, add the `teams` or `groupchat` scope to your bot.</span></span> <span data-ttu-id="791c9-105">В результате все участники беседы взаимодействовать с вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="791c9-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="791c9-106">После установки бота он имеет доступ к метаданным о беседе, например к списку участников беседы.</span><span class="sxs-lookup"><span data-stu-id="791c9-106">After the bot is installed, it has access to metadata about the conversation, such as the list of conversation members.</span></span> <span data-ttu-id="791c9-107">Кроме того, при установке в команде бот имеет доступ к сведениям об этой группе и полном списке каналов.</span><span class="sxs-lookup"><span data-stu-id="791c9-107">Also, when it is installed in a team, the bot has access to details about that team and the full list of channels.</span></span>

<span data-ttu-id="791c9-108">Боты в группе или канале получают сообщения только в том случае, если они упоминаются @botname.</span><span class="sxs-lookup"><span data-stu-id="791c9-108">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="791c9-109">Они не получают никаких других сообщений, отправленных в беседу.</span><span class="sxs-lookup"><span data-stu-id="791c9-109">They do not receive any other messages sent to the conversation.</span></span> <span data-ttu-id="791c9-110">Бот должен быть @упомянут непосредственно.</span><span class="sxs-lookup"><span data-stu-id="791c9-110">The bot must be @mentioned directly.</span></span> <span data-ttu-id="791c9-111">Ваш бот не получает сообщение, когда команда или канал упоминаются, или когда кто-то отвечает на сообщение от вашего бота без @mentioning его.</span><span class="sxs-lookup"><span data-stu-id="791c9-111">Your bot does not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

> [!NOTE]
> <span data-ttu-id="791c9-112">В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../../../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="791c9-112">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>
>
> <span data-ttu-id="791c9-113">С помощью согласия на использование ресурсов (RSC) боты могут получать все сообщения каналов в командах, в которые он установлен без @mentioned.</span><span class="sxs-lookup"><span data-stu-id="791c9-113">Using resource-specific consent (RSC), bots can receive all channel messages in teams that it is installed in without being @mentioned.</span></span> <span data-ttu-id="791c9-114">Дополнительные сведения см. в [сообщении о приеме всех сообщений канала с помощью RSC.](channel-messages-with-rsc.md)</span><span class="sxs-lookup"><span data-stu-id="791c9-114">For more information, see [receive all channel messages with RSC](channel-messages-with-rsc.md).</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="791c9-115">Рекомендации по дизайну</span><span class="sxs-lookup"><span data-stu-id="791c9-115">Design guidelines</span></span>

<span data-ttu-id="791c9-116">В отличие от личных чатов, в групповых чатах и каналах бот должен предоставить быстрое введение.</span><span class="sxs-lookup"><span data-stu-id="791c9-116">Unlike personal chats, in group chats and channels, your bot must provide a quick introduction.</span></span> <span data-ttu-id="791c9-117">Необходимо следовать этим и дополнительным рекомендациям по разработке ботов.</span><span class="sxs-lookup"><span data-stu-id="791c9-117">You must follow these and more bot design guidelines.</span></span> <span data-ttu-id="791c9-118">Дополнительные сведения о разработке ботов в Teams см. в том, как создать беседы ботов в каналах [и чатах.](~/bots/design/bots.md)</span><span class="sxs-lookup"><span data-stu-id="791c9-118">For more information on how to design bots in Teams, see [how to design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

<span data-ttu-id="791c9-119">Теперь вы можете создавать новые потоки бесед и легко управлять различными беседами в каналах.</span><span class="sxs-lookup"><span data-stu-id="791c9-119">Now, you can create new conversation threads and easily manage different conversations in channels.</span></span>

## <a name="create-new-conversation-threads"></a><span data-ttu-id="791c9-120">Создание новых потоков беседы</span><span class="sxs-lookup"><span data-stu-id="791c9-120">Create new conversation threads</span></span>

<span data-ttu-id="791c9-121">При установке бота в команде необходимо создать новый поток беседы, а не отвечать на существующий.</span><span class="sxs-lookup"><span data-stu-id="791c9-121">When your bot is installed in a team, you must create a new conversation thread rather than reply to an existing one.</span></span> <span data-ttu-id="791c9-122">Иногда трудно различать два разговора.</span><span class="sxs-lookup"><span data-stu-id="791c9-122">At times it is difficult to differentiate between two conversations.</span></span> <span data-ttu-id="791c9-123">Если беседа потоковая, проще организовать и управлять различными беседами в каналах.</span><span class="sxs-lookup"><span data-stu-id="791c9-123">If the conversation is threaded, it is easier to organize and manage different conversations in channels.</span></span> <span data-ttu-id="791c9-124">Это форма [активного обмена сообщениями.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="791c9-124">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="791c9-125">Далее можно получить упоминания с помощью объекта и добавить упоминания в `entities` сообщения с помощью `Mention` объекта.</span><span class="sxs-lookup"><span data-stu-id="791c9-125">Next, you can retrieve mentions using the `entities` object and add mentions to your messages using the `Mention` object.</span></span>

## <a name="work-with-mentions"></a><span data-ttu-id="791c9-126">Работа с упоминаниями</span><span class="sxs-lookup"><span data-stu-id="791c9-126">Work with mentions</span></span>

<span data-ttu-id="791c9-127">Каждое сообщение боту из группы или канала содержит @mention с его именем в тексте сообщения.</span><span class="sxs-lookup"><span data-stu-id="791c9-127">Every message to your bot from a group or channel contains an @mention with its name in the message text.</span></span> <span data-ttu-id="791c9-128">Кроме того, бот может получать другие пользователи, упомянутые в сообщении, и добавлять упоминания в любые сообщения, которые он отправляет.</span><span class="sxs-lookup"><span data-stu-id="791c9-128">Your bot can also retrieve other users mentioned in a message and add mentions to any messages it sends.</span></span>

<span data-ttu-id="791c9-129">Кроме того, необходимо @mentions из содержимого сообщения, которое получает бот.</span><span class="sxs-lookup"><span data-stu-id="791c9-129">You must also strip out the @mentions from the content of the message your bot receives.</span></span>

### <a name="retrieve-mentions"></a><span data-ttu-id="791c9-130">Извлечение упоминаний</span><span class="sxs-lookup"><span data-stu-id="791c9-130">Retrieve mentions</span></span>

<span data-ttu-id="791c9-131">Упоминания возвращаются в объекте в полезной нагрузке и содержат как уникальный ID пользователя, так и имя `entities` упомянутого пользователя.</span><span class="sxs-lookup"><span data-stu-id="791c9-131">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and the name of the user mentioned.</span></span> <span data-ttu-id="791c9-132">В тексте сообщения также содержится упоминание, например `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="791c9-132">The text of the message also includes the mention, such as `<at>@John Smith<at>`.</span></span> <span data-ttu-id="791c9-133">Однако не следует полагаться на текст в сообщении для получения сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="791c9-133">However, do not rely on the text in the message to retrieve any information about the user.</span></span> <span data-ttu-id="791c9-134">Это возможно для человека, отправляя сообщение, чтобы изменить его.</span><span class="sxs-lookup"><span data-stu-id="791c9-134">It is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="791c9-135">Поэтому используйте `entities` объект.</span><span class="sxs-lookup"><span data-stu-id="791c9-135">Therefore, use the `entities` object.</span></span>

<span data-ttu-id="791c9-136">Вы можете получить все упоминания в сообщении, позвонив функции в SDK Bot Builder, которая возвращает `GetMentions` массив `Mention` объектов.</span><span class="sxs-lookup"><span data-stu-id="791c9-136">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK, which returns an array of `Mention` objects.</span></span>

<span data-ttu-id="791c9-137">В следующем коде показан пример упоминаний о том, как следующую возможность:</span><span class="sxs-lookup"><span data-stu-id="791c9-137">The following code shows an example of retrieving mentions:</span></span>

# <a name="c"></a>[<span data-ttu-id="791c9-138">C#</span><span class="sxs-lookup"><span data-stu-id="791c9-138">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="791c9-139">TypeScript</span><span class="sxs-lookup"><span data-stu-id="791c9-139">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="791c9-140">JSON</span><span class="sxs-lookup"><span data-stu-id="791c9-140">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="791c9-141">Python</span><span class="sxs-lookup"><span data-stu-id="791c9-141">Python</span></span>](#tab/python)

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

### <a name="add-mentions-to-your-messages"></a><span data-ttu-id="791c9-142">Добавление упоминаний в сообщения</span><span class="sxs-lookup"><span data-stu-id="791c9-142">Add mentions to your messages</span></span>

<span data-ttu-id="791c9-143">Ваш бот может упоминать других пользователей в сообщениях, которые размещены в каналах.</span><span class="sxs-lookup"><span data-stu-id="791c9-143">Your bot can mention other users in messages posted into channels.</span></span>

<span data-ttu-id="791c9-144">Объект `Mention` имеет два свойства, которые необходимо установить, используя следующее:</span><span class="sxs-lookup"><span data-stu-id="791c9-144">The `Mention` object has two properties that you must set using the following:</span></span>

* <span data-ttu-id="791c9-145"><at>Включи @username</at> в текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="791c9-145">Include <at>@username</at> in the message text.</span></span>
* <span data-ttu-id="791c9-146">Включай объект упоминания в коллекцию сущностями.</span><span class="sxs-lookup"><span data-stu-id="791c9-146">Include the mention object inside the entities collection.</span></span>

<span data-ttu-id="791c9-147">SDK Bot Framework предоставляет дополнительные методы и объекты для создания упоминаний.</span><span class="sxs-lookup"><span data-stu-id="791c9-147">The Bot Framework SDK provides helper methods and objects to create mentions.</span></span>

<span data-ttu-id="791c9-148">В следующем коде показан пример добавления упоминаний в сообщения:</span><span class="sxs-lookup"><span data-stu-id="791c9-148">The following code shows an example of adding mentions to your messages:</span></span>

# <a name="c"></a>[<span data-ttu-id="791c9-149">C#</span><span class="sxs-lookup"><span data-stu-id="791c9-149">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="791c9-150">TypeScript</span><span class="sxs-lookup"><span data-stu-id="791c9-150">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="791c9-151">JSON</span><span class="sxs-lookup"><span data-stu-id="791c9-151">JSON</span></span>](#tab/json)

<span data-ttu-id="791c9-152">Поле объекта в массиве должно `text` `entities` соответствовать части поля `text` сообщений.</span><span class="sxs-lookup"><span data-stu-id="791c9-152">The `text` field in the object in the `entities` array must match a portion of the message `text` field.</span></span> <span data-ttu-id="791c9-153">Если этого не происходит, упоминание игнорируется.</span><span class="sxs-lookup"><span data-stu-id="791c9-153">If it does not, the mention is ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="791c9-154">Python</span><span class="sxs-lookup"><span data-stu-id="791c9-154">Python</span></span>](#tab/python)

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

<span data-ttu-id="791c9-155">Теперь вы можете отправить сообщение о вводе при первом установке или добавлении бота в группу или группу.</span><span class="sxs-lookup"><span data-stu-id="791c9-155">Now you can send an introduction message when your bot is first installed or added to a group or team.</span></span>

## <a name="send-a-message-on-installation"></a><span data-ttu-id="791c9-156">Отправка сообщения при установке</span><span class="sxs-lookup"><span data-stu-id="791c9-156">Send a message on installation</span></span>

<span data-ttu-id="791c9-157">При первом добавлении бота в группу или группу необходимо отправить вводное сообщение.</span><span class="sxs-lookup"><span data-stu-id="791c9-157">When your bot is first added to the group or team, an introduction message must be sent.</span></span> <span data-ttu-id="791c9-158">В сообщении должно быть краткое описание функций бота и их использования.</span><span class="sxs-lookup"><span data-stu-id="791c9-158">The message must provide a brief description of the bot's features and how to use them.</span></span> <span data-ttu-id="791c9-159">Необходимо подписаться на `conversationUpdate` событие с `teamMemberAdded` помощью eventType.</span><span class="sxs-lookup"><span data-stu-id="791c9-159">You must subscribe to the `conversationUpdate` event with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="791c9-160">Событие отправляется при добавлении любого нового члена команды.</span><span class="sxs-lookup"><span data-stu-id="791c9-160">The event is sent when any new team member is added.</span></span> <span data-ttu-id="791c9-161">Проверьте, является ли добавленный новый участник ботом.</span><span class="sxs-lookup"><span data-stu-id="791c9-161">Check if the new member added is the bot.</span></span> <span data-ttu-id="791c9-162">Дополнительные сведения см. [в тексте отправки приветствия новому члену группы.](~/bots/how-to/conversations/send-proactive-messages.md)</span><span class="sxs-lookup"><span data-stu-id="791c9-162">For more information, see [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="791c9-163">Отправьте личное сообщение каждому члену группы при добавлении бота.</span><span class="sxs-lookup"><span data-stu-id="791c9-163">Send a personal message to each team member when the bot is added.</span></span> <span data-ttu-id="791c9-164">Для этого получите список команд и отправьте каждому пользователю прямое сообщение.</span><span class="sxs-lookup"><span data-stu-id="791c9-164">To do this, get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="791c9-165">Не отправлять сообщение в следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="791c9-165">Do not send a message in the following cases:</span></span>

* <span data-ttu-id="791c9-166">Группа большая, например, более 100 участников.</span><span class="sxs-lookup"><span data-stu-id="791c9-166">The team is large, for example, larger than 100 members.</span></span> <span data-ttu-id="791c9-167">Ваш бот может рассматриваться как спам, а добавленный в него человек может получать жалобы.</span><span class="sxs-lookup"><span data-stu-id="791c9-167">Your bot can be seen as spam and the person who added it can get complaints.</span></span> <span data-ttu-id="791c9-168">Необходимо четко донести предложение о ценности бота до всех, кто увидит приветствие.</span><span class="sxs-lookup"><span data-stu-id="791c9-168">You must clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="791c9-169">Сначала бот упоминается в группе или канале, а не в команде.</span><span class="sxs-lookup"><span data-stu-id="791c9-169">Your bot is first mentioned in a group or channel instead of being first added to a team.</span></span>
* <span data-ttu-id="791c9-170">Группа или канал переименованы.</span><span class="sxs-lookup"><span data-stu-id="791c9-170">A group or channel is renamed.</span></span>
* <span data-ttu-id="791c9-171">Член группы добавляется в группу или канал.</span><span class="sxs-lookup"><span data-stu-id="791c9-171">A team member is added to a group or channel.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a><span data-ttu-id="791c9-172">См. также</span><span class="sxs-lookup"><span data-stu-id="791c9-172">See also</span></span>

[<span data-ttu-id="791c9-173">Получить Teams контекст</span><span class="sxs-lookup"><span data-stu-id="791c9-173">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a><span data-ttu-id="791c9-174">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="791c9-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="791c9-175">Подписка на события беседы</span><span class="sxs-lookup"><span data-stu-id="791c9-175">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
