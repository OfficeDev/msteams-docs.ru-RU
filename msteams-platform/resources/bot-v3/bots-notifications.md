---
title: Обработка событий Bot
description: Описание способов обработки событий в боты для Microsoft Teams
keywords: события Боты Teams
ms.date: 05/20/2019
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 1161d21ee755cebe6ddb2a2d5a219f9538de77cf
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409052"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="f59e9-104">Обработка событий Bot в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f59e9-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="f59e9-105">Microsoft Teams отправляет уведомления для почтового робота для изменений или событий, происходящих в областях действия ленты.</span><span class="sxs-lookup"><span data-stu-id="f59e9-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="f59e9-106">Вы можете использовать эти события для активации логики службы, например:</span><span class="sxs-lookup"><span data-stu-id="f59e9-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="f59e9-107">Инициация приветственного сообщения при добавлении ленты в группу</span><span class="sxs-lookup"><span data-stu-id="f59e9-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="f59e9-108">Сведения о группах запросов и кэш-памяти при добавлении ленты в групповой чат</span><span class="sxs-lookup"><span data-stu-id="f59e9-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="f59e9-109">Обновление кэшированных сведений о членстве в группе или о канале</span><span class="sxs-lookup"><span data-stu-id="f59e9-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="f59e9-110">Удаление кэшированных данных для команды при удалении ленты.</span><span class="sxs-lookup"><span data-stu-id="f59e9-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="f59e9-111">Когда пользователю понравится сообщение Bot</span><span class="sxs-lookup"><span data-stu-id="f59e9-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="f59e9-112">Каждое событие Bot передается `Activity` в виде объекта, в котором `messageType` определяется, какая информация находится в объекте.</span><span class="sxs-lookup"><span data-stu-id="f59e9-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="f59e9-113">Сообщения типа messages `message` можно просмотреть в разделе [Отправка и получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="f59e9-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="f59e9-114">События Teams и Group, обычно активируемые для `conversationUpdate` типа, имеют дополнительные сведения о событиях Teams, передаваемые в рамках `channelData` объекта, и поэтому обработчик события должен запросить `channelData` полезные данные для Teams `eventType` и дополнительные метаданные, связанные с событиями.</span><span class="sxs-lookup"><span data-stu-id="f59e9-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="f59e9-115">В следующей таблице перечислены события, которые могут получать и предпринимать действия от пользователя Bot.</span><span class="sxs-lookup"><span data-stu-id="f59e9-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="f59e9-116">Type</span><span class="sxs-lookup"><span data-stu-id="f59e9-116">Type</span></span>|<span data-ttu-id="f59e9-117">Объект полезных данных</span><span class="sxs-lookup"><span data-stu-id="f59e9-117">Payload object</span></span>|<span data-ttu-id="f59e9-118">Тип события Teams</span><span class="sxs-lookup"><span data-stu-id="f59e9-118">Teams eventType</span></span> |<span data-ttu-id="f59e9-119">Описание</span><span class="sxs-lookup"><span data-stu-id="f59e9-119">Description</span></span>|<span data-ttu-id="f59e9-120">Область</span><span class="sxs-lookup"><span data-stu-id="f59e9-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="f59e9-121">Участник, добавленный в группу</span><span class="sxs-lookup"><span data-stu-id="f59e9-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="f59e9-122">ко</span><span class="sxs-lookup"><span data-stu-id="f59e9-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="f59e9-123">Участник удален из группы</span><span class="sxs-lookup"><span data-stu-id="f59e9-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="f59e9-124">Команда была переименована</span><span class="sxs-lookup"><span data-stu-id="f59e9-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="f59e9-125">Создан канал</span><span class="sxs-lookup"><span data-stu-id="f59e9-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="f59e9-126">Канал переименован</span><span class="sxs-lookup"><span data-stu-id="f59e9-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="f59e9-127">Канал удален</span><span class="sxs-lookup"><span data-stu-id="f59e9-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="f59e9-128">Реакция на сообщение Bot</span><span class="sxs-lookup"><span data-stu-id="f59e9-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="f59e9-129">ко</span><span class="sxs-lookup"><span data-stu-id="f59e9-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="f59e9-130">Реакция, удаленная из сообщения Bot</span><span class="sxs-lookup"><span data-stu-id="f59e9-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="f59e9-131">ко</span><span class="sxs-lookup"><span data-stu-id="f59e9-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="f59e9-132">Добавление участников группы или ленты</span><span class="sxs-lookup"><span data-stu-id="f59e9-132">Team member or bot addition</span></span>

<span data-ttu-id="f59e9-133">[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true)Событие отправляется в Bot при получении сведений об обновлениях членства для Teams, где она была добавлена.</span><span class="sxs-lookup"><span data-stu-id="f59e9-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="f59e9-134">Он также получает обновление, когда оно добавляется в первый раз специально для личных бесед.</span><span class="sxs-lookup"><span data-stu-id="f59e9-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="f59e9-135">Обратите внимание, что сведения о пользователе ( `Id` ) уникальны для почтового робота, и их можно кэшировать для будущего использования службой (например, для отправки сообщения определенному пользователю).</span><span class="sxs-lookup"><span data-stu-id="f59e9-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="f59e9-136">Bot или пользователь, добавленный в команду</span><span class="sxs-lookup"><span data-stu-id="f59e9-136">Bot or user added to a team</span></span>

<span data-ttu-id="f59e9-137">`conversationUpdate`Событие с `membersAdded` объектом в полезных данных отправляется при добавлении в команду ленты или нового пользователя в группу, в которую добавлен Bot.</span><span class="sxs-lookup"><span data-stu-id="f59e9-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="f59e9-138">Microsoft Teams также добавляет `eventType.teamMemberAdded` в `channelData` объект.</span><span class="sxs-lookup"><span data-stu-id="f59e9-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="f59e9-139">Так как это событие отправляется в обоих случаях, необходимо выполнить анализ `membersAdded` объекта, чтобы определить, был ли добавлен пользователь или сам робот.</span><span class="sxs-lookup"><span data-stu-id="f59e9-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="f59e9-140">В последнююмся случае рекомендуется отправить [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) на канал, чтобы пользователи могли ознакомиться с функциями, которые предоставляет ваш почтовый робот.</span><span class="sxs-lookup"><span data-stu-id="f59e9-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="f59e9-141">Пример кода: Проверка того, был ли элемент Bot добавлен.</span><span class="sxs-lookup"><span data-stu-id="f59e9-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="f59e9-142">.NET</span><span class="sxs-lookup"><span data-stu-id="f59e9-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="f59e9-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="f59e9-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="f59e9-144">Пример схемы: Bot добавлен в группу</span><span class="sxs-lookup"><span data-stu-id="f59e9-144">Schema example: Bot added to team</span></span>

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a><span data-ttu-id="f59e9-145">Пользователь, добавленный на собрание</span><span class="sxs-lookup"><span data-stu-id="f59e9-145">User Added to a meeting</span></span>

<span data-ttu-id="f59e9-146">`conversationUpdate`Событие с `membersAdded` объектом в полезных данных отправляется, когда пользователь добавляется в частное запланированное собрание.</span><span class="sxs-lookup"><span data-stu-id="f59e9-146">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when a user is added to a private scheduled meeting.</span></span> <span data-ttu-id="f59e9-147">Сведения о событии будут отправляться, даже если анонимные пользователи присоединяются к собранию.</span><span class="sxs-lookup"><span data-stu-id="f59e9-147">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="f59e9-148">Когда анонимный пользователь добавляется к собранию, объект полезных данных Мемберсаддед не имеет `aadObjectId` поля.</span><span class="sxs-lookup"><span data-stu-id="f59e9-148">When an anonymous user is added to a meeting, membersAdded payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="f59e9-149">Когда анонимный пользователь добавляется к собранию, `from` объект в полезных данных всегда будет иметь идентификатор организатора собрания, даже если анонимный пользователь добавлен другим докладчиком.</span><span class="sxs-lookup"><span data-stu-id="f59e9-149">When an anonymous user is added to a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was added by another presenter.</span></span>

#### <a name="schema-example-user-added-to-meeting"></a><span data-ttu-id="f59e9-150">Пример схемы: пользователь добавлен на собрание</span><span class="sxs-lookup"><span data-stu-id="f59e9-150">Schema example: User added to meeting</span></span>

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="f59e9-151">Добавление ленты только для личного контекста</span><span class="sxs-lookup"><span data-stu-id="f59e9-151">Bot added for personal context only</span></span>

<span data-ttu-id="f59e9-152">Пользователь Bot получает `conversationUpdate` `membersAdded` сведения о том, когда пользователь добавляет его непосредственно для личного чата.</span><span class="sxs-lookup"><span data-stu-id="f59e9-152">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="f59e9-153">В этом случае полезные данные, получаемые от botа, не содержат `channelData.team` объект.</span><span class="sxs-lookup"><span data-stu-id="f59e9-153">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="f59e9-154">Вы должны использовать этот фильтр в том случае, если вы хотите, чтобы ваш Bot предлагал другое [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) в зависимости от области действия.</span><span class="sxs-lookup"><span data-stu-id="f59e9-154">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="f59e9-155">Для личной Боты ваш робот получит `conversationUpdate` событие несколько раз, даже если он был удален и добавлен повторно.</span><span class="sxs-lookup"><span data-stu-id="f59e9-155">For personal scoped bots, your bot will  receive the `conversationUpdate` event multiple times, even if the bot is removed and re-added.</span></span> <span data-ttu-id="f59e9-156">Для разработки и тестирования может потребоваться добавить вспомогательную функцию, которая позволит полностью сбросить объект Bot.</span><span class="sxs-lookup"><span data-stu-id="f59e9-156">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="f59e9-157">Более подробную информацию об реализации этого примера можно узнать в [Node.js примере](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) или [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) .</span><span class="sxs-lookup"><span data-stu-id="f59e9-157">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="f59e9-158">Пример схемы: Bot добавлен в личный контекст</span><span class="sxs-lookup"><span data-stu-id="f59e9-158">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="f59e9-159">Участник группы или Bot удален</span><span class="sxs-lookup"><span data-stu-id="f59e9-159">Team member or bot removed</span></span>

<span data-ttu-id="f59e9-160">`conversationUpdate`Событие с `membersRemoved` объектом в полезных данных отправляется при удалении ленты из команды или при удалении пользователя из группы, в которую добавлен Bot.</span><span class="sxs-lookup"><span data-stu-id="f59e9-160">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="f59e9-161">Microsoft Teams также добавляет `eventType.teamMemberRemoved` в `channelData` объект.</span><span class="sxs-lookup"><span data-stu-id="f59e9-161">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="f59e9-162">Как и в `membersAdded` случае с объектом, необходимо проанализировать `membersRemoved` объект для идентификатора приложения Bot, чтобы определить, кто был удален.</span><span class="sxs-lookup"><span data-stu-id="f59e9-162">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="f59e9-163">Пример схемы: удален участник группы</span><span class="sxs-lookup"><span data-stu-id="f59e9-163">Schema example: Team member removed</span></span>

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

### <a name="user-removed-from-a-meeting"></a><span data-ttu-id="f59e9-164">Пользователь удален из собрания</span><span class="sxs-lookup"><span data-stu-id="f59e9-164">User removed from a meeting</span></span>

<span data-ttu-id="f59e9-165">`conversationUpdate`Событие с `membersRemoved` объектом в полезных данных отправляется, когда пользователь удаляется из частного запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="f59e9-165">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when a user is removed from a private scheduled meeting.</span></span> <span data-ttu-id="f59e9-166">Сведения о событии будут отправляться, даже если анонимные пользователи присоединяются к собранию.</span><span class="sxs-lookup"><span data-stu-id="f59e9-166">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
><span data-ttu-id="f59e9-167">_ Если анонимный пользователь удален из собрания, объект полезных данных Мемберсремовед не имеет `aadObjectId` поля.</span><span class="sxs-lookup"><span data-stu-id="f59e9-167">_ When an anonymous user is removed from a meeting, membersRemoved payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="f59e9-168">Когда анонимный пользователь удаляется из собрания, `from` объект в полезных данных всегда будет иметь идентификатор организатора собрания, даже если анонимный пользователь был удален другим докладчиком.</span><span class="sxs-lookup"><span data-stu-id="f59e9-168">When an anonymous user is removed from a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was removed by another presenter.</span></span>

#### <a name="schema-example-user-removed-from-meeting"></a><span data-ttu-id="f59e9-169">Пример схемы: пользователь удален из собрания</span><span class="sxs-lookup"><span data-stu-id="f59e9-169">Schema example: User removed from meeting</span></span>

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a><span data-ttu-id="f59e9-170">Обновления имени команды</span><span class="sxs-lookup"><span data-stu-id="f59e9-170">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="f59e9-171">Не существует функции для запроса всех имен команд, а имя команды не возвращается в полезных данных из других событий.</span><span class="sxs-lookup"><span data-stu-id="f59e9-171">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="f59e9-172">Ваш робот получает уведомление, когда группа, в которую она находится, была переименована.</span><span class="sxs-lookup"><span data-stu-id="f59e9-172">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="f59e9-173">Он получает `conversationUpdate` событие `eventType.teamRenamed` в `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="f59e9-173">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="f59e9-174">Обратите внимание, что уведомления о создании или удалении команды не отображаются, так как боты существует только в составе Teams и не отображается за пределами области, в которой они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="f59e9-174">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="f59e9-175">Пример схемы: команда переименована</span><span class="sxs-lookup"><span data-stu-id="f59e9-175">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="f59e9-176">Обновления канала</span><span class="sxs-lookup"><span data-stu-id="f59e9-176">Channel updates</span></span>

<span data-ttu-id="f59e9-177">Ваш робот получает уведомление о создании, переименовании или удалении канала в группе, в которой он был добавлен.</span><span class="sxs-lookup"><span data-stu-id="f59e9-177">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="f59e9-178">Опять же, `conversationUpdate` получается событие, а идентификатор события, зависящий от Teams, отправляется в составе `channelData.eventType` объекта, где данные канала  `channel.id` являются идентификатором GUID канала, и `channel.name` содержит само имя канала.</span><span class="sxs-lookup"><span data-stu-id="f59e9-178">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="f59e9-179">Ниже приведены события канала.</span><span class="sxs-lookup"><span data-stu-id="f59e9-179">The channel events are as follows:</span></span>

* <span data-ttu-id="f59e9-180">**чаннелкреатед** &emsp; Пользователь добавляет новый канал в команду.</span><span class="sxs-lookup"><span data-stu-id="f59e9-180">**channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="f59e9-181">**чаннелренамед** &emsp; Пользователь переименовывает существующий канал</span><span class="sxs-lookup"><span data-stu-id="f59e9-181">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="f59e9-182">**чаннелделетед** &emsp; Пользователь удаляет канал</span><span class="sxs-lookup"><span data-stu-id="f59e9-182">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="f59e9-183">Пример полной схемы: Чаннелкреатед</span><span class="sxs-lookup"><span data-stu-id="f59e9-183">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="f59e9-184">Фрагмент схемы: Чаннелдата для Чаннелренамед</span><span class="sxs-lookup"><span data-stu-id="f59e9-184">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="f59e9-185">Фрагмент схемы: Чаннелдата для Чаннелделетед</span><span class="sxs-lookup"><span data-stu-id="f59e9-185">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="f59e9-186">Реакция</span><span class="sxs-lookup"><span data-stu-id="f59e9-186">Reactions</span></span>

<span data-ttu-id="f59e9-187">`messageReaction`Событие отправляется, когда пользователь добавляет или удаляет его реакцию на сообщение, которое изначально было отправлено с помощью робота.</span><span class="sxs-lookup"><span data-stu-id="f59e9-187">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="f59e9-188">`replyToId` содержит идентификатор определенного сообщения.</span><span class="sxs-lookup"><span data-stu-id="f59e9-188">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="f59e9-189">Пример схемы: пользователю нравится сообщение</span><span class="sxs-lookup"><span data-stu-id="f59e9-189">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="f59e9-190">Пример схемы: пользователю не нравится сообщение</span><span class="sxs-lookup"><span data-stu-id="f59e9-190">Schema example: A user un-likes a message</span></span>

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
