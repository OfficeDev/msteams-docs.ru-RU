---
title: Подписаться на события разговора
author: WashingtonKayaker
description: Как подписаться на события бесед от бота Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: b4dc70e4619043bd0b675206770093b086fc5ec6
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014322"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="50e56-103">Подписаться на события разговора</span><span class="sxs-lookup"><span data-stu-id="50e56-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="50e56-104">Microsoft Teams отправляет боту уведомления о событиях, которые происходят в тех случаях, когда бот активен.</span><span class="sxs-lookup"><span data-stu-id="50e56-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="50e56-105">Вы можете зафиксировать эти события в коде и принять с ними меры, например:</span><span class="sxs-lookup"><span data-stu-id="50e56-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="50e56-106">Запуск приветствия при добавлении бота в команду</span><span class="sxs-lookup"><span data-stu-id="50e56-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="50e56-107">Запуск приветствия при добавлении или удалении нового участника группы</span><span class="sxs-lookup"><span data-stu-id="50e56-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="50e56-108">Запуск уведомления при его запуске, переименовании или удалении</span><span class="sxs-lookup"><span data-stu-id="50e56-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="50e56-109">Если сообщение бота нравится пользователю</span><span class="sxs-lookup"><span data-stu-id="50e56-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="50e56-110">События обновления беседы</span><span class="sxs-lookup"><span data-stu-id="50e56-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="50e56-111">Новые события можно добавлять в любое время, и ваш бот начнет их получать.</span><span class="sxs-lookup"><span data-stu-id="50e56-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="50e56-112">Необходимо проработать возможность получения непредвиденных событий.</span><span class="sxs-lookup"><span data-stu-id="50e56-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="50e56-113">Если вы используете SDK Bot Framework, бот автоматически ответит на любые события, которые вы `200 - OK` не решите обработать.</span><span class="sxs-lookup"><span data-stu-id="50e56-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="50e56-114">Бот получает событие при добавлении в беседу, добавлении или удалении других участников беседы или изменения метаданных `conversationUpdate` беседы.</span><span class="sxs-lookup"><span data-stu-id="50e56-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="50e56-115">Это событие отправляется боту, когда он получает сведения об обновлениях членства для `conversationUpdate` команд, в которые оно было добавлено.</span><span class="sxs-lookup"><span data-stu-id="50e56-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="50e56-116">Кроме того, он получает обновление при первом добавлении специально для личных бесед.</span><span class="sxs-lookup"><span data-stu-id="50e56-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="50e56-117">В следующей таблице показан список событий обновления бесед Teams со ссылками на дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="50e56-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="50e56-118">Предпринятые действия</span><span class="sxs-lookup"><span data-stu-id="50e56-118">Action Taken</span></span>        | <span data-ttu-id="50e56-119">EventType</span><span class="sxs-lookup"><span data-stu-id="50e56-119">EventType</span></span>         | <span data-ttu-id="50e56-120">Метод called</span><span class="sxs-lookup"><span data-stu-id="50e56-120">Method Called</span></span>              | <span data-ttu-id="50e56-121">Описание</span><span class="sxs-lookup"><span data-stu-id="50e56-121">Description</span></span>                | <span data-ttu-id="50e56-122">Область</span><span class="sxs-lookup"><span data-stu-id="50e56-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="50e56-123">канал создан</span><span class="sxs-lookup"><span data-stu-id="50e56-123">channel created</span></span>     | <span data-ttu-id="50e56-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="50e56-124">channelCreated</span></span>    | <span data-ttu-id="50e56-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="50e56-126">Канал создан</span><span class="sxs-lookup"><span data-stu-id="50e56-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="50e56-127">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-127">Team</span></span> |
| <span data-ttu-id="50e56-128">channel renamed</span><span class="sxs-lookup"><span data-stu-id="50e56-128">channel renamed</span></span>     | <span data-ttu-id="50e56-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="50e56-129">channelRenamed</span></span>    | <span data-ttu-id="50e56-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="50e56-131">Канал был переименован</span><span class="sxs-lookup"><span data-stu-id="50e56-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="50e56-132">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-132">Team</span></span> |
| <span data-ttu-id="50e56-133">канал удален</span><span class="sxs-lookup"><span data-stu-id="50e56-133">channel deleted</span></span>     | <span data-ttu-id="50e56-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="50e56-134">channelDeleted</span></span>    | <span data-ttu-id="50e56-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="50e56-136">Канал был удален</span><span class="sxs-lookup"><span data-stu-id="50e56-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="50e56-137">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-137">Team</span></span> |
| <span data-ttu-id="50e56-138">восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="50e56-138">channel restored</span></span>    | <span data-ttu-id="50e56-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="50e56-139">channelRestored</span></span>    | <span data-ttu-id="50e56-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="50e56-141">Канал был восстановлен</span><span class="sxs-lookup"><span data-stu-id="50e56-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="50e56-142">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-142">Team</span></span> |
| <span data-ttu-id="50e56-143">добавлены члены</span><span class="sxs-lookup"><span data-stu-id="50e56-143">members added</span></span>   | <span data-ttu-id="50e56-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="50e56-144">membersAdded</span></span>   | <span data-ttu-id="50e56-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="50e56-146">Добавлен участник</span><span class="sxs-lookup"><span data-stu-id="50e56-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="50e56-147">Все</span><span class="sxs-lookup"><span data-stu-id="50e56-147">All</span></span> |
| <span data-ttu-id="50e56-148">удалены члены</span><span class="sxs-lookup"><span data-stu-id="50e56-148">members removed</span></span> | <span data-ttu-id="50e56-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="50e56-149">membersRemoved</span></span> | <span data-ttu-id="50e56-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="50e56-151">Член был удален</span><span class="sxs-lookup"><span data-stu-id="50e56-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="50e56-152">groupChat & команды</span><span class="sxs-lookup"><span data-stu-id="50e56-152">groupChat & team</span></span> |
| <span data-ttu-id="50e56-153">команда переименована</span><span class="sxs-lookup"><span data-stu-id="50e56-153">team renamed</span></span>        | <span data-ttu-id="50e56-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="50e56-154">teamRenamed</span></span>       | <span data-ttu-id="50e56-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="50e56-156">Команда была переименована</span><span class="sxs-lookup"><span data-stu-id="50e56-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="50e56-157">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-157">Team</span></span> |
| <span data-ttu-id="50e56-158">команда удалена</span><span class="sxs-lookup"><span data-stu-id="50e56-158">team deleted</span></span>        | <span data-ttu-id="50e56-159">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="50e56-159">teamDeleted</span></span>       | <span data-ttu-id="50e56-160">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-160">OnTeamsTeamDeletedAsync</span></span>    | [<span data-ttu-id="50e56-161">Команда удалена</span><span class="sxs-lookup"><span data-stu-id="50e56-161">A Team was deleted</span></span>](#team-deleted)       | <span data-ttu-id="50e56-162">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-162">Team</span></span> |
| <span data-ttu-id="50e56-163">team archived</span><span class="sxs-lookup"><span data-stu-id="50e56-163">team archived</span></span>        | <span data-ttu-id="50e56-164">teamArchived</span><span class="sxs-lookup"><span data-stu-id="50e56-164">teamArchived</span></span>       | <span data-ttu-id="50e56-165">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-165">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="50e56-166">Архивировать команду</span><span class="sxs-lookup"><span data-stu-id="50e56-166">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="50e56-167">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-167">Team</span></span> |
| <span data-ttu-id="50e56-168">команда, неархивная</span><span class="sxs-lookup"><span data-stu-id="50e56-168">team unarchived</span></span>        | <span data-ttu-id="50e56-169">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="50e56-169">teamUnarchived</span></span>       | <span data-ttu-id="50e56-170">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-170">OnTeamsTeamUnarchivedAsync</span></span>    | [<span data-ttu-id="50e56-171">Команда не была вархивовлена</span><span class="sxs-lookup"><span data-stu-id="50e56-171">A Team was unarchived</span></span>](#team-unarchived)       | <span data-ttu-id="50e56-172">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-172">Team</span></span> |
| <span data-ttu-id="50e56-173">команда восстановлена</span><span class="sxs-lookup"><span data-stu-id="50e56-173">team restored</span></span>        | <span data-ttu-id="50e56-174">teamRestored</span><span class="sxs-lookup"><span data-stu-id="50e56-174">teamRestored</span></span>      | <span data-ttu-id="50e56-175">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="50e56-175">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="50e56-176">Команда восстановлена</span><span class="sxs-lookup"><span data-stu-id="50e56-176">A Team was restored</span></span>](#team-restored)       | <span data-ttu-id="50e56-177">Команда</span><span class="sxs-lookup"><span data-stu-id="50e56-177">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="50e56-178">Канал создан</span><span class="sxs-lookup"><span data-stu-id="50e56-178">Channel created</span></span>

<span data-ttu-id="50e56-179">Событие, созданное каналом, отправляется вашему боту всякий раз, когда в команде создается новый канал, в который устанавливается бот.</span><span class="sxs-lookup"><span data-stu-id="50e56-179">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-180">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-181">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-181">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-182">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-182">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="50e56-183">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-183">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="50e56-184">Канал переименован</span><span class="sxs-lookup"><span data-stu-id="50e56-184">Channel renamed</span></span>

<span data-ttu-id="50e56-185">Событие переименования канала отправляется вашему боту при переименовании канала в команде, в которая установлен бот.</span><span class="sxs-lookup"><span data-stu-id="50e56-185">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-186">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-186">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-187">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-187">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-188">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="50e56-189">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-189">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="50e56-190">Канал удален</span><span class="sxs-lookup"><span data-stu-id="50e56-190">Channel Deleted</span></span>

<span data-ttu-id="50e56-191">Событие удаления канала отправляется вашему боту при удалении канала в команде, в которая установлен этот бот.</span><span class="sxs-lookup"><span data-stu-id="50e56-191">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-193">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-194">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-194">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="50e56-195">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-195">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="50e56-196">Канал восстановлен</span><span class="sxs-lookup"><span data-stu-id="50e56-196">Channel restored</span></span>

<span data-ttu-id="50e56-197">Восстановленное событие канала отправляется боту всякий раз, когда ранее удаленный канал восстанавливается в команде, в которую уже установлен бот.</span><span class="sxs-lookup"><span data-stu-id="50e56-197">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-199">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-199">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRestoredEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Restored', `${channelInfo.name} is the Channel restored`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="50e56-200">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-200">JSON</span></span>](#tab/json)

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
        "eventType": "channelRestored",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="50e56-201">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-201">Python</span></span>](#tab/python)

```python
async def on_teams_channel_restored(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The restored channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="50e56-202">Добавлены участники команды</span><span class="sxs-lookup"><span data-stu-id="50e56-202">Team members added</span></span>

<span data-ttu-id="50e56-203">Это событие отправляется боту при первом добавлении в беседу и при каждом добавлении нового пользователя в команду или групповой чат, в который устанавливается `teamMemberAdded` бот.</span><span class="sxs-lookup"><span data-stu-id="50e56-203">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="50e56-204">Сведения о пользователе (ID) уникальны для вашего бота и могут кэшться для дальнейшего использования вашей службой (например, отправки сообщения определенному пользователю).</span><span class="sxs-lookup"><span data-stu-id="50e56-204">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-205">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-205">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded , TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in teamsMembersAdded)
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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-206">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-206">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-207">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-207">JSON</span></span>](#tab/json)

<span data-ttu-id="50e56-208">Это сообщение, которое ваш бот получит при добавлении бота **в команду.**</span><span class="sxs-lookup"><span data-stu-id="50e56-208">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="50e56-209">Это сообщение, которое ваш бот получит при добавлении бота \* в один *к одному чату.*</span><span class="sxs-lookup"><span data-stu-id="50e56-209">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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
    "aadObjectId": "**_"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "_*_"
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

# <a name="python"></a>[<span data-ttu-id="50e56-210">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-210">Python</span></span>](#tab/python)

```python
async def on_teams_members_added(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

<span data-ttu-id="50e56-211">_ \* \*</span><span class="sxs-lookup"><span data-stu-id="50e56-211">_ \* \*</span></span>

### <a name="team-members-removed"></a><span data-ttu-id="50e56-212">Участники команды удалены</span><span class="sxs-lookup"><span data-stu-id="50e56-212">Team members removed</span></span>

<span data-ttu-id="50e56-213">Это событие отправляется вашему боту, если оно удаляется из команды и каждый раз, когда любой пользователь удаляется из команды, участником которую является `teamMemberRemoved` ваш бот.</span><span class="sxs-lookup"><span data-stu-id="50e56-213">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="50e56-214">Вы можете определить, был ли новый член удален самим ботом или пользователем, посмотрев на `Activity` объект `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="50e56-214">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="50e56-215">Если поле объекта такое же, как и поле объекта, удаляемая член является ботом, в противном случае `Id` `MembersRemoved` это `Id` `Recipient` пользователь.</span><span class="sxs-lookup"><span data-stu-id="50e56-215">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="50e56-216">Бот, как `Id` правило, будет: `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="50e56-216">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="50e56-217">Когда пользователь окончательно удаляется из клиента, `membersRemoved conversationUpdate` инициирует событие.</span><span class="sxs-lookup"><span data-stu-id="50e56-217">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-218">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-218">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-219">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-219">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-220">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-220">JSON</span></span>](#tab/json)

<span data-ttu-id="50e56-221">Объект в следующем примере полезной нагрузки основан на добавлении участника в команду вместо группового чата или инициировании новой беседы "один `channelData` к одному":</span><span class="sxs-lookup"><span data-stu-id="50e56-221">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="50e56-222">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-222">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="50e56-223">Команда переименована</span><span class="sxs-lookup"><span data-stu-id="50e56-223">Team renamed</span></span>

<span data-ttu-id="50e56-224">Бот будет уведомлен о переименовании команды.</span><span class="sxs-lookup"><span data-stu-id="50e56-224">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="50e56-225">Он получает событие `conversationUpdate` в `eventType.teamRenamed` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="50e56-225">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-226">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-226">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-227">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-227">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-228">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-228">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="50e56-229">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-229">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="50e56-230">Команда удалена</span><span class="sxs-lookup"><span data-stu-id="50e56-230">Team deleted</span></span>

<span data-ttu-id="50e56-231">Бот будет уведомлен об удалении команды.</span><span class="sxs-lookup"><span data-stu-id="50e56-231">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="50e56-232">Он получает событие `conversationUpdate` в `eventType.teamDeleted` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="50e56-232">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-233">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-233">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-234">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-234">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamDeletedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            //handle delete event
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="50e56-235">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-235">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamDeleted",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="50e56-236">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-236">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="50e56-237">Команда восстановлена</span><span class="sxs-lookup"><span data-stu-id="50e56-237">Team restored</span></span>

<span data-ttu-id="50e56-238">Бот получает уведомление при восстановлении после удаления.</span><span class="sxs-lookup"><span data-stu-id="50e56-238">The bot receives a notification when it is restored from deletion.</span></span> <span data-ttu-id="50e56-239">Он получает событие `conversationUpdate` в `eventType.teamrestored` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="50e56-239">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-241">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-241">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamrestoredEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team restored', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="50e56-242">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-242">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamrestored",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="50e56-243">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-243">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="50e56-244">Архивная группа</span><span class="sxs-lookup"><span data-stu-id="50e56-244">Team archived</span></span>

<span data-ttu-id="50e56-245">Бот получает уведомление о том, что установленная в нем команда архивна.</span><span class="sxs-lookup"><span data-stu-id="50e56-245">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="50e56-246">Он получает событие `conversationUpdate` в `eventType.teamarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="50e56-246">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-248">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-248">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamArchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="50e56-249">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-249">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamArchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="50e56-250">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="50e56-251">Команда, не вархивная</span><span class="sxs-lookup"><span data-stu-id="50e56-251">Team unarchived</span></span>

<span data-ttu-id="50e56-252">Бот получает уведомление о том, что установленная в нем команда не является искомой.</span><span class="sxs-lookup"><span data-stu-id="50e56-252">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="50e56-253">Он получает событие `conversationUpdate` в `eventType.teamUnarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="50e56-253">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-254">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-254">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-255">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-255">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamUnarchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="50e56-256">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-256">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamUnarchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="50e56-257">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-257">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="50e56-258">События реакции на сообщения</span><span class="sxs-lookup"><span data-stu-id="50e56-258">Message reaction events</span></span>

<span data-ttu-id="50e56-259">Событие отправляется, когда пользователь добавляет или удаляет реакции на `messageReaction` сообщение, отправленное вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="50e56-259">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="50e56-260">Содержит ИД конкретного сообщения и тип реакции в `replyToId` `Type` текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="50e56-260">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="50e56-261">К типам реакции относятся : "за", "heart", "в", "like", "Клык", "удивитесь".</span><span class="sxs-lookup"><span data-stu-id="50e56-261">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="50e56-262">Это событие не содержит содержимого исходного сообщения, поэтому если обработка реакции на ваши сообщения важна для вашего бота, вам потребуется сохранить сообщения при их отправке.</span><span class="sxs-lookup"><span data-stu-id="50e56-262">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="50e56-263">EventType</span><span class="sxs-lookup"><span data-stu-id="50e56-263">EventType</span></span>       | <span data-ttu-id="50e56-264">Объект Payload</span><span class="sxs-lookup"><span data-stu-id="50e56-264">Payload object</span></span>   | <span data-ttu-id="50e56-265">Описание</span><span class="sxs-lookup"><span data-stu-id="50e56-265">Description</span></span>                                                             | <span data-ttu-id="50e56-266">Область</span><span class="sxs-lookup"><span data-stu-id="50e56-266">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="50e56-267">messageReaction</span><span class="sxs-lookup"><span data-stu-id="50e56-267">messageReaction</span></span> | <span data-ttu-id="50e56-268">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="50e56-268">reactionsAdded</span></span>   | [<span data-ttu-id="50e56-269">Реакция на сообщение бота</span><span class="sxs-lookup"><span data-stu-id="50e56-269">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="50e56-270">Все</span><span class="sxs-lookup"><span data-stu-id="50e56-270">All</span></span>   |
| <span data-ttu-id="50e56-271">messageReaction</span><span class="sxs-lookup"><span data-stu-id="50e56-271">messageReaction</span></span> | <span data-ttu-id="50e56-272">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="50e56-272">reactionsRemoved</span></span> | [<span data-ttu-id="50e56-273">Реакция, удаленная из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="50e56-273">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="50e56-274">Все</span><span class="sxs-lookup"><span data-stu-id="50e56-274">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="50e56-275">Реакции на сообщение бота</span><span class="sxs-lookup"><span data-stu-id="50e56-275">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-276">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-276">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-277">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-277">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-278">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-278">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="50e56-279">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-279">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="50e56-280">Реакции удалены из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="50e56-280">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="50e56-281">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="50e56-281">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="50e56-282">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="50e56-282">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="50e56-283">JSON</span><span class="sxs-lookup"><span data-stu-id="50e56-283">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="50e56-284">Python</span><span class="sxs-lookup"><span data-stu-id="50e56-284">Python</span></span>](#tab/python)

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

## <a name="samples"></a><span data-ttu-id="50e56-285">Примеры</span><span class="sxs-lookup"><span data-stu-id="50e56-285">Samples</span></span>
<span data-ttu-id="50e56-286">Пример кода с событиями бесед ботов см. в:</span><span class="sxs-lookup"><span data-stu-id="50e56-286">For sample code showing the bots conversation events, see:</span></span>

[<span data-ttu-id="50e56-287">Пример событий бесед ботов Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="50e56-287">Microsoft Teams bots conversation events sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)



