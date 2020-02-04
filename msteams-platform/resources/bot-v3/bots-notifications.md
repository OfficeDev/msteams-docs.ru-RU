---
title: Обработка событий Bot
description: Описание способов обработки событий в боты для Microsoft Teams
keywords: события Боты Teams
ms.date: 05/20/2019
ms.openlocfilehash: 06da5e6b0668e86012d87af3184493cdeb70aecd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675470"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="02f3e-104">Обработка событий Bot в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="02f3e-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="02f3e-105">Microsoft Teams отправляет уведомления для почтового робота для изменений или событий, происходящих в областях действия ленты.</span><span class="sxs-lookup"><span data-stu-id="02f3e-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="02f3e-106">Вы можете использовать эти события для активации логики службы, например:</span><span class="sxs-lookup"><span data-stu-id="02f3e-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="02f3e-107">Инициация приветственного сообщения при добавлении ленты в группу</span><span class="sxs-lookup"><span data-stu-id="02f3e-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="02f3e-108">Сведения о группах запросов и кэш-памяти при добавлении ленты в групповой чат</span><span class="sxs-lookup"><span data-stu-id="02f3e-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="02f3e-109">Обновление кэшированных сведений о членстве в группе или о канале</span><span class="sxs-lookup"><span data-stu-id="02f3e-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="02f3e-110">Удаление кэшированных данных для команды при удалении ленты.</span><span class="sxs-lookup"><span data-stu-id="02f3e-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="02f3e-111">Когда пользователю понравится сообщение Bot</span><span class="sxs-lookup"><span data-stu-id="02f3e-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="02f3e-112">Каждое событие Bot передается в `Activity` виде объекта, `messageType` в котором определяется, какая информация находится в объекте.</span><span class="sxs-lookup"><span data-stu-id="02f3e-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="02f3e-113">Сообщения типа `message`messages можно просмотреть в разделе [Отправка и получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="02f3e-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="02f3e-114">События Teams и Group, обычно активируемые для `conversationUpdate` типа, имеют дополнительные сведения о событиях Teams, передаваемые `channelData` в рамках объекта, и поэтому обработчик события должен запросить `channelData` полезные данные для Teams `eventType` и дополнительные метаданные, связанные с событиями.</span><span class="sxs-lookup"><span data-stu-id="02f3e-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="02f3e-115">В следующей таблице перечислены события, которые могут получать и предпринимать действия от пользователя Bot.</span><span class="sxs-lookup"><span data-stu-id="02f3e-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="02f3e-116">Тип</span><span class="sxs-lookup"><span data-stu-id="02f3e-116">Type</span></span>|<span data-ttu-id="02f3e-117">Объект полезных данных</span><span class="sxs-lookup"><span data-stu-id="02f3e-117">Payload object</span></span>|<span data-ttu-id="02f3e-118">Тип события Teams</span><span class="sxs-lookup"><span data-stu-id="02f3e-118">Teams eventType</span></span> |<span data-ttu-id="02f3e-119">Описание</span><span class="sxs-lookup"><span data-stu-id="02f3e-119">Description</span></span>|<span data-ttu-id="02f3e-120">Область</span><span class="sxs-lookup"><span data-stu-id="02f3e-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="02f3e-121">Участник, добавленный в группу</span><span class="sxs-lookup"><span data-stu-id="02f3e-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="02f3e-122">ко</span><span class="sxs-lookup"><span data-stu-id="02f3e-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="02f3e-123">Участник удален из группы</span><span class="sxs-lookup"><span data-stu-id="02f3e-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="02f3e-124">Команда была переименована</span><span class="sxs-lookup"><span data-stu-id="02f3e-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="02f3e-125">Создан канал</span><span class="sxs-lookup"><span data-stu-id="02f3e-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="02f3e-126">Канал переименован</span><span class="sxs-lookup"><span data-stu-id="02f3e-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="02f3e-127">Канал удален</span><span class="sxs-lookup"><span data-stu-id="02f3e-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="02f3e-128">Реакция на сообщение Bot</span><span class="sxs-lookup"><span data-stu-id="02f3e-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="02f3e-129">ко</span><span class="sxs-lookup"><span data-stu-id="02f3e-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="02f3e-130">Реакция, удаленная из сообщения Bot</span><span class="sxs-lookup"><span data-stu-id="02f3e-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="02f3e-131">ко</span><span class="sxs-lookup"><span data-stu-id="02f3e-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="02f3e-132">Добавление участников группы или ленты</span><span class="sxs-lookup"><span data-stu-id="02f3e-132">Team member or bot addition</span></span>

<span data-ttu-id="02f3e-133">[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) Событие отправляется в Bot при получении сведений об обновлениях членства для Teams, где она была добавлена.</span><span class="sxs-lookup"><span data-stu-id="02f3e-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="02f3e-134">Он также получает обновление, когда оно добавляется в первый раз специально для личных бесед.</span><span class="sxs-lookup"><span data-stu-id="02f3e-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="02f3e-135">Обратите внимание, что сведения`Id`о пользователе () уникальны для почтового робота, и их можно кэшировать для будущего использования службой (например, для отправки сообщения определенному пользователю).</span><span class="sxs-lookup"><span data-stu-id="02f3e-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="02f3e-136">Bot или пользователь, добавленный в команду</span><span class="sxs-lookup"><span data-stu-id="02f3e-136">Bot or user added to a team</span></span>

<span data-ttu-id="02f3e-137">`conversationUpdate` Событие с `membersAdded` объектом в полезных данных отправляется при добавлении в команду ленты или нового пользователя в группу, в которую добавлен Bot.</span><span class="sxs-lookup"><span data-stu-id="02f3e-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="02f3e-138">Microsoft Teams также `eventType.teamMemberAdded` добавляет в `channelData` объект.</span><span class="sxs-lookup"><span data-stu-id="02f3e-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="02f3e-139">Так как это событие отправляется в обоих случаях, необходимо выполнить анализ `membersAdded` объекта, чтобы определить, был ли добавлен пользователь или сам робот.</span><span class="sxs-lookup"><span data-stu-id="02f3e-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="02f3e-140">В последнююмся случае рекомендуется отправить [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) на канал, чтобы пользователи могли ознакомиться с функциями, которые предоставляет ваш почтовый робот.</span><span class="sxs-lookup"><span data-stu-id="02f3e-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="02f3e-141">Пример кода: Проверка того, был ли элемент Bot добавлен.</span><span class="sxs-lookup"><span data-stu-id="02f3e-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="02f3e-142">.NET</span><span class="sxs-lookup"><span data-stu-id="02f3e-142">.NET</span></span>

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a><span data-ttu-id="02f3e-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="02f3e-143">Node.js</span></span>

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="02f3e-144">Пример схемы: Bot добавлен в группу</span><span class="sxs-lookup"><span data-stu-id="02f3e-144">Schema example: Bot added to team</span></span>

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

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="02f3e-145">Добавление ленты только для личного контекста</span><span class="sxs-lookup"><span data-stu-id="02f3e-145">Bot added for personal context only</span></span>

<span data-ttu-id="02f3e-146">Пользователь Bot получает сведения `conversationUpdate` о `membersAdded` том, когда пользователь добавляет его непосредственно для личного чата.</span><span class="sxs-lookup"><span data-stu-id="02f3e-146">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="02f3e-147">В этом случае полезные данные, получаемые от botа, не `channelData.team` содержат объект.</span><span class="sxs-lookup"><span data-stu-id="02f3e-147">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="02f3e-148">Вы должны использовать этот фильтр в том случае, если вы хотите, чтобы ваш Bot предлагал другое [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) в зависимости от области действия.</span><span class="sxs-lookup"><span data-stu-id="02f3e-148">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="02f3e-149">Для личной области Боты ваш робот будет получать `conversationUpdate` событие только один раз, даже при удалении и повторном добавлении ленты.</span><span class="sxs-lookup"><span data-stu-id="02f3e-149">For personal scoped bots, your bot will only ever receive the `conversationUpdate` event a single time, even if the bot is removed and re-added.</span></span> <span data-ttu-id="02f3e-150">Для разработки и тестирования может потребоваться добавить вспомогательную функцию, которая позволит полностью сбросить объект Bot.</span><span class="sxs-lookup"><span data-stu-id="02f3e-150">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="02f3e-151">Для получения дополнительных сведений о реализации этого [примера, например, Node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) или [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) .</span><span class="sxs-lookup"><span data-stu-id="02f3e-151">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="02f3e-152">Пример схемы: Bot добавлен в личный контекст</span><span class="sxs-lookup"><span data-stu-id="02f3e-152">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="02f3e-153">Участник группы или Bot удален</span><span class="sxs-lookup"><span data-stu-id="02f3e-153">Team member or bot removed</span></span>

<span data-ttu-id="02f3e-154">`conversationUpdate` Событие с `membersRemoved` объектом в полезных данных отправляется при удалении ленты из команды или при удалении пользователя из группы, в которую добавлен Bot.</span><span class="sxs-lookup"><span data-stu-id="02f3e-154">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="02f3e-155">Microsoft Teams также `eventType.teamMemberRemoved` добавляет в `channelData` объект.</span><span class="sxs-lookup"><span data-stu-id="02f3e-155">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="02f3e-156">Как и в `membersAdded` случае с объектом, необходимо проанализировать `membersRemoved` объект для идентификатора приложения Bot, чтобы определить, кто был удален.</span><span class="sxs-lookup"><span data-stu-id="02f3e-156">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="02f3e-157">Пример схемы: удален участник группы</span><span class="sxs-lookup"><span data-stu-id="02f3e-157">Schema example: Team member removed</span></span>

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

## <a name="team-name-updates"></a><span data-ttu-id="02f3e-158">Обновления имени команды</span><span class="sxs-lookup"><span data-stu-id="02f3e-158">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="02f3e-159">Не существует функции для запроса всех имен команд, а имя команды не возвращается в полезных данных из других событий.</span><span class="sxs-lookup"><span data-stu-id="02f3e-159">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="02f3e-160">Ваш робот получает уведомление, когда группа, в которую она находится, была переименована.</span><span class="sxs-lookup"><span data-stu-id="02f3e-160">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="02f3e-161">Он получает `conversationUpdate` событие `eventType.teamRenamed` в `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="02f3e-161">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="02f3e-162">Обратите внимание, что уведомления о создании или удалении команды не отображаются, так как боты существует только в составе Teams и не отображается за пределами области, в которой они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="02f3e-162">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="02f3e-163">Пример схемы: команда переименована</span><span class="sxs-lookup"><span data-stu-id="02f3e-163">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="02f3e-164">Обновления канала</span><span class="sxs-lookup"><span data-stu-id="02f3e-164">Channel updates</span></span>

<span data-ttu-id="02f3e-165">Ваш робот получает уведомление о создании, переименовании или удалении канала в группе, в которой он был добавлен.</span><span class="sxs-lookup"><span data-stu-id="02f3e-165">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="02f3e-166">Опять же, `conversationUpdate` получается событие, а идентификатор события, зависящий от Teams, отправляется в `channelData.eventType` составе объекта, где данные канала `channel.id` являются идентификатором GUID канала, и `channel.name` содержит само имя канала.</span><span class="sxs-lookup"><span data-stu-id="02f3e-166">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="02f3e-167">Ниже приведены события канала.</span><span class="sxs-lookup"><span data-stu-id="02f3e-167">The channel events are as follows:</span></span>

* <span data-ttu-id="02f3e-168">**чаннелкреатед**&emsp;пользователь добавляет новый канал в команду.</span><span class="sxs-lookup"><span data-stu-id="02f3e-168">**channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="02f3e-169">**чаннелренамед**&emsp;пользователь переименовывает существующий канал</span><span class="sxs-lookup"><span data-stu-id="02f3e-169">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="02f3e-170">**чаннелделетед**&emsp;пользователь удаляет канал</span><span class="sxs-lookup"><span data-stu-id="02f3e-170">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="02f3e-171">Пример полной схемы: Чаннелкреатед</span><span class="sxs-lookup"><span data-stu-id="02f3e-171">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="02f3e-172">Фрагмент схемы: Чаннелдата для Чаннелренамед</span><span class="sxs-lookup"><span data-stu-id="02f3e-172">Schema excerpt: channelData for channelRenamed</span></span>

```json
⋮
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
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="02f3e-173">Фрагмент схемы: Чаннелдата для Чаннелделетед</span><span class="sxs-lookup"><span data-stu-id="02f3e-173">Schema excerpt: channelData for channelDeleted</span></span>

```json
⋮
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
⋮
```

## <a name="reactions"></a><span data-ttu-id="02f3e-174">Реакция</span><span class="sxs-lookup"><span data-stu-id="02f3e-174">Reactions</span></span>

<span data-ttu-id="02f3e-175">`messageReaction` Событие отправляется, когда пользователь добавляет или удаляет его реакцию на сообщение, которое изначально было отправлено с помощью робота.</span><span class="sxs-lookup"><span data-stu-id="02f3e-175">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="02f3e-176">`replyToId`содержит идентификатор определенного сообщения.</span><span class="sxs-lookup"><span data-stu-id="02f3e-176">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="02f3e-177">Пример схемы: пользователю нравится сообщение</span><span class="sxs-lookup"><span data-stu-id="02f3e-177">Schema example: A user likes a message</span></span>

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
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="02f3e-178">Пример схемы: пользователю не нравится сообщение</span><span class="sxs-lookup"><span data-stu-id="02f3e-178">Schema example: A user un-likes a message</span></span>

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
    "replyToId": "1575667808184"
}
```