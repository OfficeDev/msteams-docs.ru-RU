---
title: Подписаться на события разговора
author: WashingtonKayaker
description: Подписка на события беседы из бота Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bc4ae36d8cffe5b19ee778a71e1c7b1c00c5e88c
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634504"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="f4a3f-103">Подписаться на события разговора</span><span class="sxs-lookup"><span data-stu-id="f4a3f-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="f4a3f-104">Microsoft Teams отправляет вашему боту уведомления о событиях в тех областях, где этот бот активен.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="f4a3f-105">Эти события можно обрабатывать в коде и выполнять с ними те или иные действия, например:</span><span class="sxs-lookup"><span data-stu-id="f4a3f-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="f4a3f-106">Запуск приветствия при добавлении бота в команду</span><span class="sxs-lookup"><span data-stu-id="f4a3f-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="f4a3f-107">Запуск приветствия при добавлении или удалении нового члена группы</span><span class="sxs-lookup"><span data-stu-id="f4a3f-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="f4a3f-108">Запуск уведомления при запуске, переименовании или удалении канала</span><span class="sxs-lookup"><span data-stu-id="f4a3f-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="f4a3f-109">Если сообщение бота нравится пользователю</span><span class="sxs-lookup"><span data-stu-id="f4a3f-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="f4a3f-110">События обновления беседы</span><span class="sxs-lookup"><span data-stu-id="f4a3f-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="f4a3f-111">Новые события могут быть добавлены в любое время, и ваш бот начнет получать их.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="f4a3f-112">Необходимо разработать возможность получения неожиданных событий.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="f4a3f-113">Если вы используете SDK Bot Framework, ваш бот будет автоматически отвечать на любые события, которые `200 - OK` не будут обрабатываться.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="f4a3f-114">Бот получает событие `conversationUpdate`, когда его добавляют в беседу, когда в нее добавляются или из нее удаляются другие участники, а также при изменении метаданных беседы.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="f4a3f-115">Событие `conversationUpdate` отправляется боту, когда поступают сведения об обновлении членства в командах, куда он добавлен.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="f4a3f-116">Бот также получает обновление при первом добавлении в личную беседу.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="f4a3f-117">В следующей таблице показан список событий обновления беседы Teams с ссылками на дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="f4a3f-118">Действия, принятые</span><span class="sxs-lookup"><span data-stu-id="f4a3f-118">Action Taken</span></span>        | <span data-ttu-id="f4a3f-119">EventType</span><span class="sxs-lookup"><span data-stu-id="f4a3f-119">EventType</span></span>         | <span data-ttu-id="f4a3f-120">Вызван метод</span><span class="sxs-lookup"><span data-stu-id="f4a3f-120">Method Called</span></span>              | <span data-ttu-id="f4a3f-121">Описание</span><span class="sxs-lookup"><span data-stu-id="f4a3f-121">Description</span></span>                | <span data-ttu-id="f4a3f-122">Область</span><span class="sxs-lookup"><span data-stu-id="f4a3f-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="f4a3f-123">созданный канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-123">channel created</span></span>     | <span data-ttu-id="f4a3f-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="f4a3f-124">channelCreated</span></span>    | <span data-ttu-id="f4a3f-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="f4a3f-126">Создан канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="f4a3f-127">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-127">Team</span></span> |
| <span data-ttu-id="f4a3f-128">переименован канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-128">channel renamed</span></span>     | <span data-ttu-id="f4a3f-129">ChannelRenamed</span><span class="sxs-lookup"><span data-stu-id="f4a3f-129">channelRenamed</span></span>    | <span data-ttu-id="f4a3f-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="f4a3f-131">Канал был переименован</span><span class="sxs-lookup"><span data-stu-id="f4a3f-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="f4a3f-132">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-132">Team</span></span> |
| <span data-ttu-id="f4a3f-133">канал удален</span><span class="sxs-lookup"><span data-stu-id="f4a3f-133">channel deleted</span></span>     | <span data-ttu-id="f4a3f-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="f4a3f-134">channelDeleted</span></span>    | <span data-ttu-id="f4a3f-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="f4a3f-136">Канал был удален</span><span class="sxs-lookup"><span data-stu-id="f4a3f-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="f4a3f-137">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-137">Team</span></span> |
| <span data-ttu-id="f4a3f-138">восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-138">channel restored</span></span>    | <span data-ttu-id="f4a3f-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="f4a3f-139">channelRestored</span></span>    | <span data-ttu-id="f4a3f-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="f4a3f-141">Восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="f4a3f-142">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-142">Team</span></span> |
| <span data-ttu-id="f4a3f-143">добавлены участники</span><span class="sxs-lookup"><span data-stu-id="f4a3f-143">members added</span></span>   | <span data-ttu-id="f4a3f-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="f4a3f-144">membersAdded</span></span>   | <span data-ttu-id="f4a3f-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="f4a3f-146">Добавлен член</span><span class="sxs-lookup"><span data-stu-id="f4a3f-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="f4a3f-147">Все</span><span class="sxs-lookup"><span data-stu-id="f4a3f-147">All</span></span> |
| <span data-ttu-id="f4a3f-148">удалены члены</span><span class="sxs-lookup"><span data-stu-id="f4a3f-148">members removed</span></span> | <span data-ttu-id="f4a3f-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="f4a3f-149">membersRemoved</span></span> | <span data-ttu-id="f4a3f-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="f4a3f-151">Был удален член</span><span class="sxs-lookup"><span data-stu-id="f4a3f-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="f4a3f-152">группа & groupChat</span><span class="sxs-lookup"><span data-stu-id="f4a3f-152">groupChat & team</span></span> |
| <span data-ttu-id="f4a3f-153">переименованная команда</span><span class="sxs-lookup"><span data-stu-id="f4a3f-153">team renamed</span></span>        | <span data-ttu-id="f4a3f-154">переименованная команда</span><span class="sxs-lookup"><span data-stu-id="f4a3f-154">teamRenamed</span></span>       | <span data-ttu-id="f4a3f-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="f4a3f-156">Команда была переименована</span><span class="sxs-lookup"><span data-stu-id="f4a3f-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="f4a3f-157">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-157">Team</span></span> |
| <span data-ttu-id="f4a3f-158">удалена команда</span><span class="sxs-lookup"><span data-stu-id="f4a3f-158">team deleted</span></span>        | <span data-ttu-id="f4a3f-159">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="f4a3f-159">teamDeleted</span></span>       | <span data-ttu-id="f4a3f-160">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-160">OnTeamsTeamDeletedAsync</span></span>    | [<span data-ttu-id="f4a3f-161">Команда была удалена</span><span class="sxs-lookup"><span data-stu-id="f4a3f-161">A Team was deleted</span></span>](#team-deleted)       | <span data-ttu-id="f4a3f-162">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-162">Team</span></span> |
| <span data-ttu-id="f4a3f-163">архивировать команду</span><span class="sxs-lookup"><span data-stu-id="f4a3f-163">team archived</span></span>        | <span data-ttu-id="f4a3f-164">teamArchived</span><span class="sxs-lookup"><span data-stu-id="f4a3f-164">teamArchived</span></span>       | <span data-ttu-id="f4a3f-165">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-165">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="f4a3f-166">В архиве была архивная группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-166">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="f4a3f-167">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-167">Team</span></span> |
| <span data-ttu-id="f4a3f-168">команда без анархии</span><span class="sxs-lookup"><span data-stu-id="f4a3f-168">team unarchived</span></span>        | <span data-ttu-id="f4a3f-169">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="f4a3f-169">teamUnarchived</span></span>       | <span data-ttu-id="f4a3f-170">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-170">OnTeamsTeamUnarchivedAsync</span></span>    | [<span data-ttu-id="f4a3f-171">Команда не была анархивна</span><span class="sxs-lookup"><span data-stu-id="f4a3f-171">A Team was unarchived</span></span>](#team-unarchived)       | <span data-ttu-id="f4a3f-172">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-172">Team</span></span> |
| <span data-ttu-id="f4a3f-173">восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="f4a3f-173">team restored</span></span>        | <span data-ttu-id="f4a3f-174">teamRestored</span><span class="sxs-lookup"><span data-stu-id="f4a3f-174">teamRestored</span></span>      | <span data-ttu-id="f4a3f-175">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="f4a3f-175">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="f4a3f-176">Команда была восстановлена</span><span class="sxs-lookup"><span data-stu-id="f4a3f-176">A Team was restored</span></span>](#team-restored)       | <span data-ttu-id="f4a3f-177">Группа</span><span class="sxs-lookup"><span data-stu-id="f4a3f-177">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="f4a3f-178">Созданный канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-178">Channel created</span></span>

<span data-ttu-id="f4a3f-179">Событие, созданное каналом, отправляется вашему боту всякий раз, когда новый канал создается в команде, в которая установлен бот.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-179">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-180">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-181">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-181">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-182">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-182">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-183">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-183">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="f4a3f-184">Переименован канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-184">Channel renamed</span></span>

<span data-ttu-id="f4a3f-185">Событие переименования канала отправляется вашему боту всякий раз, когда канал переименован в команде, в которая установлен бот.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-185">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-186">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-186">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-187">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-187">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-188">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-189">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-189">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="f4a3f-190">Удаленный канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-190">Channel Deleted</span></span>

<span data-ttu-id="f4a3f-191">Событие удаления канала отправляется вашему боту всякий раз, когда канал удаляется в команде, в которая установлен ваш бот.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-191">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-193">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-194">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-194">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-195">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-195">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="f4a3f-196">Восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="f4a3f-196">Channel restored</span></span>

<span data-ttu-id="f4a3f-197">Восстановленное событие канала отправляется в бот всякий раз, когда удаленный ранее канал восстанавливается в команде, в которую уже установлен бот.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-197">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-199">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-199">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-200">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-200">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-201">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-201">Python</span></span>](#tab/python)

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

### <a name="team-members-added"></a><span data-ttu-id="f4a3f-202">Добавлены участники группы</span><span class="sxs-lookup"><span data-stu-id="f4a3f-202">Team members added</span></span>

<span data-ttu-id="f4a3f-203">Событие отправляется боту при первом добавлении в беседу и при каждом добавлении нового пользователя в командный или групповой чат, в который установлен `teamMemberAdded` бот.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-203">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="f4a3f-204">Пользовательские сведения (ID) уникальны для вашего бота и могут быть кэшировали для дальнейшего использования службой (например, отправки сообщения конкретному пользователю).</span><span class="sxs-lookup"><span data-stu-id="f4a3f-204">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-205">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-205">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-206">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-206">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-207">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-207">JSON</span></span>](#tab/json)

<span data-ttu-id="f4a3f-208">Это сообщение, которое ваш бот получит при добавлении бота **в команду.**</span><span class="sxs-lookup"><span data-stu-id="f4a3f-208">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="f4a3f-209">Это сообщение, которое ваш бот получит при добавлении бота \* в чат один *к одному.*</span><span class="sxs-lookup"><span data-stu-id="f4a3f-209">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-210">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-210">Python</span></span>](#tab/python)

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

* * *

### <a name="team-members-removed"></a><span data-ttu-id="f4a3f-211">Удалены члены группы</span><span class="sxs-lookup"><span data-stu-id="f4a3f-211">Team members removed</span></span>

<span data-ttu-id="f4a3f-212">Событие отправляется вашему боту, если оно удаляется из группы и каждый раз, когда любой пользователь удаляется из команды, в которую входит `teamMemberRemoved` ваш бот.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-212">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="f4a3f-213">Вы можете определить, был ли удален новый участник самим ботом или пользователем, посмотрев объект `Activity` `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="f4a3f-213">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="f4a3f-214">Если поле объекта такое же, как и поле объекта, то удаляемого члена является бот, в противном случае он `Id` `MembersRemoved` является `Id` `Recipient` пользователем.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-214">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="f4a3f-215">Бот, как `Id` правило, будет: `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="f4a3f-215">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="f4a3f-216">При постоянном удалении пользователя из клиента `membersRemoved conversationUpdate` запускается событие.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-216">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-217">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-217">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-218">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-218">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-219">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-219">JSON</span></span>](#tab/json)

<span data-ttu-id="f4a3f-220">Объект в следующем примере полезной нагрузки основан на добавлении члена в команду, а не групповом чате или инициировании нового беседы один `channelData` к одному:</span><span class="sxs-lookup"><span data-stu-id="f4a3f-220">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="f4a3f-221">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-221">Python</span></span>](#tab/python)

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

### <a name="team-renamed"></a><span data-ttu-id="f4a3f-222">Переименована команда</span><span class="sxs-lookup"><span data-stu-id="f4a3f-222">Team renamed</span></span>

<span data-ttu-id="f4a3f-223">Ваш бот уведомлен о переименовании команды, в которая он находится.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-223">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="f4a3f-224">Он получает событие `conversationUpdate` в `eventType.teamRenamed` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-224">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-225">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-225">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-226">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-226">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-227">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-227">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-228">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-228">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="f4a3f-229">Удалена команда</span><span class="sxs-lookup"><span data-stu-id="f4a3f-229">Team deleted</span></span>

<span data-ttu-id="f4a3f-230">Ваш бот уведомлен об удалении команды.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-230">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="f4a3f-231">Он получает событие `conversationUpdate` в `eventType.teamDeleted` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-231">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-232">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-232">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-233">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-233">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-234">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-234">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-235">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-235">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="f4a3f-236">Восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="f4a3f-236">Team restored</span></span>

<span data-ttu-id="f4a3f-237">Бот получает уведомление о восстановлении группы после удаления.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-237">The bot receives a notification when the team is restored from deletion.</span></span> <span data-ttu-id="f4a3f-238">Бот получает событие `conversationUpdate` в `eventType.teamrestored` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-238">The bot receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-239">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-239">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-240">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-240">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-241">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-242">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="f4a3f-243">Архив команд</span><span class="sxs-lookup"><span data-stu-id="f4a3f-243">Team archived</span></span>

<span data-ttu-id="f4a3f-244">Бот получает уведомление, когда установленная в нем команда будет архивироваться.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-244">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="f4a3f-245">Он получает событие `conversationUpdate` в `eventType.teamarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-245">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-246">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-246">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-247">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-247">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-248">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-248">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-249">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-249">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="f4a3f-250">Команда без анархии</span><span class="sxs-lookup"><span data-stu-id="f4a3f-250">Team unarchived</span></span>

<span data-ttu-id="f4a3f-251">Бот получает уведомление, когда установленная в нем команда не является анархивной.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-251">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="f4a3f-252">Он получает событие `conversationUpdate` в `eventType.teamUnarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-252">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-253">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-253">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-254">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-254">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-255">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-255">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-256">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-256">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="f4a3f-257">События реакции на сообщения</span><span class="sxs-lookup"><span data-stu-id="f4a3f-257">Message reaction events</span></span>

<span data-ttu-id="f4a3f-258">Событие отправляется, когда пользователь добавляет или удаляет отклики на `messageReaction` сообщение, отправленное ботом.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-258">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="f4a3f-259">Содержит ID конкретного сообщения и тип реакции `replyToId` `Type` в текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-259">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="f4a3f-260">Типы реакций: "злой", "сердечный", "смех", "like", "Sad", "surprised".</span><span class="sxs-lookup"><span data-stu-id="f4a3f-260">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="f4a3f-261">Это событие не содержит содержимое исходного сообщения, поэтому если обработка реакций на сообщения важна для вашего бота, вам потребуется хранить сообщения при их отправке.</span><span class="sxs-lookup"><span data-stu-id="f4a3f-261">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="f4a3f-262">EventType</span><span class="sxs-lookup"><span data-stu-id="f4a3f-262">EventType</span></span>       | <span data-ttu-id="f4a3f-263">Объект полезной нагрузки</span><span class="sxs-lookup"><span data-stu-id="f4a3f-263">Payload object</span></span>   | <span data-ttu-id="f4a3f-264">Описание</span><span class="sxs-lookup"><span data-stu-id="f4a3f-264">Description</span></span>                                                             | <span data-ttu-id="f4a3f-265">Область</span><span class="sxs-lookup"><span data-stu-id="f4a3f-265">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="f4a3f-266">messageReaction</span><span class="sxs-lookup"><span data-stu-id="f4a3f-266">messageReaction</span></span> | <span data-ttu-id="f4a3f-267">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="f4a3f-267">reactionsAdded</span></span>   | [<span data-ttu-id="f4a3f-268">Реакция на сообщение бота</span><span class="sxs-lookup"><span data-stu-id="f4a3f-268">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="f4a3f-269">Все</span><span class="sxs-lookup"><span data-stu-id="f4a3f-269">All</span></span>   |
| <span data-ttu-id="f4a3f-270">messageReaction</span><span class="sxs-lookup"><span data-stu-id="f4a3f-270">messageReaction</span></span> | <span data-ttu-id="f4a3f-271">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="f4a3f-271">reactionsRemoved</span></span> | [<span data-ttu-id="f4a3f-272">Реакция, удаленная из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="f4a3f-272">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="f4a3f-273">Все</span><span class="sxs-lookup"><span data-stu-id="f4a3f-273">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="f4a3f-274">Реакция на сообщение бота</span><span class="sxs-lookup"><span data-stu-id="f4a3f-274">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-275">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-275">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-276">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-276">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-277">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-277">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-278">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-278">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="f4a3f-279">Реакции, удаленые из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="f4a3f-279">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f4a3f-280">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f4a3f-280">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f4a3f-281">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f4a3f-281">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="f4a3f-282">JSON</span><span class="sxs-lookup"><span data-stu-id="f4a3f-282">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="f4a3f-283">Python</span><span class="sxs-lookup"><span data-stu-id="f4a3f-283">Python</span></span>](#tab/python)

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

## <a name="samples"></a><span data-ttu-id="f4a3f-284">Примеры</span><span class="sxs-lookup"><span data-stu-id="f4a3f-284">Samples</span></span>

<span data-ttu-id="f4a3f-285">Пример кода с событиями беседы ботов см. в примере:</span><span class="sxs-lookup"><span data-stu-id="f4a3f-285">For sample code showing the bots conversation events, see:</span></span>

[<span data-ttu-id="f4a3f-286">Пример событий беседы в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f4a3f-286">Microsoft Teams bots conversation events sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)



