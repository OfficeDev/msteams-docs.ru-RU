---
title: Подписаться на события разговора
author: WashingtonKayaker
description: Как подписаться на события бесед из робота Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: c678690b1dc2c948cceacdf42c95f169fff753bb
ms.sourcegitcommit: 560bf433129c16888135879e2703dbdeb38ec99f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2020
ms.locfileid: "48397682"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="cefd6-103">Подписаться на события разговора</span><span class="sxs-lookup"><span data-stu-id="cefd6-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="cefd6-104">Microsoft Teams отправляет уведомления в Bot для событий, происходящих в областях действия ленты.</span><span class="sxs-lookup"><span data-stu-id="cefd6-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="cefd6-105">Вы можете записать эти события в код и выполнить действия с ними, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="cefd6-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="cefd6-106">Инициация приветственного сообщения при добавлении ленты в группу</span><span class="sxs-lookup"><span data-stu-id="cefd6-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="cefd6-107">Инициация приветственного сообщения при добавлении или удалении нового участника группы</span><span class="sxs-lookup"><span data-stu-id="cefd6-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="cefd6-108">Запуск уведомления при создании, переименовании или удалении канала</span><span class="sxs-lookup"><span data-stu-id="cefd6-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="cefd6-109">Когда пользователю понравится сообщение Bot</span><span class="sxs-lookup"><span data-stu-id="cefd6-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="cefd6-110">События обновления беседы</span><span class="sxs-lookup"><span data-stu-id="cefd6-110">Conversation update events</span></span>

<span data-ttu-id="cefd6-111">Элемент Bot получает `conversationUpdate` событие, когда оно было добавлено в беседу, другие элементы были добавлены в беседу или удалены из нее, а метаданные беседы изменились.</span><span class="sxs-lookup"><span data-stu-id="cefd6-111">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="cefd6-112">`conversationUpdate`Событие отправляется в Bot при получении сведений об обновлениях членства для Teams, где она была добавлена.</span><span class="sxs-lookup"><span data-stu-id="cefd6-112">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="cefd6-113">Он также получает обновление, когда оно добавляется в первый раз специально для личных бесед.</span><span class="sxs-lookup"><span data-stu-id="cefd6-113">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="cefd6-114">В следующей таблице приведен список событий обновления бесед в Teams со ссылками на дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="cefd6-114">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="cefd6-115">Выполняемое действие</span><span class="sxs-lookup"><span data-stu-id="cefd6-115">Action Taken</span></span>        | <span data-ttu-id="cefd6-116">EventType</span><span class="sxs-lookup"><span data-stu-id="cefd6-116">EventType</span></span>         | <span data-ttu-id="cefd6-117">Метод с именем</span><span class="sxs-lookup"><span data-stu-id="cefd6-117">Method Called</span></span>              | <span data-ttu-id="cefd6-118">Описание</span><span class="sxs-lookup"><span data-stu-id="cefd6-118">Description</span></span>                | <span data-ttu-id="cefd6-119">Область</span><span class="sxs-lookup"><span data-stu-id="cefd6-119">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="cefd6-120">канал создан</span><span class="sxs-lookup"><span data-stu-id="cefd6-120">channel created</span></span>     | <span data-ttu-id="cefd6-121">чаннелкреатед</span><span class="sxs-lookup"><span data-stu-id="cefd6-121">channelCreated</span></span>    | <span data-ttu-id="cefd6-122">онтеамсчаннелкреатедасинк</span><span class="sxs-lookup"><span data-stu-id="cefd6-122">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="cefd6-123">Создан канал</span><span class="sxs-lookup"><span data-stu-id="cefd6-123">A channel was created</span></span>](#channel-created) | <span data-ttu-id="cefd6-124">Команда</span><span class="sxs-lookup"><span data-stu-id="cefd6-124">Team</span></span> |
| <span data-ttu-id="cefd6-125">канал переименован</span><span class="sxs-lookup"><span data-stu-id="cefd6-125">channel renamed</span></span>     | <span data-ttu-id="cefd6-126">чаннелренамед</span><span class="sxs-lookup"><span data-stu-id="cefd6-126">channelRenamed</span></span>    | <span data-ttu-id="cefd6-127">онтеамсчаннелренамедасинк</span><span class="sxs-lookup"><span data-stu-id="cefd6-127">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="cefd6-128">Канал переименован</span><span class="sxs-lookup"><span data-stu-id="cefd6-128">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="cefd6-129">Команда</span><span class="sxs-lookup"><span data-stu-id="cefd6-129">Team</span></span> |
| <span data-ttu-id="cefd6-130">канал удален</span><span class="sxs-lookup"><span data-stu-id="cefd6-130">channel deleted</span></span>     | <span data-ttu-id="cefd6-131">чаннелделетед</span><span class="sxs-lookup"><span data-stu-id="cefd6-131">channelDeleted</span></span>    | <span data-ttu-id="cefd6-132">онтеамсчаннелделетедасинк</span><span class="sxs-lookup"><span data-stu-id="cefd6-132">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="cefd6-133">Канал удален</span><span class="sxs-lookup"><span data-stu-id="cefd6-133">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="cefd6-134">Команда</span><span class="sxs-lookup"><span data-stu-id="cefd6-134">Team</span></span> |
| <span data-ttu-id="cefd6-135">добавленные участники группы</span><span class="sxs-lookup"><span data-stu-id="cefd6-135">team members added</span></span>   | <span data-ttu-id="cefd6-136">теаммембераддед</span><span class="sxs-lookup"><span data-stu-id="cefd6-136">teamMemberAdded</span></span>   | <span data-ttu-id="cefd6-137">онтеамсмемберсаддедасинк</span><span class="sxs-lookup"><span data-stu-id="cefd6-137">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="cefd6-138">Участник, добавленный в группу</span><span class="sxs-lookup"><span data-stu-id="cefd6-138">A Member added to team</span></span>](#team-members-added)   | <span data-ttu-id="cefd6-139">Все</span><span class="sxs-lookup"><span data-stu-id="cefd6-139">All</span></span> |
| <span data-ttu-id="cefd6-140">удалены участники группы</span><span class="sxs-lookup"><span data-stu-id="cefd6-140">team members removed</span></span> | <span data-ttu-id="cefd6-141">теаммемберремовед</span><span class="sxs-lookup"><span data-stu-id="cefd6-141">teamMemberRemoved</span></span> | <span data-ttu-id="cefd6-142">онтеамсмемберсремоведасинк</span><span class="sxs-lookup"><span data-stu-id="cefd6-142">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="cefd6-143">Участник удален из группы</span><span class="sxs-lookup"><span data-stu-id="cefd6-143">A Member was removed from team</span></span>](#team-members-removed) | <span data-ttu-id="cefd6-144">Группа & groupChat</span><span class="sxs-lookup"><span data-stu-id="cefd6-144">groupChat & team</span></span> |
| <span data-ttu-id="cefd6-145">Команда переименована</span><span class="sxs-lookup"><span data-stu-id="cefd6-145">team renamed</span></span>        | <span data-ttu-id="cefd6-146">теамренамед</span><span class="sxs-lookup"><span data-stu-id="cefd6-146">teamRenamed</span></span>       | <span data-ttu-id="cefd6-147">онтеамстеамренамедасинк</span><span class="sxs-lookup"><span data-stu-id="cefd6-147">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="cefd6-148">Команда была переименована</span><span class="sxs-lookup"><span data-stu-id="cefd6-148">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="cefd6-149">Команда</span><span class="sxs-lookup"><span data-stu-id="cefd6-149">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="cefd6-150">Канал создан</span><span class="sxs-lookup"><span data-stu-id="cefd6-150">Channel created</span></span>

<span data-ttu-id="cefd6-151">Событие созданного канала отправляется на ваш робот при создании нового канала в группе, в которой установлен почтовый робот.</span><span class="sxs-lookup"><span data-stu-id="cefd6-151">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-152">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-152">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-153">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-153">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelCreatedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Created', `${channelInfo.name} is the Channel created`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="cefd6-154">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-154">JSON</span></span>](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="cefd6-155">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-155">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="cefd6-156">Канал переименован</span><span class="sxs-lookup"><span data-stu-id="cefd6-156">Channel renamed</span></span>

<span data-ttu-id="cefd6-157">Событие переименования канала передается в Bot при переименовании канала в группе, в которой установлен почтовый робот.</span><span class="sxs-lookup"><span data-stu-id="cefd6-157">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-158">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-158">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-159">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-159">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRenamedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Renamed', `${channelInfo.name} is the new Channel name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
```

# <a name="json"></a>[<span data-ttu-id="cefd6-160">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-160">JSON</span></span>](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "PhotographyUpdates"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelRenamed",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="cefd6-161">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-161">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="cefd6-162">Канал удален</span><span class="sxs-lookup"><span data-stu-id="cefd6-162">Channel Deleted</span></span>

<span data-ttu-id="cefd6-163">Событие Deleted Channel отправляется на ваш Bot при удалении канала в группе, в которой установлен почтовый робот.</span><span class="sxs-lookup"><span data-stu-id="cefd6-163">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-164">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-165">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-165">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelDeletedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Deleted', `${channelInfo.name} is the Channel deleted`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="cefd6-166">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-166">JSON</span></span>](#tab/json)

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "PhotographyUpdates"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelDeleted",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="cefd6-167">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-167">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="cefd6-168">Добавленные участники группы</span><span class="sxs-lookup"><span data-stu-id="cefd6-168">Team members added</span></span>

<span data-ttu-id="cefd6-169">`teamMemberAdded`Событие отправляется на почтовый робот при первом добавлении в беседу и при каждом добавлении нового пользователя в команду или группу чата, в которой установлена программа-робот.</span><span class="sxs-lookup"><span data-stu-id="cefd6-169">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="cefd6-170">Сведения о пользователе (ID) уникальны для почтового робота и могут кэшироваться для последующего использования службой (например, для отправки сообщения определенному пользователю).</span><span class="sxs-lookup"><span data-stu-id="cefd6-170">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<ChannelAccount> membersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersAdded)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // Send a message to introduce the bot to the team
            var heroCard = new HeroCard(text: $"The {member.Name} bot has joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-172">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-172">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersAddedEvent(async (membersAdded: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
                let newMembers: string = '';
                console.log(JSON.stringify(membersAdded));
                membersAdded.forEach((account) => {
                    newMembers += account.id + ' ';
                });
                const name = !teamInfo ? 'not in team' : teamInfo.name;
                const card = CardFactory.heroCard('Account Added', `${newMembers} joined ${name}.`);
                const message = MessageFactory.attachment(card);
                await turnContext.sendActivity(message);
                await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="cefd6-173">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-173">JSON</span></span>](#tab/json)

<span data-ttu-id="cefd6-174">Это сообщение, которое будет получать ваш почтовый робот при добавлении в **команду**ленты.</span><span class="sxs-lookup"><span data-stu-id="cefd6-174">This is the message your bot will receive when the bot is added **to a team**.</span></span>

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

<span data-ttu-id="cefd6-175">Это сообщение, которое будет получать ваш почтовый робот при добавлении ленты \**в чат "один к одному*".</span><span class="sxs-lookup"><span data-stu-id="cefd6-175">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

# <a name="python"></a>[<span data-ttu-id="cefd6-176">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-176">Python</span></span>](#tab/python)

```python
async def on_teams_members_added_activity(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

* * *

### <a name="team-members-removed"></a><span data-ttu-id="cefd6-177">Удалены участники группы</span><span class="sxs-lookup"><span data-stu-id="cefd6-177">Team members removed</span></span>

<span data-ttu-id="cefd6-178">`teamMemberRemoved`Событие отправляется в Bot, если оно удалено из команды и каждый раз, когда какой-либо пользователь удаляется из команды, участником которой является пользователь Bot.</span><span class="sxs-lookup"><span data-stu-id="cefd6-178">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="cefd6-179">Вы можете определить, был ли удаленный участник участником "bot" или пользователем, изучив `Activity` объект `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="cefd6-179">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="cefd6-180">Если `Id` поле объекта совпадает с `MembersRemoved` `Id` полем `Recipient` объекта, то член удален, а в противном случае — пользователь.</span><span class="sxs-lookup"><span data-stu-id="cefd6-180">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise it is a user.</span></span>  <span data-ttu-id="cefd6-181">Как правило, в качестве ленты `Id` будет использоваться: `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="cefd6-181">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="cefd6-182">Когда пользователь безвозвратно удален из клиента, `membersRemoved conversationUpdate` инициируется событие.</span><span class="sxs-lookup"><span data-stu-id="cefd6-182">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-183">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-183">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersRemovedAsync(IList<ChannelAccount> membersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersRemoved)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // The bot was removed
            // You should clear any cached data you have for this team
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} was removed from {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-184">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-184">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersRemovedEvent(async (membersRemoved: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            let removedMembers: string = '';
            console.log(JSON.stringify(membersRemoved));
            membersRemoved.forEach((account) => {
                removedMembers += account.id + ' ';
            });
            const name = !teamInfo ? 'not in team' : teamInfo.name;
            const card = CardFactory.heroCard('Account Removed', `${removedMembers} removed from ${teamInfo.name}.`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="cefd6-185">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-185">JSON</span></span>](#tab/json)

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```


# <a name="python"></a>[<span data-ttu-id="cefd6-186">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-186">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed_activity(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to your team member {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="cefd6-187">Команда переименована</span><span class="sxs-lookup"><span data-stu-id="cefd6-187">Team renamed</span></span>

<span data-ttu-id="cefd6-188">Ваш робот получает уведомление, когда группа, в которую она находится, была переименована.</span><span class="sxs-lookup"><span data-stu-id="cefd6-188">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="cefd6-189">Он получает `conversationUpdate` событие `eventType.teamRenamed` в `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="cefd6-189">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-190">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-190">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-191">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-191">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamRenamedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team Renamed', `${teamInfo.name} is the new Team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="cefd6-192">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-192">JSON</span></span>](#tab/json)

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```


# <a name="python"></a>[<span data-ttu-id="cefd6-193">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-193">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed_activity(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="cefd6-194">События реакции сообщений</span><span class="sxs-lookup"><span data-stu-id="cefd6-194">Message reaction events</span></span>

<span data-ttu-id="cefd6-195">`messageReaction`Событие отправляется, когда пользователь добавляет или удаляет реакции на сообщение, отправленное вашим роботом.</span><span class="sxs-lookup"><span data-stu-id="cefd6-195">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="cefd6-196">`replyToId`Содержит идентификатор определенного сообщения, а также `Type` тип реакции в текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="cefd6-196">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="cefd6-197">К типам реакции относятся: "Ангри", "сердце", "лаугх", "Like", "грустный", "удивленный".</span><span class="sxs-lookup"><span data-stu-id="cefd6-197">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="cefd6-198">Это событие не содержит содержимое исходного сообщения, поэтому если обработка реакции на сообщения очень важна для ленты, необходимо сохранить сообщения при их отправке.</span><span class="sxs-lookup"><span data-stu-id="cefd6-198">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="cefd6-199">EventType</span><span class="sxs-lookup"><span data-stu-id="cefd6-199">EventType</span></span>       | <span data-ttu-id="cefd6-200">Объект полезных данных</span><span class="sxs-lookup"><span data-stu-id="cefd6-200">Payload object</span></span>   | <span data-ttu-id="cefd6-201">Описание</span><span class="sxs-lookup"><span data-stu-id="cefd6-201">Description</span></span>                                                             | <span data-ttu-id="cefd6-202">Область</span><span class="sxs-lookup"><span data-stu-id="cefd6-202">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="cefd6-203">мессажереактион</span><span class="sxs-lookup"><span data-stu-id="cefd6-203">messageReaction</span></span> | <span data-ttu-id="cefd6-204">реактионсаддед</span><span class="sxs-lookup"><span data-stu-id="cefd6-204">reactionsAdded</span></span>   | [<span data-ttu-id="cefd6-205">Реакция на сообщение Bot</span><span class="sxs-lookup"><span data-stu-id="cefd6-205">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="cefd6-206">Все</span><span class="sxs-lookup"><span data-stu-id="cefd6-206">All</span></span>   |
| <span data-ttu-id="cefd6-207">мессажереактион</span><span class="sxs-lookup"><span data-stu-id="cefd6-207">messageReaction</span></span> | <span data-ttu-id="cefd6-208">реактионсремовед</span><span class="sxs-lookup"><span data-stu-id="cefd6-208">reactionsRemoved</span></span> | [<span data-ttu-id="cefd6-209">Реакция, удаленная из сообщения Bot</span><span class="sxs-lookup"><span data-stu-id="cefd6-209">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="cefd6-210">Все</span><span class="sxs-lookup"><span data-stu-id="cefd6-210">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="cefd6-211">Реакции на сообщение Bot</span><span class="sxs-lookup"><span data-stu-id="cefd6-211">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-212">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-212">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsAddedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You reacted with '{reaction.Type}' to the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-213">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-213">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- Verify -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsAdded(async (context, next) => {
           const reactionsAdded = context.activity.reactionsAdded;
            if (reactionsAdded && reactionsAdded.length > 0) {
                for (let i = 0; i < reactionsAdded.length; i++) {
                    const reaction = reactionsAdded[i];
                    const newReaction = `You reacted with '${reaction.type}' to the following message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="cefd6-214">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-214">JSON</span></span>](#tab/json)

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="cefd6-215">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-215">Python</span></span>](#tab/python)

```python
async def on_reactions_added(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You added '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="cefd6-216">Реакции, удаленные из сообщения Bot</span><span class="sxs-lookup"><span data-stu-id="cefd6-216">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cefd6-217">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cefd6-217">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsRemovedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You removed the reaction '{reaction.Type}' from the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="cefd6-218">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="cefd6-218">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- Verify -->

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsRemoved(async(context,next)=>{
            const reactionsRemoved = context.activity.reactionsRemoved;
            if (reactionsRemoved && reactionsRemoved.length > 0) {
                for (let i = 0; i < reactionsRemoved.length; i++) {
                    const reaction = reactionsRemoved[i];
                    const newReaction = `You removed the reaction '${reaction.type}' from the message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="cefd6-219">JSON</span><span class="sxs-lookup"><span data-stu-id="cefd6-219">JSON</span></span>](#tab/json)

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="cefd6-220">Python</span><span class="sxs-lookup"><span data-stu-id="cefd6-220">Python</span></span>](#tab/python)

```python
async def on_reactions_removed(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You removed '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *
