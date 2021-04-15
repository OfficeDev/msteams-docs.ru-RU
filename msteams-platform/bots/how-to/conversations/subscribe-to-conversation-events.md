---
title: События беседы
author: WashingtonKayaker
description: Работа с событиями беседы с помощью бота Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: af06dba58b3784a03dbcbbc627fa38fce681eeb8
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696348"
---
# <a name="conversation-events-in-your-teams-bot"></a><span data-ttu-id="af6f6-103">События беседы в боте Teams</span><span class="sxs-lookup"><span data-stu-id="af6f6-103">Conversation events in your Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="af6f6-104">При создании разговорных ботов для Microsoft Teams можно работать с событиями беседы.</span><span class="sxs-lookup"><span data-stu-id="af6f6-104">When building your conversational bots for Microsoft Teams, you can work with conversation events.</span></span> <span data-ttu-id="af6f6-105">Teams отправляет уведомления вашему боту для событий беседы, которые происходят в сферах, где ваш бот активен.</span><span class="sxs-lookup"><span data-stu-id="af6f6-105">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="af6f6-106">Эти события можно зафиксировать в коде и принять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="af6f6-106">You can capture these events in your code and take the following actions:</span></span>

* <span data-ttu-id="af6f6-107">Запуск приветствия при добавлении бота в команду.</span><span class="sxs-lookup"><span data-stu-id="af6f6-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="af6f6-108">Запуск приветствия при добавлении или удалении нового члена группы.</span><span class="sxs-lookup"><span data-stu-id="af6f6-108">Trigger a welcome message when a new team member is added or removed.</span></span>
* <span data-ttu-id="af6f6-109">Запуск уведомления при запуске, переименовании или удалении канала.</span><span class="sxs-lookup"><span data-stu-id="af6f6-109">Trigger a notification when a channel is created, renamed, or deleted.</span></span>
* <span data-ttu-id="af6f6-110">Когда сообщение бота нравится пользователю.</span><span class="sxs-lookup"><span data-stu-id="af6f6-110">When a bot message is liked by a user.</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="af6f6-111">События обновления беседы</span><span class="sxs-lookup"><span data-stu-id="af6f6-111">Conversation update events</span></span>

<span data-ttu-id="af6f6-112">События обновления беседы можно использовать для предоставления более эффективных уведомлений и более эффективных действий бота.</span><span class="sxs-lookup"><span data-stu-id="af6f6-112">You can use conversation update events to provide better notifications and more effective bot actions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="af6f6-113">Вы можете добавлять новые события в любое время и ваш бот начинает получать их.</span><span class="sxs-lookup"><span data-stu-id="af6f6-113">You can add new events any time and your bot begins to receive them.</span></span>
> * <span data-ttu-id="af6f6-114">Чтобы получить неожиданные события, необходимо разработать бот.</span><span class="sxs-lookup"><span data-stu-id="af6f6-114">You must design your bot to receive unexpected events.</span></span>
> * <span data-ttu-id="af6f6-115">Если вы используете SDK Bot Framework, ваш бот автоматически отвечает на любые события, которые `200 - OK` вы не хотите обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="af6f6-115">If you are using the Bot Framework SDK, your bot automatically responds with a `200 - OK` to any events you choose not to handle.</span></span>

<span data-ttu-id="af6f6-116">Бот получает событие `conversationUpdate` в любом из следующих случаев:</span><span class="sxs-lookup"><span data-stu-id="af6f6-116">A bot receives a `conversationUpdate` event in either of the following cases:</span></span>

* <span data-ttu-id="af6f6-117">При добавлении бота в беседу.</span><span class="sxs-lookup"><span data-stu-id="af6f6-117">When bot has been added to a conversation.</span></span>
* <span data-ttu-id="af6f6-118">Другие участники добавляются или удаляются из беседы.</span><span class="sxs-lookup"><span data-stu-id="af6f6-118">Other members are added to or removed from a conversation.</span></span>
* <span data-ttu-id="af6f6-119">Метаданные беседы изменились.</span><span class="sxs-lookup"><span data-stu-id="af6f6-119">Conversation metadata has changed.</span></span>

<span data-ttu-id="af6f6-120">Событие `conversationUpdate` отправляется боту, когда поступают сведения об обновлении членства в командах, куда он добавлен.</span><span class="sxs-lookup"><span data-stu-id="af6f6-120">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="af6f6-121">Кроме того, он получает обновление при первом добавлении для личных бесед.</span><span class="sxs-lookup"><span data-stu-id="af6f6-121">It also receives an update when it has been added for the first time for personal conversations.</span></span>

<span data-ttu-id="af6f6-122">В следующей таблице показан список событий обновления беседы Teams с дополнительными сведениями:</span><span class="sxs-lookup"><span data-stu-id="af6f6-122">The following table shows a list of Teams conversation update events with more details:</span></span>

| <span data-ttu-id="af6f6-123">Действие, принятое</span><span class="sxs-lookup"><span data-stu-id="af6f6-123">Action taken</span></span>        | <span data-ttu-id="af6f6-124">EventType</span><span class="sxs-lookup"><span data-stu-id="af6f6-124">EventType</span></span>         | <span data-ttu-id="af6f6-125">Метод, называемый</span><span class="sxs-lookup"><span data-stu-id="af6f6-125">Method called</span></span>              | <span data-ttu-id="af6f6-126">Описание</span><span class="sxs-lookup"><span data-stu-id="af6f6-126">Description</span></span>                | <span data-ttu-id="af6f6-127">Область</span><span class="sxs-lookup"><span data-stu-id="af6f6-127">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="af6f6-128">Созданный канал</span><span class="sxs-lookup"><span data-stu-id="af6f6-128">Channel created</span></span>     | <span data-ttu-id="af6f6-129">channelCreated</span><span class="sxs-lookup"><span data-stu-id="af6f6-129">channelCreated</span></span>    | <span data-ttu-id="af6f6-130">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-130">OnTeamsChannelCreatedAsync</span></span> | <span data-ttu-id="af6f6-131">[Создается канал](#channel-created).</span><span class="sxs-lookup"><span data-stu-id="af6f6-131">[A channel is created](#channel-created).</span></span> | <span data-ttu-id="af6f6-132">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-132">Team</span></span> |
| <span data-ttu-id="af6f6-133">Переименован канал</span><span class="sxs-lookup"><span data-stu-id="af6f6-133">Channel renamed</span></span>     | <span data-ttu-id="af6f6-134">ChannelRenamed</span><span class="sxs-lookup"><span data-stu-id="af6f6-134">channelRenamed</span></span>    | <span data-ttu-id="af6f6-135">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-135">OnTeamsChannelRenamedAsync</span></span> | <span data-ttu-id="af6f6-136">[Канал переименован.](#channel-renamed)</span><span class="sxs-lookup"><span data-stu-id="af6f6-136">[A channel is renamed](#channel-renamed).</span></span> | <span data-ttu-id="af6f6-137">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-137">Team</span></span> |
| <span data-ttu-id="af6f6-138">Канал удален</span><span class="sxs-lookup"><span data-stu-id="af6f6-138">Channel deleted</span></span>     | <span data-ttu-id="af6f6-139">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="af6f6-139">channelDeleted</span></span>    | <span data-ttu-id="af6f6-140">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-140">OnTeamsChannelDeletedAsync</span></span> | <span data-ttu-id="af6f6-141">[Канал удаляется.](#channel-deleted)</span><span class="sxs-lookup"><span data-stu-id="af6f6-141">[A channel is deleted](#channel-deleted).</span></span> | <span data-ttu-id="af6f6-142">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-142">Team</span></span> |
| <span data-ttu-id="af6f6-143">Восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="af6f6-143">Channel restored</span></span>    | <span data-ttu-id="af6f6-144">channelRestored</span><span class="sxs-lookup"><span data-stu-id="af6f6-144">channelRestored</span></span>    | <span data-ttu-id="af6f6-145">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-145">OnTeamsChannelRestoredAsync</span></span> | <span data-ttu-id="af6f6-146">[Канал восстанавливается.](#channel-deleted)</span><span class="sxs-lookup"><span data-stu-id="af6f6-146">[A channel is restored](#channel-deleted).</span></span> | <span data-ttu-id="af6f6-147">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-147">Team</span></span> |
| <span data-ttu-id="af6f6-148">Добавлены участники</span><span class="sxs-lookup"><span data-stu-id="af6f6-148">Members added</span></span>   | <span data-ttu-id="af6f6-149">membersAdded</span><span class="sxs-lookup"><span data-stu-id="af6f6-149">membersAdded</span></span>   | <span data-ttu-id="af6f6-150">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-150">OnTeamsMembersAddedAsync</span></span>   | <span data-ttu-id="af6f6-151">[Добавлен член](#team-members-added).</span><span class="sxs-lookup"><span data-stu-id="af6f6-151">[A member is added](#team-members-added).</span></span> | <span data-ttu-id="af6f6-152">Все</span><span class="sxs-lookup"><span data-stu-id="af6f6-152">All</span></span> |
| <span data-ttu-id="af6f6-153">Удалены участники</span><span class="sxs-lookup"><span data-stu-id="af6f6-153">Members removed</span></span> | <span data-ttu-id="af6f6-154">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="af6f6-154">membersRemoved</span></span> | <span data-ttu-id="af6f6-155">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-155">OnTeamsMembersRemovedAsync</span></span> | <span data-ttu-id="af6f6-156">[Член удаляется.](#team-members-removed)</span><span class="sxs-lookup"><span data-stu-id="af6f6-156">[A member is removed](#team-members-removed).</span></span> | <span data-ttu-id="af6f6-157">groupChat и team</span><span class="sxs-lookup"><span data-stu-id="af6f6-157">groupChat and team</span></span> |
| <span data-ttu-id="af6f6-158">Переименована команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-158">Team renamed</span></span>        | <span data-ttu-id="af6f6-159">переименованная команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-159">teamRenamed</span></span>       | <span data-ttu-id="af6f6-160">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-160">OnTeamsTeamRenamedAsync</span></span>    | <span data-ttu-id="af6f6-161">[Команда переименована.](#team-renamed)</span><span class="sxs-lookup"><span data-stu-id="af6f6-161">[A team is renamed](#team-renamed).</span></span>       | <span data-ttu-id="af6f6-162">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-162">Team</span></span> |
| <span data-ttu-id="af6f6-163">Удалена команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-163">Team deleted</span></span>        | <span data-ttu-id="af6f6-164">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="af6f6-164">teamDeleted</span></span>       | <span data-ttu-id="af6f6-165">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-165">OnTeamsTeamDeletedAsync</span></span>    | <span data-ttu-id="af6f6-166">[Команда удалена.](#team-deleted)</span><span class="sxs-lookup"><span data-stu-id="af6f6-166">[A team is deleted](#team-deleted).</span></span>       | <span data-ttu-id="af6f6-167">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-167">Team</span></span> |
| <span data-ttu-id="af6f6-168">Архив команд</span><span class="sxs-lookup"><span data-stu-id="af6f6-168">Team archived</span></span>        | <span data-ttu-id="af6f6-169">teamArchived</span><span class="sxs-lookup"><span data-stu-id="af6f6-169">teamArchived</span></span>       | <span data-ttu-id="af6f6-170">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-170">OnTeamsTeamArchivedAsync</span></span>    | <span data-ttu-id="af6f6-171">[Команда архивна.](#team-archived)</span><span class="sxs-lookup"><span data-stu-id="af6f6-171">[A team is archived](#team-archived).</span></span>       | <span data-ttu-id="af6f6-172">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-172">Team</span></span> |
| <span data-ttu-id="af6f6-173">Команда без анархии</span><span class="sxs-lookup"><span data-stu-id="af6f6-173">Team unarchived</span></span>        | <span data-ttu-id="af6f6-174">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="af6f6-174">teamUnarchived</span></span>       | <span data-ttu-id="af6f6-175">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-175">OnTeamsTeamUnarchivedAsync</span></span>    | <span data-ttu-id="af6f6-176">[Команда не является анархивной.](#team-unarchived)</span><span class="sxs-lookup"><span data-stu-id="af6f6-176">[A team is unarchived](#team-unarchived).</span></span>       | <span data-ttu-id="af6f6-177">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-177">Team</span></span> |
| <span data-ttu-id="af6f6-178">Восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-178">Team restored</span></span>        | <span data-ttu-id="af6f6-179">teamRestored</span><span class="sxs-lookup"><span data-stu-id="af6f6-179">teamRestored</span></span>      | <span data-ttu-id="af6f6-180">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="af6f6-180">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="af6f6-181">Восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-181">A team is restored</span></span>](#team-restored)       | <span data-ttu-id="af6f6-182">Группа</span><span class="sxs-lookup"><span data-stu-id="af6f6-182">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="af6f6-183">Созданный канал</span><span class="sxs-lookup"><span data-stu-id="af6f6-183">Channel created</span></span>

<span data-ttu-id="af6f6-184">Событие, созданное каналом, отправляется вашему боту всякий раз, когда новый канал создается в команде, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="af6f6-184">The channel created event is sent to your bot whenever a new channel is created in a team where your bot is installed.</span></span>

<span data-ttu-id="af6f6-185">В следующем коде показан пример события, созданного каналом:</span><span class="sxs-lookup"><span data-stu-id="af6f6-185">The following code shows an example of channel created event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-186">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-186">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-187">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-187">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-188">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-189">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-189">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="af6f6-190">Переименован канал</span><span class="sxs-lookup"><span data-stu-id="af6f6-190">Channel renamed</span></span>

<span data-ttu-id="af6f6-191">Событие, переименованное в канал, отправляется вашему боту всякий раз, когда канал переименован в команде, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="af6f6-191">The channel renamed event is sent to your bot whenever a channel is renamed in a team where your bot is installed.</span></span>

<span data-ttu-id="af6f6-192">В следующем коде показан пример события переименования канала:</span><span class="sxs-lookup"><span data-stu-id="af6f6-192">The following code shows an example of channel renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-193">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-194">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-195">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-195">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-196">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-196">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="af6f6-197">Канал удален</span><span class="sxs-lookup"><span data-stu-id="af6f6-197">Channel deleted</span></span>

<span data-ttu-id="af6f6-198">Событие удаления канала отправляется вашему боту всякий раз, когда канал удаляется в команде, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="af6f6-198">The channel deleted event is sent to your bot whenever a channel is deleted in a team where your bot is installed.</span></span>

<span data-ttu-id="af6f6-199">В следующем коде показан пример события удаления канала:</span><span class="sxs-lookup"><span data-stu-id="af6f6-199">The following code shows an example of channel deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-200">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-200">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-201">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-201">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-202">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-202">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-203">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-203">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="af6f6-204">Восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="af6f6-204">Channel restored</span></span>

<span data-ttu-id="af6f6-205">Восстановленное событие канала отправляется в бот всякий раз, когда удаленный ранее канал восстанавливается в команде, где уже установлен бот.</span><span class="sxs-lookup"><span data-stu-id="af6f6-205">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team where your bot is already installed.</span></span>

<span data-ttu-id="af6f6-206">В следующем коде показан пример события восстановления канала:</span><span class="sxs-lookup"><span data-stu-id="af6f6-206">The following code shows an example of channel restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-207">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-207">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-208">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-208">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-209">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-209">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-210">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-210">Python</span></span>](#tab/python)

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

### <a name="team-members-added"></a><span data-ttu-id="af6f6-211">Добавлены участники группы</span><span class="sxs-lookup"><span data-stu-id="af6f6-211">Team members added</span></span>

<span data-ttu-id="af6f6-212">Событие отправляется боту при первом добавлении в `teamMemberAdded` беседу.</span><span class="sxs-lookup"><span data-stu-id="af6f6-212">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation.</span></span> <span data-ttu-id="af6f6-213">Событие отправляется боту каждый раз, когда новый пользователь добавляется в командный или групповой чат, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="af6f6-213">The event is sent to your bot every time a new user is added to a team or group chat where your bot is installed.</span></span> <span data-ttu-id="af6f6-214">ID пользователя является уникальным для вашего бота и может быть кэшировали для дальнейшего использования службой, например отправки сообщения конкретному пользователю.</span><span class="sxs-lookup"><span data-stu-id="af6f6-214">The user information that is ID is unique for your bot and can be cached for future use by your service, such as sending a message to a specific user.</span></span>

<span data-ttu-id="af6f6-215">В следующем коде показан пример добавленного события участников группы:</span><span class="sxs-lookup"><span data-stu-id="af6f6-215">The following code shows an example of team members added event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-216">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-216">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="af6f6-217">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-217">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-218">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-218">JSON</span></span>](#tab/json)

<span data-ttu-id="af6f6-219">Это сообщение, которое получает бот при добавлении бота в команду.</span><span class="sxs-lookup"><span data-stu-id="af6f6-219">This is the message your bot receives when the bot is added to a team.</span></span>

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

<span data-ttu-id="af6f6-220">Это сообщение, которое получает бот при добавлении бота в один чат.</span><span class="sxs-lookup"><span data-stu-id="af6f6-220">This is the message your bot receives when the bot is added to a one-to-one chat.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="af6f6-221">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-221">Python</span></span>](#tab/python)

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

### <a name="team-members-removed"></a><span data-ttu-id="af6f6-222">Удалены члены группы</span><span class="sxs-lookup"><span data-stu-id="af6f6-222">Team members removed</span></span>

<span data-ttu-id="af6f6-223">Событие `teamMemberRemoved` отправляется боту, если оно удалено из группы.</span><span class="sxs-lookup"><span data-stu-id="af6f6-223">The `teamMemberRemoved` event is sent to your bot if it is removed from a team.</span></span> <span data-ttu-id="af6f6-224">Событие отправляется боту каждый раз, когда любой пользователь удаляется из команды, в которой ваш бот является участником.</span><span class="sxs-lookup"><span data-stu-id="af6f6-224">The event is sent to your bot every time any user is removed from a team where your bot is a member.</span></span> <span data-ttu-id="af6f6-225">Чтобы определить, был ли удален новый участник самим ботом или пользователем, проверьте `Activity` объект `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="af6f6-225">To determine if the new member removed was the bot itself or a user, check the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="af6f6-226">Если поле объекта такое же, как и поле объекта, то удаляемого члена является бот, иначе `Id` `MembersRemoved` это `Id` `Recipient` пользователь.</span><span class="sxs-lookup"><span data-stu-id="af6f6-226">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, else it is a user.</span></span> <span data-ttu-id="af6f6-227">Бот, как `Id` правило, `28:<MicrosoftAppId>` является .</span><span class="sxs-lookup"><span data-stu-id="af6f6-227">The bot's `Id` generally is `28:<MicrosoftAppId>`.</span></span>

> [!NOTE]
> <span data-ttu-id="af6f6-228">При постоянном удалении пользователя из клиента `membersRemoved conversationUpdate` запускается событие.</span><span class="sxs-lookup"><span data-stu-id="af6f6-228">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

<span data-ttu-id="af6f6-229">В следующем коде показан пример удаления события участниками группы:</span><span class="sxs-lookup"><span data-stu-id="af6f6-229">The following code shows an example of team members removed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-230">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-230">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="af6f6-231">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-231">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-232">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-232">JSON</span></span>](#tab/json)

<span data-ttu-id="af6f6-233">Объект в следующем примере полезной нагрузки основан на добавлении члена в команду, а не групповом чате или инициировании нового беседы один `channelData` к одному:</span><span class="sxs-lookup"><span data-stu-id="af6f6-233">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="af6f6-234">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-234">Python</span></span>](#tab/python)

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

### <a name="team-renamed"></a><span data-ttu-id="af6f6-235">Переименована команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-235">Team renamed</span></span>

<span data-ttu-id="af6f6-236">Ваш бот уведомлен о переименовании команды, в которая он находится.</span><span class="sxs-lookup"><span data-stu-id="af6f6-236">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="af6f6-237">Он получает событие `conversationUpdate` в `eventType.teamRenamed` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="af6f6-237">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

<span data-ttu-id="af6f6-238">В следующем коде показан пример переименования события в команду:</span><span class="sxs-lookup"><span data-stu-id="af6f6-238">The following code shows an example of team renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-239">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-239">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-240">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-240">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-241">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-242">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="af6f6-243">Удалена команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-243">Team deleted</span></span>

<span data-ttu-id="af6f6-244">Ваш бот уведомлен об удалении команды.</span><span class="sxs-lookup"><span data-stu-id="af6f6-244">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="af6f6-245">Он получает событие `conversationUpdate` в `eventType.teamDeleted` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="af6f6-245">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

<span data-ttu-id="af6f6-246">В следующем коде показан пример события, удаляемого командой:</span><span class="sxs-lookup"><span data-stu-id="af6f6-246">The following code shows an example of team deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-247">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-247">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-248">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-248">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-249">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-249">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-250">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="af6f6-251">Восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="af6f6-251">Team restored</span></span>

<span data-ttu-id="af6f6-252">Бот получает уведомление о восстановлении команды после удаления.</span><span class="sxs-lookup"><span data-stu-id="af6f6-252">The bot receives a notification when a team is restored after being deleted.</span></span> <span data-ttu-id="af6f6-253">Он получает событие `conversationUpdate` в `eventType.teamrestored` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="af6f6-253">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

<span data-ttu-id="af6f6-254">В следующем коде показан пример восстановленного события группы:</span><span class="sxs-lookup"><span data-stu-id="af6f6-254">The following code shows an example of team restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-255">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-255">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-256">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-256">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-257">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-257">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-258">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-258">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="af6f6-259">Архив команд</span><span class="sxs-lookup"><span data-stu-id="af6f6-259">Team archived</span></span>

<span data-ttu-id="af6f6-260">Бот получает уведомление, когда установленная в нем команда будет архивироваться.</span><span class="sxs-lookup"><span data-stu-id="af6f6-260">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="af6f6-261">Он получает событие `conversationUpdate` в `eventType.teamarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="af6f6-261">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

<span data-ttu-id="af6f6-262">В следующем коде показан пример события архива группы:</span><span class="sxs-lookup"><span data-stu-id="af6f6-262">The following code shows an example of team archived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-263">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-263">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-264">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-264">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-265">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-265">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-266">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-266">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="af6f6-267">Команда без анархии</span><span class="sxs-lookup"><span data-stu-id="af6f6-267">Team unarchived</span></span>

<span data-ttu-id="af6f6-268">Бот получает уведомление, когда установленная в нем команда не является анархивной.</span><span class="sxs-lookup"><span data-stu-id="af6f6-268">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="af6f6-269">Он получает событие `conversationUpdate` в `eventType.teamUnarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="af6f6-269">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

<span data-ttu-id="af6f6-270">В следующем коде показан пример события, неархивного для группы:</span><span class="sxs-lookup"><span data-stu-id="af6f6-270">The following code shows an example of team unarchived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-271">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-271">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="af6f6-272">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-272">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-273">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-273">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-274">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-274">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

<span data-ttu-id="af6f6-275">Теперь, когда вы работали с событиями обновления беседы, вы можете понять события реакции на сообщения, которые происходят для различных реакций на сообщение.</span><span class="sxs-lookup"><span data-stu-id="af6f6-275">Now that you have worked with the conversation update events, you can understand the message reaction events that occur for different reactions to a message.</span></span>

## <a name="message-reaction-events"></a><span data-ttu-id="af6f6-276">События реакции на сообщения</span><span class="sxs-lookup"><span data-stu-id="af6f6-276">Message reaction events</span></span>

<span data-ttu-id="af6f6-277">Событие отправляется, когда пользователь добавляет или удаляет отклики на `messageReaction` сообщение, отправленное ботом.</span><span class="sxs-lookup"><span data-stu-id="af6f6-277">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="af6f6-278">Документ содержит ID сообщения и является типом реакции `replyToId` `Type` в текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="af6f6-278">The `replyToId` contains the ID of the message, and the `Type` is the type of reaction in text format.</span></span> <span data-ttu-id="af6f6-279">Типы реакций включают гнев, сердце, смех, как, грустно, и удивлен.</span><span class="sxs-lookup"><span data-stu-id="af6f6-279">The types of reactions include angry, heart, laugh, like, sad, and surprised.</span></span> <span data-ttu-id="af6f6-280">Это событие не содержит содержимое исходного сообщения.</span><span class="sxs-lookup"><span data-stu-id="af6f6-280">This event does not contain the contents of the original message.</span></span> <span data-ttu-id="af6f6-281">Если обработка реакций на сообщения важна для вашего бота, необходимо хранить сообщения при их отправке.</span><span class="sxs-lookup"><span data-stu-id="af6f6-281">If processing reactions to your messages is important for your bot, you must store the messages when you send them.</span></span> <span data-ttu-id="af6f6-282">В следующей таблице приводится больше сведений о типе события и объектах полезной нагрузки:</span><span class="sxs-lookup"><span data-stu-id="af6f6-282">The following table provides more information about the event type and payload objects:</span></span>

| <span data-ttu-id="af6f6-283">EventType</span><span class="sxs-lookup"><span data-stu-id="af6f6-283">EventType</span></span>       | <span data-ttu-id="af6f6-284">Объект полезной нагрузки</span><span class="sxs-lookup"><span data-stu-id="af6f6-284">Payload object</span></span>   | <span data-ttu-id="af6f6-285">Описание</span><span class="sxs-lookup"><span data-stu-id="af6f6-285">Description</span></span>                                                             | <span data-ttu-id="af6f6-286">Область</span><span class="sxs-lookup"><span data-stu-id="af6f6-286">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="af6f6-287">messageReaction</span><span class="sxs-lookup"><span data-stu-id="af6f6-287">messageReaction</span></span> | <span data-ttu-id="af6f6-288">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="af6f6-288">reactionsAdded</span></span>   | [<span data-ttu-id="af6f6-289">Реакция на сообщение бота</span><span class="sxs-lookup"><span data-stu-id="af6f6-289">Reactions to a bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="af6f6-290">Все</span><span class="sxs-lookup"><span data-stu-id="af6f6-290">All</span></span>   |
| <span data-ttu-id="af6f6-291">messageReaction</span><span class="sxs-lookup"><span data-stu-id="af6f6-291">messageReaction</span></span> | <span data-ttu-id="af6f6-292">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="af6f6-292">reactionsRemoved</span></span> | [<span data-ttu-id="af6f6-293">Реакции, удаленые из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="af6f6-293">Reactions removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="af6f6-294">Все</span><span class="sxs-lookup"><span data-stu-id="af6f6-294">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="af6f6-295">Реакция на сообщение бота</span><span class="sxs-lookup"><span data-stu-id="af6f6-295">Reactions to a bot message</span></span>

<span data-ttu-id="af6f6-296">В следующем коде показан пример реакций на сообщение бота:</span><span class="sxs-lookup"><span data-stu-id="af6f6-296">The following code shows an example of reactions to a bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-297">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-297">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="af6f6-298">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-298">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-299">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-299">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-300">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-300">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="af6f6-301">Реакции, удаленые из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="af6f6-301">Reactions removed from bot message</span></span>

<span data-ttu-id="af6f6-302">В следующем коде показан пример реакций, удаленых из сообщения бота:</span><span class="sxs-lookup"><span data-stu-id="af6f6-302">The following code shows an example of reactions removed from bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="af6f6-303">C#</span><span class="sxs-lookup"><span data-stu-id="af6f6-303">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="af6f6-304">TypeScript</span><span class="sxs-lookup"><span data-stu-id="af6f6-304">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="af6f6-305">JSON</span><span class="sxs-lookup"><span data-stu-id="af6f6-305">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="af6f6-306">Python</span><span class="sxs-lookup"><span data-stu-id="af6f6-306">Python</span></span>](#tab/python)

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

## <a name="code-sample"></a><span data-ttu-id="af6f6-307">Пример кода</span><span class="sxs-lookup"><span data-stu-id="af6f6-307">Code sample</span></span>

<span data-ttu-id="af6f6-308">В следующей таблице приводится простой пример кода, который включает события беседы ботов в приложение Teams:</span><span class="sxs-lookup"><span data-stu-id="af6f6-308">The following table provides a simple code sample that incorporates bots conversation events into a Teams application:</span></span>

| <span data-ttu-id="af6f6-309">Пример</span><span class="sxs-lookup"><span data-stu-id="af6f6-309">Sample</span></span> | <span data-ttu-id="af6f6-310">Описание</span><span class="sxs-lookup"><span data-stu-id="af6f6-310">Description</span></span> | <span data-ttu-id="af6f6-311">.NET Core</span><span class="sxs-lookup"><span data-stu-id="af6f6-311">.NET Core</span></span> |
|--------|------------- |---|
| <span data-ttu-id="af6f6-312">Teams bots conversation events sample</span><span class="sxs-lookup"><span data-stu-id="af6f6-312">Teams bots conversation events sample</span></span> | <span data-ttu-id="af6f6-313">Образец бот-бота bot Framework v4 для teams.</span><span class="sxs-lookup"><span data-stu-id="af6f6-313">Bot Framework v4 conversation bot sample for Teams.</span></span> | [<span data-ttu-id="af6f6-314">View</span><span class="sxs-lookup"><span data-stu-id="af6f6-314">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|

## <a name="next-step"></a><span data-ttu-id="af6f6-315">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="af6f6-315">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="af6f6-316">Отправлять активные сообщения</span><span class="sxs-lookup"><span data-stu-id="af6f6-316">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
