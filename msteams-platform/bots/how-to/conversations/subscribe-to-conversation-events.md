---
title: События беседы
author: WashingtonKayaker
description: Работа с событиями беседы из Microsoft Teams бота.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 7dfafbd02c53ea0fe7393d4e4f771a50ad2954d2
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630707"
---
# <a name="conversation-events-in-your-teams-bot"></a><span data-ttu-id="1c4ef-103">События бесед в вашем боте Teams</span><span class="sxs-lookup"><span data-stu-id="1c4ef-103">Conversation events in your Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="1c4ef-104">При создании разговорных ботов для Microsoft Teams можно работать с событиями беседы.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-104">When building your conversational bots for Microsoft Teams, you can work with conversation events.</span></span> <span data-ttu-id="1c4ef-105">Teams отправляет уведомления боту для событий беседы, которые происходят в сферах, где ваш бот активен.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-105">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="1c4ef-106">Эти события можно зафиксировать в коде и принять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-106">You can capture these events in your code and take the following actions:</span></span>

* <span data-ttu-id="1c4ef-107">Запуск приветствия при добавлении бота в команду.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="1c4ef-108">Запуск приветствия при добавлении или удалении нового члена группы.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-108">Trigger a welcome message when a new team member is added or removed.</span></span>
* <span data-ttu-id="1c4ef-109">Запуск уведомления при запуске, переименовании или удалении канала.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-109">Trigger a notification when a channel is created, renamed, or deleted.</span></span>
* <span data-ttu-id="1c4ef-110">Когда сообщение бота нравится пользователю.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-110">When a bot message is liked by a user.</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="1c4ef-111">События обновления беседы</span><span class="sxs-lookup"><span data-stu-id="1c4ef-111">Conversation update events</span></span>

<span data-ttu-id="1c4ef-112">События обновления беседы можно использовать для предоставления более эффективных уведомлений и более эффективных действий бота.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-112">You can use conversation update events to provide better notifications and more effective bot actions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1c4ef-113">Вы можете добавлять новые события в любое время и ваш бот начинает получать их.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-113">You can add new events any time and your bot begins to receive them.</span></span>
> * <span data-ttu-id="1c4ef-114">Чтобы получить неожиданные события, необходимо разработать бот.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-114">You must design your bot to receive unexpected events.</span></span>
> * <span data-ttu-id="1c4ef-115">Если вы используете SDK Bot Framework, ваш бот автоматически отвечает на любые события, которые `200 - OK` вы не хотите обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-115">If you are using the Bot Framework SDK, your bot automatically responds with a `200 - OK` to any events you choose not to handle.</span></span>

<span data-ttu-id="1c4ef-116">Бот получает событие `conversationUpdate` в любом из следующих случаев:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-116">A bot receives a `conversationUpdate` event in either of the following cases:</span></span>

* <span data-ttu-id="1c4ef-117">При добавлении бота в беседу.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-117">When bot has been added to a conversation.</span></span>
* <span data-ttu-id="1c4ef-118">Другие участники добавляются или удаляются из беседы.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-118">Other members are added to or removed from a conversation.</span></span>
* <span data-ttu-id="1c4ef-119">Метаданные беседы изменились.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-119">Conversation metadata has changed.</span></span>

<span data-ttu-id="1c4ef-120">Событие `conversationUpdate` отправляется боту, когда поступают сведения об обновлении членства в командах, куда он добавлен.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-120">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="1c4ef-121">Кроме того, он получает обновление при первом добавлении для личных бесед.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-121">It also receives an update when it has been added for the first time for personal conversations.</span></span>

<span data-ttu-id="1c4ef-122">В следующей таблице показан список событий обновления Teams беседы с дополнительными сведениями:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-122">The following table shows a list of Teams conversation update events with more details:</span></span>

| <span data-ttu-id="1c4ef-123">Действие, принятое</span><span class="sxs-lookup"><span data-stu-id="1c4ef-123">Action taken</span></span>        | <span data-ttu-id="1c4ef-124">EventType</span><span class="sxs-lookup"><span data-stu-id="1c4ef-124">EventType</span></span>         | <span data-ttu-id="1c4ef-125">Метод, называемый</span><span class="sxs-lookup"><span data-stu-id="1c4ef-125">Method called</span></span>              | <span data-ttu-id="1c4ef-126">Описание</span><span class="sxs-lookup"><span data-stu-id="1c4ef-126">Description</span></span>                | <span data-ttu-id="1c4ef-127">Область</span><span class="sxs-lookup"><span data-stu-id="1c4ef-127">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="1c4ef-128">Созданный канал</span><span class="sxs-lookup"><span data-stu-id="1c4ef-128">Channel created</span></span>     | <span data-ttu-id="1c4ef-129">channelCreated</span><span class="sxs-lookup"><span data-stu-id="1c4ef-129">channelCreated</span></span>    | <span data-ttu-id="1c4ef-130">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-130">OnTeamsChannelCreatedAsync</span></span> | <span data-ttu-id="1c4ef-131">[Создается канал](#channel-created).</span><span class="sxs-lookup"><span data-stu-id="1c4ef-131">[A channel is created](#channel-created).</span></span> | <span data-ttu-id="1c4ef-132">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-132">Team</span></span> |
| <span data-ttu-id="1c4ef-133">Переименован канал</span><span class="sxs-lookup"><span data-stu-id="1c4ef-133">Channel renamed</span></span>     | <span data-ttu-id="1c4ef-134">ChannelRenamed</span><span class="sxs-lookup"><span data-stu-id="1c4ef-134">channelRenamed</span></span>    | <span data-ttu-id="1c4ef-135">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-135">OnTeamsChannelRenamedAsync</span></span> | <span data-ttu-id="1c4ef-136">[Канал переименован.](#channel-renamed)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-136">[A channel is renamed](#channel-renamed).</span></span> | <span data-ttu-id="1c4ef-137">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-137">Team</span></span> |
| <span data-ttu-id="1c4ef-138">Канал удален</span><span class="sxs-lookup"><span data-stu-id="1c4ef-138">Channel deleted</span></span>     | <span data-ttu-id="1c4ef-139">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="1c4ef-139">channelDeleted</span></span>    | <span data-ttu-id="1c4ef-140">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-140">OnTeamsChannelDeletedAsync</span></span> | <span data-ttu-id="1c4ef-141">[Канал удаляется.](#channel-deleted)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-141">[A channel is deleted](#channel-deleted).</span></span> | <span data-ttu-id="1c4ef-142">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-142">Team</span></span> |
| <span data-ttu-id="1c4ef-143">Восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="1c4ef-143">Channel restored</span></span>    | <span data-ttu-id="1c4ef-144">channelRestored</span><span class="sxs-lookup"><span data-stu-id="1c4ef-144">channelRestored</span></span>    | <span data-ttu-id="1c4ef-145">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-145">OnTeamsChannelRestoredAsync</span></span> | <span data-ttu-id="1c4ef-146">[Канал восстанавливается.](#channel-deleted)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-146">[A channel is restored](#channel-deleted).</span></span> | <span data-ttu-id="1c4ef-147">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-147">Team</span></span> |
| <span data-ttu-id="1c4ef-148">Добавлены участники</span><span class="sxs-lookup"><span data-stu-id="1c4ef-148">Members added</span></span>   | <span data-ttu-id="1c4ef-149">membersAdded</span><span class="sxs-lookup"><span data-stu-id="1c4ef-149">membersAdded</span></span>   | <span data-ttu-id="1c4ef-150">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-150">OnTeamsMembersAddedAsync</span></span>   | <span data-ttu-id="1c4ef-151">[Добавлен член](#team-members-added).</span><span class="sxs-lookup"><span data-stu-id="1c4ef-151">[A member is added](#team-members-added).</span></span> | <span data-ttu-id="1c4ef-152">Все</span><span class="sxs-lookup"><span data-stu-id="1c4ef-152">All</span></span> |
| <span data-ttu-id="1c4ef-153">Удалены участники</span><span class="sxs-lookup"><span data-stu-id="1c4ef-153">Members removed</span></span> | <span data-ttu-id="1c4ef-154">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="1c4ef-154">membersRemoved</span></span> | <span data-ttu-id="1c4ef-155">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-155">OnTeamsMembersRemovedAsync</span></span> | <span data-ttu-id="1c4ef-156">[Член удаляется.](#team-members-removed)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-156">[A member is removed](#team-members-removed).</span></span> | <span data-ttu-id="1c4ef-157">groupChat и team</span><span class="sxs-lookup"><span data-stu-id="1c4ef-157">groupChat and team</span></span> |
| <span data-ttu-id="1c4ef-158">Переименована команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-158">Team renamed</span></span>        | <span data-ttu-id="1c4ef-159">переименованная команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-159">teamRenamed</span></span>       | <span data-ttu-id="1c4ef-160">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-160">OnTeamsTeamRenamedAsync</span></span>    | <span data-ttu-id="1c4ef-161">[Команда переименована.](#team-renamed)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-161">[A team is renamed](#team-renamed).</span></span>       | <span data-ttu-id="1c4ef-162">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-162">Team</span></span> |
| <span data-ttu-id="1c4ef-163">Удалена команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-163">Team deleted</span></span>        | <span data-ttu-id="1c4ef-164">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="1c4ef-164">teamDeleted</span></span>       | <span data-ttu-id="1c4ef-165">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-165">OnTeamsTeamDeletedAsync</span></span>    | <span data-ttu-id="1c4ef-166">[Команда удалена.](#team-deleted)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-166">[A team is deleted](#team-deleted).</span></span>       | <span data-ttu-id="1c4ef-167">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-167">Team</span></span> |
| <span data-ttu-id="1c4ef-168">Архив команд</span><span class="sxs-lookup"><span data-stu-id="1c4ef-168">Team archived</span></span>        | <span data-ttu-id="1c4ef-169">teamArchived</span><span class="sxs-lookup"><span data-stu-id="1c4ef-169">teamArchived</span></span>       | <span data-ttu-id="1c4ef-170">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-170">OnTeamsTeamArchivedAsync</span></span>    | <span data-ttu-id="1c4ef-171">[Команда архивна.](#team-archived)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-171">[A team is archived](#team-archived).</span></span>       | <span data-ttu-id="1c4ef-172">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-172">Team</span></span> |
| <span data-ttu-id="1c4ef-173">Команда без анархии</span><span class="sxs-lookup"><span data-stu-id="1c4ef-173">Team unarchived</span></span>        | <span data-ttu-id="1c4ef-174">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="1c4ef-174">teamUnarchived</span></span>       | <span data-ttu-id="1c4ef-175">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-175">OnTeamsTeamUnarchivedAsync</span></span>    | <span data-ttu-id="1c4ef-176">[Команда не является анархивной.](#team-unarchived)</span><span class="sxs-lookup"><span data-stu-id="1c4ef-176">[A team is unarchived](#team-unarchived).</span></span>       | <span data-ttu-id="1c4ef-177">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-177">Team</span></span> |
| <span data-ttu-id="1c4ef-178">Восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-178">Team restored</span></span>        | <span data-ttu-id="1c4ef-179">teamRestored</span><span class="sxs-lookup"><span data-stu-id="1c4ef-179">teamRestored</span></span>      | <span data-ttu-id="1c4ef-180">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="1c4ef-180">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="1c4ef-181">Восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-181">A team is restored</span></span>](#team-restored)       | <span data-ttu-id="1c4ef-182">Команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-182">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="1c4ef-183">Созданный канал</span><span class="sxs-lookup"><span data-stu-id="1c4ef-183">Channel created</span></span>

<span data-ttu-id="1c4ef-184">Событие, созданное каналом, отправляется вашему боту всякий раз, когда новый канал создается в команде, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-184">The channel created event is sent to your bot whenever a new channel is created in a team where your bot is installed.</span></span>

<span data-ttu-id="1c4ef-185">В следующем коде показан пример события, созданного каналом:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-185">The following code shows an example of channel created event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-186">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-186">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-187">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-187">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-188">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-189">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-189">Python</span></span>](#tab/python)

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

---

### <a name="channel-renamed"></a><span data-ttu-id="1c4ef-190">Переименован канал</span><span class="sxs-lookup"><span data-stu-id="1c4ef-190">Channel renamed</span></span>

<span data-ttu-id="1c4ef-191">Событие, переименованное в канал, отправляется вашему боту всякий раз, когда канал переименован в команде, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-191">The channel renamed event is sent to your bot whenever a channel is renamed in a team where your bot is installed.</span></span>

<span data-ttu-id="1c4ef-192">В следующем коде показан пример события переименования канала:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-192">The following code shows an example of channel renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-193">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-194">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-195">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-195">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-196">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-196">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

---

### <a name="channel-deleted"></a><span data-ttu-id="1c4ef-197">Канал удален</span><span class="sxs-lookup"><span data-stu-id="1c4ef-197">Channel deleted</span></span>

<span data-ttu-id="1c4ef-198">Событие удаления канала отправляется вашему боту всякий раз, когда канал удаляется в команде, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-198">The channel deleted event is sent to your bot whenever a channel is deleted in a team where your bot is installed.</span></span>

<span data-ttu-id="1c4ef-199">В следующем коде показан пример события удаления канала:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-199">The following code shows an example of channel deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-200">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-200">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-201">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-201">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-202">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-202">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-203">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-203">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

---

### <a name="channel-restored"></a><span data-ttu-id="1c4ef-204">Восстановлен канал</span><span class="sxs-lookup"><span data-stu-id="1c4ef-204">Channel restored</span></span>

<span data-ttu-id="1c4ef-205">Восстановленное событие канала отправляется в бот всякий раз, когда удаленный ранее канал восстанавливается в команде, где уже установлен бот.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-205">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team where your bot is already installed.</span></span>

<span data-ttu-id="1c4ef-206">В следующем коде показан пример события восстановления канала:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-206">The following code shows an example of channel restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-207">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-207">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-208">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-208">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-209">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-209">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-210">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-210">Python</span></span>](#tab/python)

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

---

### <a name="team-members-added"></a><span data-ttu-id="1c4ef-211">Добавлены участники группы</span><span class="sxs-lookup"><span data-stu-id="1c4ef-211">Team members added</span></span>

<span data-ttu-id="1c4ef-212">Событие отправляется боту при первом добавлении в `teamMemberAdded` беседу.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-212">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation.</span></span> <span data-ttu-id="1c4ef-213">Событие отправляется боту каждый раз, когда новый пользователь добавляется в командный или групповой чат, где установлен бот.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-213">The event is sent to your bot every time a new user is added to a team or group chat where your bot is installed.</span></span> <span data-ttu-id="1c4ef-214">ID пользователя является уникальным для вашего бота и может быть кэшировали для дальнейшего использования службой, например отправки сообщения конкретному пользователю.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-214">The user information that is ID is unique for your bot and can be cached for future use by your service, such as sending a message to a specific user.</span></span>

<span data-ttu-id="1c4ef-215">В следующем коде показан пример добавленного события участников группы:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-215">The following code shows an example of team members added event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-216">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-216">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-217">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-217">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-218">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-218">JSON</span></span>](#tab/json)

<span data-ttu-id="1c4ef-219">Это сообщение, которое получает бот при добавлении бота в команду.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-219">This is the message your bot receives when the bot is added to a team.</span></span>

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

<span data-ttu-id="1c4ef-220">Это сообщение, которое получает бот при добавлении бота в один чат.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-220">This is the message your bot receives when the bot is added to a one-to-one chat.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-221">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-221">Python</span></span>](#tab/python)

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

---

### <a name="team-members-removed"></a><span data-ttu-id="1c4ef-222">Удалены члены группы</span><span class="sxs-lookup"><span data-stu-id="1c4ef-222">Team members removed</span></span>

<span data-ttu-id="1c4ef-223">Событие `teamMemberRemoved` отправляется боту, если оно удалено из группы.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-223">The `teamMemberRemoved` event is sent to your bot if it is removed from a team.</span></span> <span data-ttu-id="1c4ef-224">Событие отправляется боту каждый раз, когда любой пользователь удаляется из команды, в которой ваш бот является участником.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-224">The event is sent to your bot every time any user is removed from a team where your bot is a member.</span></span> <span data-ttu-id="1c4ef-225">Чтобы определить, был ли удален новый участник самим ботом или пользователем, проверьте `Activity` объект `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="1c4ef-225">To determine if the new member removed was the bot itself or a user, check the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="1c4ef-226">Если поле объекта такое же, как и поле объекта, то удаляемого члена является бот, иначе `Id` `MembersRemoved` это `Id` `Recipient` пользователь.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-226">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, else it is a user.</span></span> <span data-ttu-id="1c4ef-227">Бот, как `Id` правило, `28:<MicrosoftAppId>` является .</span><span class="sxs-lookup"><span data-stu-id="1c4ef-227">The bot's `Id` generally is `28:<MicrosoftAppId>`.</span></span>

> [!NOTE]
> <span data-ttu-id="1c4ef-228">При постоянном удалении пользователя из клиента `membersRemoved conversationUpdate` запускается событие.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-228">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

<span data-ttu-id="1c4ef-229">В следующем коде показан пример удаления события участниками группы:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-229">The following code shows an example of team members removed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-230">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-230">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-231">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-231">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-232">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-232">JSON</span></span>](#tab/json)

<span data-ttu-id="1c4ef-233">Объект в следующем примере полезной нагрузки основан на добавлении члена в команду, а не групповом чате или инициировании нового беседы один `channelData` к одному:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-233">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="1c4ef-234">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-234">Python</span></span>](#tab/python)

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

---

### <a name="team-renamed"></a><span data-ttu-id="1c4ef-235">Переименована команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-235">Team renamed</span></span>

<span data-ttu-id="1c4ef-236">Ваш бот уведомлен о переименовании команды, в которая он находится.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-236">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="1c4ef-237">Он получает событие `conversationUpdate` в `eventType.teamRenamed` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-237">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

<span data-ttu-id="1c4ef-238">В следующем коде показан пример переименования события в команду:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-238">The following code shows an example of team renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-239">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-239">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-240">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-240">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-241">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-242">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

---

### <a name="team-deleted"></a><span data-ttu-id="1c4ef-243">Удалена команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-243">Team deleted</span></span>

<span data-ttu-id="1c4ef-244">Ваш бот уведомлен об удалении команды.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-244">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="1c4ef-245">Он получает событие `conversationUpdate` в `eventType.teamDeleted` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-245">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

<span data-ttu-id="1c4ef-246">В следующем коде показан пример события, удаляемого командой:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-246">The following code shows an example of team deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-247">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-247">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-248">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-248">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-249">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-249">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-250">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

---

### <a name="team-restored"></a><span data-ttu-id="1c4ef-251">Восстановлена команда</span><span class="sxs-lookup"><span data-stu-id="1c4ef-251">Team restored</span></span>

<span data-ttu-id="1c4ef-252">Бот получает уведомление о восстановлении команды после удаления.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-252">The bot receives a notification when a team is restored after being deleted.</span></span> <span data-ttu-id="1c4ef-253">Он получает событие `conversationUpdate` в `eventType.teamrestored` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-253">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

<span data-ttu-id="1c4ef-254">В следующем коде показан пример восстановленного события группы:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-254">The following code shows an example of team restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-255">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-255">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-256">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-256">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-257">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-257">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-258">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-258">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---

### <a name="team-archived"></a><span data-ttu-id="1c4ef-259">Архив команд</span><span class="sxs-lookup"><span data-stu-id="1c4ef-259">Team archived</span></span>

<span data-ttu-id="1c4ef-260">Бот получает уведомление, когда установленная в нем команда будет архивироваться.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-260">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="1c4ef-261">Он получает событие `conversationUpdate` в `eventType.teamarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-261">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

<span data-ttu-id="1c4ef-262">В следующем коде показан пример события архива группы:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-262">The following code shows an example of team archived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-263">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-263">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-264">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-264">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-265">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-265">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-266">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-266">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---


### <a name="team-unarchived"></a><span data-ttu-id="1c4ef-267">Команда без анархии</span><span class="sxs-lookup"><span data-stu-id="1c4ef-267">Team unarchived</span></span>

<span data-ttu-id="1c4ef-268">Бот получает уведомление, когда установленная в нем команда не является анархивной.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-268">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="1c4ef-269">Он получает событие `conversationUpdate` в `eventType.teamUnarchived` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-269">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

<span data-ttu-id="1c4ef-270">В следующем коде показан пример события, неархивного для группы:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-270">The following code shows an example of team unarchived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-271">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-271">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-272">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-272">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-273">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-273">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-274">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-274">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---

<span data-ttu-id="1c4ef-275">Теперь, когда вы работали с событиями обновления беседы, вы можете понять события реакции на сообщения, которые происходят для различных реакций на сообщение.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-275">Now that you have worked with the conversation update events, you can understand the message reaction events that occur for different reactions to a message.</span></span>

## <a name="message-reaction-events"></a><span data-ttu-id="1c4ef-276">События реакции на сообщения</span><span class="sxs-lookup"><span data-stu-id="1c4ef-276">Message reaction events</span></span>

<span data-ttu-id="1c4ef-277">Событие отправляется, когда пользователь добавляет или удаляет отклики на `messageReaction` сообщение, отправленное ботом.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-277">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="1c4ef-278">Документ содержит ID сообщения и является типом реакции `replyToId` `Type` в текстовом формате.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-278">The `replyToId` contains the ID of the message, and the `Type` is the type of reaction in text format.</span></span> <span data-ttu-id="1c4ef-279">Типы реакций включают гнев, сердце, смех, как, грустно, и удивлен.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-279">The types of reactions include angry, heart, laugh, like, sad, and surprised.</span></span> <span data-ttu-id="1c4ef-280">Это событие не содержит содержимое исходного сообщения.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-280">This event does not contain the contents of the original message.</span></span> <span data-ttu-id="1c4ef-281">Если обработка реакций на сообщения важна для вашего бота, необходимо хранить сообщения при их отправке.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-281">If processing reactions to your messages is important for your bot, you must store the messages when you send them.</span></span> <span data-ttu-id="1c4ef-282">В следующей таблице приводится больше сведений о типе события и объектах полезной нагрузки:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-282">The following table provides more information about the event type and payload objects:</span></span>

| <span data-ttu-id="1c4ef-283">EventType</span><span class="sxs-lookup"><span data-stu-id="1c4ef-283">EventType</span></span>       | <span data-ttu-id="1c4ef-284">Объект полезной нагрузки</span><span class="sxs-lookup"><span data-stu-id="1c4ef-284">Payload object</span></span>   | <span data-ttu-id="1c4ef-285">Описание</span><span class="sxs-lookup"><span data-stu-id="1c4ef-285">Description</span></span>                                                             | <span data-ttu-id="1c4ef-286">Область</span><span class="sxs-lookup"><span data-stu-id="1c4ef-286">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="1c4ef-287">messageReaction</span><span class="sxs-lookup"><span data-stu-id="1c4ef-287">messageReaction</span></span> | <span data-ttu-id="1c4ef-288">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="1c4ef-288">reactionsAdded</span></span>   | <span data-ttu-id="1c4ef-289">[Реакции, добавленные в сообщение бота](#reactions-added-to-bot-message).</span><span class="sxs-lookup"><span data-stu-id="1c4ef-289">[Reactions added to bot message](#reactions-added-to-bot-message).</span></span>           | <span data-ttu-id="1c4ef-290">Все</span><span class="sxs-lookup"><span data-stu-id="1c4ef-290">All</span></span>   |
| <span data-ttu-id="1c4ef-291">messageReaction</span><span class="sxs-lookup"><span data-stu-id="1c4ef-291">messageReaction</span></span> | <span data-ttu-id="1c4ef-292">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="1c4ef-292">reactionsRemoved</span></span> | <span data-ttu-id="1c4ef-293">[Реакции, удалены из сообщения бота](#reactions-removed-from-bot-message).</span><span class="sxs-lookup"><span data-stu-id="1c4ef-293">[Reactions removed from bot message](#reactions-removed-from-bot-message).</span></span> | <span data-ttu-id="1c4ef-294">Все</span><span class="sxs-lookup"><span data-stu-id="1c4ef-294">All</span></span> |

### <a name="reactions-added-to-bot-message"></a><span data-ttu-id="1c4ef-295">Реакции, добавленные в сообщение бота</span><span class="sxs-lookup"><span data-stu-id="1c4ef-295">Reactions added to bot message</span></span>

<span data-ttu-id="1c4ef-296">В следующем коде показан пример реакций на сообщение бота:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-296">The following code shows an example of reactions to a bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-297">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-297">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-298">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-298">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-299">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-299">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-300">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-300">Python</span></span>](#tab/python)

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

---

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="1c4ef-301">Реакции, удаленые из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="1c4ef-301">Reactions removed from bot message</span></span>

<span data-ttu-id="1c4ef-302">В следующем коде показан пример реакций, удаленых из сообщения бота:</span><span class="sxs-lookup"><span data-stu-id="1c4ef-302">The following code shows an example of reactions removed from bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-303">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-303">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-304">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-304">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="1c4ef-305">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-305">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="1c4ef-306">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-306">Python</span></span>](#tab/python)

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

---

## <a name="installation-update-event"></a><span data-ttu-id="1c4ef-307">Событие обновления установки</span><span class="sxs-lookup"><span data-stu-id="1c4ef-307">Installation update event</span></span>

<span data-ttu-id="1c4ef-308">Бот получает событие `installationUpdate` при установке бота в поток беседы.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-308">The bot receives an `installationUpdate` event when you install a bot to a conversation thread.</span></span> <span data-ttu-id="1c4ef-309">Спуск бота из потока также вызывает событие.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-309">Uninstallation of the bot from the thread also triggers the event.</span></span> <span data-ttu-id="1c4ef-310">При установке бота  будет добавлено поле действий в событии, а после  удаления бота поле действия будет *удаляться.*</span><span class="sxs-lookup"><span data-stu-id="1c4ef-310">On installing a bot, the **action** field in the event is set to *add*, and when the bot is uninstalled the **action** field is set to *remove*.</span></span>
 
> [!NOTE]
> <span data-ttu-id="1c4ef-311">При обновлении приложения и добавлении или удалите бот, действие также запускает `installationUpdate` событие.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-311">When you upgrade an application, and then add or remove a bot, the action also triggers the `installationUpdate` event.</span></span> <span data-ttu-id="1c4ef-312">Поле **действия** настроено на обновление *при* добавлении бота или *удаления-обновления* при удалите бот.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-312">The **action** field is set to *add-upgrade* if you add a bot or *remove-upgrade* if you remove a bot.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1c4ef-313">События обновления установки находятся в предварительной версии разработчика сегодня и будут доступны в марте 2021 г.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-313">Installation update events are in developer preview today and will be Generally Available (GA) in March 2021.</span></span> <span data-ttu-id="1c4ef-314">Чтобы просмотреть события обновления установки, можно переместить Teams клиента в общедоступный предварительный просмотр разработчика и добавить приложение лично или в команду или чат.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-314">To see the installation update events, you can move your Teams client to public developer preview, and add your app personally or to a team or a chat.</span></span>

### <a name="install-update-event"></a><span data-ttu-id="1c4ef-315">Событие установки обновления</span><span class="sxs-lookup"><span data-stu-id="1c4ef-315">Install update event</span></span>
<span data-ttu-id="1c4ef-316">Используйте событие `installationUpdate` для отправки вводного сообщения от бота при установке.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-316">Use the `installationUpdate` event to send an introductory message from your bot on installation.</span></span> <span data-ttu-id="1c4ef-317">Это событие поможет вам соответствовать требованиям конфиденциальности и хранения данных.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-317">This event helps you to meet your privacy and data retention requirements.</span></span> <span data-ttu-id="1c4ef-318">Кроме того, при удалении бота можно очистить и удалить данные пользователя или потока.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-318">You can also clean up and delete user or thread data when the bot is uninstalled.</span></span>

# <a name="c"></a>[<span data-ttu-id="1c4ef-319">C#</span><span class="sxs-lookup"><span data-stu-id="1c4ef-319">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task
OnInstallationUpdateActivityAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken) {
var activity = turnContext.Activity; if
(string.Equals(activity.Action, "Add",
StringComparison.InvariantCultureIgnoreCase)) {
// TO:DO Installation workflow }
else
{ // TO:DO Uninstallation workflow
} return; }
```

<span data-ttu-id="1c4ef-320">Кроме того, для добавления или  удаления  сценариев в качестве альтернативного метода для захвата события можно использовать специальный обработок.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-320">You can also use a dedicated handler for *add* or *remove* scenarios as an alternative method to capture an event.</span></span>

```csharp
protected override async Task
OnInstallationUpdateAddAsync(ITurnContext<IInstallationUpdateActivity>
turnContext, CancellationToken cancellationToken) {
// TO:DO Installation workflow return;
}
```

# <a name="typescript"></a>[<span data-ttu-id="1c4ef-321">TypeScript</span><span class="sxs-lookup"><span data-stu-id="1c4ef-321">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="1c4ef-322">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1c4ef-322">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="1c4ef-323">JSON</span><span class="sxs-lookup"><span data-stu-id="1c4ef-323">JSON</span></span>](#tab/json)

```json
{ 
  "action": "add", 
  "type": "installationUpdate", 
  "timestamp": "2020-10-20T22:08:07.869Z", 
  "id": "f:3033745319439849398", 
  "channelId": "msteams", 
  "serviceUrl": "https://smba.trafficmanager.net/amer/", 
  "from": { 
    "id": "sample id", 
    "aadObjectId": "sample AAD Object ID" 
  },
  "conversation": { 
    "isGroup": true, 
    "conversationType": "channel", 
    "tenantId": "sample tenant ID", 
    "id": "sample conversation Id@thread.skype" 
  }, 

  "recipient": { 
    "id": "sample reciepent bot ID", 
    "name": "bot name" 
  }, 
  "entities": [ 
    { 
      "locale": "en", 
      "platform": "Windows", 
      "type": "clientInfo" 
    } 
  ], 
  "channelData": { 
    "settings": { 
      "selectedChannel": { 
        "id": "sample channel ID@thread.skype" 
      } 
    }, 
    "channel": { 
      "id": "sample channel ID" 
    }, 
    "team": { 
      "id": "sample team ID" 
    }, 
    "tenant": { 
      "id": "sample tenant ID" 
    }, 
    "source": { 
      "name": "message" 
    } 
  }, 
  "locale": "en" 
}
```

# <a name="python"></a>[<span data-ttu-id="1c4ef-324">Python</span><span class="sxs-lookup"><span data-stu-id="1c4ef-324">Python</span></span>](#tab/python)

<span data-ttu-id="1c4ef-325">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1c4ef-325">Not available</span></span>

---

## <a name="code-sample"></a><span data-ttu-id="1c4ef-326">Пример кода</span><span class="sxs-lookup"><span data-stu-id="1c4ef-326">Code sample</span></span>

| <span data-ttu-id="1c4ef-327">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="1c4ef-327">**Sample name**</span></span> | <span data-ttu-id="1c4ef-328">**Описание**</span><span class="sxs-lookup"><span data-stu-id="1c4ef-328">**Description**</span></span> | <span data-ttu-id="1c4ef-329">**.NET**</span><span class="sxs-lookup"><span data-stu-id="1c4ef-329">**.NET**</span></span> | <span data-ttu-id="1c4ef-330">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="1c4ef-330">**Node.js**</span></span> | <span data-ttu-id="1c4ef-331">**Python**</span><span class="sxs-lookup"><span data-stu-id="1c4ef-331">**Python**</span></span> |
|----------|-----------------|----------|
| <span data-ttu-id="1c4ef-332">Бот-беседа</span><span class="sxs-lookup"><span data-stu-id="1c4ef-332">Conversation bot</span></span> | <span data-ttu-id="1c4ef-333">Пример кода для событий беседы ботов.</span><span class="sxs-lookup"><span data-stu-id="1c4ef-333">Sample code for bots conversation events.</span></span> | [<span data-ttu-id="1c4ef-334">View</span><span class="sxs-lookup"><span data-stu-id="1c4ef-334">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)  | [<span data-ttu-id="1c4ef-335">View</span><span class="sxs-lookup"><span data-stu-id="1c4ef-335">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="1c4ef-336">View</span><span class="sxs-lookup"><span data-stu-id="1c4ef-336">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="1c4ef-337">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="1c4ef-337">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c4ef-338">Отправка упреждающих сообщений</span><span class="sxs-lookup"><span data-stu-id="1c4ef-338">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
