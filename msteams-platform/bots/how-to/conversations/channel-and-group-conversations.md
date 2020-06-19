---
title: Канал и групповые разговоры
author: clearab
description: Отправка, получение и обработка сообщений для программы Bot в канале или группе чата.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ccc27d7638820cfa3c2b7cfe12b91b3a3a9fef1d
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2020
ms.locfileid: "44801525"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="e013b-103">Беседы в каналах и группах для общения с помощью робота Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e013b-103">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="e013b-104">Добавление `teams` `groupchat` области или области к интерфейсу робота может быть доступна для установки в команде или группе чата.</span><span class="sxs-lookup"><span data-stu-id="e013b-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="e013b-105">Это позволяет всем участникам беседы взаимодействовать с роботом.</span><span class="sxs-lookup"><span data-stu-id="e013b-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="e013b-106">После установки он также будет иметь доступ к метаданным беседы, как к списку участников беседы, а также при установке в группе сведений о команде и полном списке каналов.</span><span class="sxs-lookup"><span data-stu-id="e013b-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="e013b-107">Боты в группе или канале получать сообщения только при их упоминании ("@botname"), они не получают никаких других сообщений, отправляемых в беседу.</span><span class="sxs-lookup"><span data-stu-id="e013b-107">Bots in a group or channel only receive messages when they are mentioned ("@botname"), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="e013b-108">Bot должен быть @mentioned напрямую.</span><span class="sxs-lookup"><span data-stu-id="e013b-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="e013b-109">Программа-робот не получает сообщение при упоминании команды или канала, а также когда кто-то отвечает на сообщение от пользователя Bot, не @mentioning его.</span><span class="sxs-lookup"><span data-stu-id="e013b-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-considerations"></a><span data-ttu-id="e013b-110">Особенности дизайна</span><span class="sxs-lookup"><span data-stu-id="e013b-110">Design considerations</span></span>

<span data-ttu-id="e013b-111">Bot должен предоставлять сведения, которые соответствуют всем участникам группы или канала.</span><span class="sxs-lookup"><span data-stu-id="e013b-111">A bot should provide information that is both appropriate and relevant to all members in a group or channel.</span></span> <span data-ttu-id="e013b-112">Беседы с ним видны всем, которые являются частью группы или канала.</span><span class="sxs-lookup"><span data-stu-id="e013b-112">Conversations with it are visible to everyone that is a part of the group or channel.</span></span> <span data-ttu-id="e013b-113">С помощью хорошо спроектированного почтового робота можно добавить значение ко всем пользователям, не создавая при этом непреднамеренное совместное использование информации в беседе "один к одному".</span><span class="sxs-lookup"><span data-stu-id="e013b-113">A well designed bot can add value to all users while not inadvertently sharing information that is more appropriate in a one-to-one conversation.</span></span> <span data-ttu-id="e013b-114">Для сбора информации в беседах, таких как диалоговые окна, следует избегать использования карточек и/или модулей задач.</span><span class="sxs-lookup"><span data-stu-id="e013b-114">Multi-turn conversations like dialogs should be avoided - use cards and/or task modules to collect information instead.</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="e013b-115">Создание новых потоков беседы</span><span class="sxs-lookup"><span data-stu-id="e013b-115">Creating new conversation threads</span></span>

<span data-ttu-id="e013b-116">При установке ленты в команду иногда может потребоваться создать новый поток бесед, а не отвечать на него.</span><span class="sxs-lookup"><span data-stu-id="e013b-116">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="e013b-117">Это форма [упреждающего обмена сообщениями](~/bots/how-to/conversations/send-proactive-messages.md).</span><span class="sxs-lookup"><span data-stu-id="e013b-117">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="e013b-118">Работа с упоминаниями</span><span class="sxs-lookup"><span data-stu-id="e013b-118">Working with mentions</span></span>

<span data-ttu-id="e013b-119">Каждое сообщение для ленты из группы или канала будет содержать @mention с собственным именем в тексте сообщения, поэтому необходимо убедиться, что маркеры синтаксического анализа сообщения.</span><span class="sxs-lookup"><span data-stu-id="e013b-119">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="e013b-120">С помощью Bot можно также получить других пользователей, упомянутых в сообщении, и добавить упоминания в сообщения, которые он отправляет.</span><span class="sxs-lookup"><span data-stu-id="e013b-120">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="e013b-121">Удаление упоминаний из текста сообщения</span><span class="sxs-lookup"><span data-stu-id="e013b-121">Stripping mentions from message text</span></span>

<span data-ttu-id="e013b-122">Может потребоваться изъять @mentions из текста сообщения, полученного от ленты.</span><span class="sxs-lookup"><span data-stu-id="e013b-122">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="e013b-123">Получение упоминаний</span><span class="sxs-lookup"><span data-stu-id="e013b-123">Retrieving mentions</span></span>

<span data-ttu-id="e013b-124">Упоминания возвращаются в `entities` объекте полезных данных и содержат как уникальный идентификатор пользователя, так и, в большинстве случаев, имя пользователя, указанное пользователем.</span><span class="sxs-lookup"><span data-stu-id="e013b-124">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="e013b-125">Текст сообщения также будет содержать упоминание о том, как `<at>@John Smith<at>` .</span><span class="sxs-lookup"><span data-stu-id="e013b-125">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="e013b-126">Тем не менее, не следует полагаться на текст в сообщении, чтобы получить сведения о пользователе; пользователь, отправивший сообщение, может изменить его.</span><span class="sxs-lookup"><span data-stu-id="e013b-126">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="e013b-127">Вместо этого используйте `entities` объект.</span><span class="sxs-lookup"><span data-stu-id="e013b-127">Instead, use the `entities` object.</span></span>

<span data-ttu-id="e013b-128">Вы можете получить все упоминания в сообщении, вызвав `GetMentions` функцию в пакете SDK построителя ленты, которая возвращает массив `Mention` объектов.</span><span class="sxs-lookup"><span data-stu-id="e013b-128">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e013b-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e013b-129">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e013b-130">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e013b-130">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e013b-131">JSON</span><span class="sxs-lookup"><span data-stu-id="e013b-131">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="e013b-132">Python</span><span class="sxs-lookup"><span data-stu-id="e013b-132">Python</span></span>](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="e013b-133">Добавление упоминания к сообщениям</span><span class="sxs-lookup"><span data-stu-id="e013b-133">Adding mentions to your messages</span></span>

<span data-ttu-id="e013b-134">Ваш Bot может заупоминаниь других пользователей в сообщениях, размещенных в каналах.</span><span class="sxs-lookup"><span data-stu-id="e013b-134">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="e013b-135">Для этого сообщение должно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e013b-135">To do this, your message must do the following:</span></span>

<span data-ttu-id="e013b-136">У `Mention` объекта есть два свойства, которые необходимо задать:</span><span class="sxs-lookup"><span data-stu-id="e013b-136">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="e013b-137">Включение <at>@username</at> в текст сообщения</span><span class="sxs-lookup"><span data-stu-id="e013b-137">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="e013b-138">Добавление объекта упоминаемого объекта в коллекцию сущностей</span><span class="sxs-lookup"><span data-stu-id="e013b-138">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="e013b-139">Пакет SDK для ленты предоставляет вспомогательные методы и объекты для упрощения создания упоминания.</span><span class="sxs-lookup"><span data-stu-id="e013b-139">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="e013b-140">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e013b-140">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="e013b-141">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="e013b-141">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="e013b-142">JSON</span><span class="sxs-lookup"><span data-stu-id="e013b-142">JSON</span></span>](#tab/json)

<span data-ttu-id="e013b-143">`text`Поле в объекте в `entities` массиве должно *точно* соответствовать части `text` поля сообщения.</span><span class="sxs-lookup"><span data-stu-id="e013b-143">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="e013b-144">В противном случае упоминание будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="e013b-144">If it does not, the mention will be ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="e013b-145">Python</span><span class="sxs-lookup"><span data-stu-id="e013b-145">Python</span></span>](#tab/python)

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

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="e013b-146">Отправка сообщения при установке</span><span class="sxs-lookup"><span data-stu-id="e013b-146">Sending a message on installation</span></span>

<span data-ttu-id="e013b-147">При первом добавлении ленты в группу или группу может быть полезно отправить сообщение.</span><span class="sxs-lookup"><span data-stu-id="e013b-147">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="e013b-148">Сообщение должно содержать краткое описание функций и их использования.</span><span class="sxs-lookup"><span data-stu-id="e013b-148">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="e013b-149">Вы хотите подписаться на `conversationUpdate` событие с помощью `teamMemberAdded` EventType.</span><span class="sxs-lookup"><span data-stu-id="e013b-149">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="e013b-150">Так как событие отправляется при добавлении нового члена группы, необходимо проверить, добавлен ли новый член Bot.</span><span class="sxs-lookup"><span data-stu-id="e013b-150">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="e013b-151">Узнайте больше о том, как [Отправить приветственное сообщение новому участнику группы](~/bots/how-to/conversations/send-proactive-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="e013b-151">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="e013b-152">Кроме того, вы можете отправить личное сообщение каждому участнику команды при добавлении ленты.</span><span class="sxs-lookup"><span data-stu-id="e013b-152">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="e013b-153">Для этого вы можете получить список участников команды и отправить ему прямое сообщение.</span><span class="sxs-lookup"><span data-stu-id="e013b-153">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="e013b-154">Не рекомендуется отправлять сообщения в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="e013b-154">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="e013b-155">Команда является большой (субъективно субъективна, но например, более 100 членов).</span><span class="sxs-lookup"><span data-stu-id="e013b-155">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="e013b-156">Ваш робот может отображаться как "нежелательный", а пользователь, который добавил его, может получать жалобу, если вы не хотите явно сообщить о значении для пользователя, который видит приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="e013b-156">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="e013b-157">Первый из них упоминается в группе или канале (в отличие от первого добавления в группу).</span><span class="sxs-lookup"><span data-stu-id="e013b-157">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="e013b-158">Переименование группы или канала</span><span class="sxs-lookup"><span data-stu-id="e013b-158">A group or channel is renamed</span></span>
* <span data-ttu-id="e013b-159">Участник группы добавляется в группу или канал</span><span class="sxs-lookup"><span data-stu-id="e013b-159">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="e013b-160">Подробнее</span><span class="sxs-lookup"><span data-stu-id="e013b-160">Learn more</span></span>

<span data-ttu-id="e013b-161">У вас есть доступ к дополнительным сведениям о групповой беседе или группе, в которой он установлен.</span><span class="sxs-lookup"><span data-stu-id="e013b-161">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="e013b-162">Ознакомьтесь с [контекстом Get Teams](~/bots/how-to/get-teams-context.md) , чтобы получить дополнительные API, доступные для ленты.</span><span class="sxs-lookup"><span data-stu-id="e013b-162">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="e013b-163">Кроме того, существуют дополнительные события, на которые может подписаться и реагировать ваш робот.</span><span class="sxs-lookup"><span data-stu-id="e013b-163">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="e013b-164">Узнайте, как [подписаться на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md) .</span><span class="sxs-lookup"><span data-stu-id="e013b-164">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
