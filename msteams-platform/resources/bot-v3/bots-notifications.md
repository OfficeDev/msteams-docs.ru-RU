---
title: Обработка событий бота
description: Описывает, как обрабатывать события в ботах для Microsoft Teams
keywords: события командных ботов
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 6a9eaab388927fcff51d7883e1a61ca1cec81fac
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069078"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="039dd-104">Обработка событий бота в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="039dd-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="039dd-105">Microsoft Teams отправляет уведомления боту об изменениях или событиях, которые происходят в сферах, где активен бот.</span><span class="sxs-lookup"><span data-stu-id="039dd-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="039dd-106">Эти события можно использовать для запуска логики службы, например следующих:</span><span class="sxs-lookup"><span data-stu-id="039dd-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="039dd-107">Запуск приветствия при добавлении бота в команду.</span><span class="sxs-lookup"><span data-stu-id="039dd-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="039dd-108">Сведения о групповом запросе и кэше при добавлении бота в групповой чат.</span><span class="sxs-lookup"><span data-stu-id="039dd-108">Query and cache group information when the bot is added to a group chat.</span></span>
* <span data-ttu-id="039dd-109">Обновление кэшных сведений о членстве в команде или сведениях о канале.</span><span class="sxs-lookup"><span data-stu-id="039dd-109">Update cached information on team membership or channel information.</span></span>
* <span data-ttu-id="039dd-110">Удалите кэшные сведения для группы, если бот удален.</span><span class="sxs-lookup"><span data-stu-id="039dd-110">Remove cached information for a team if the bot is removed.</span></span>
* <span data-ttu-id="039dd-111">Когда сообщение бота нравится пользователю.</span><span class="sxs-lookup"><span data-stu-id="039dd-111">When a bot message is liked by a user.</span></span>

<span data-ttu-id="039dd-112">Каждое событие бота отправляется в качестве объекта, в `Activity` котором `messageType` определяется, какая информация находится в объекте.</span><span class="sxs-lookup"><span data-stu-id="039dd-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="039dd-113">Для сообщений типа `message` см. [в рублях Отправка и получение сообщений.](~/resources/bot-v3/bot-conversations/bots-conversations.md)</span><span class="sxs-lookup"><span data-stu-id="039dd-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="039dd-114">Teams и групповые события, которые обычно запускаются с типа, имеют дополнительные сведения о событиях Teams, переданные в рамках объекта, поэтому обработник событий должен запрашивать полезной нагрузки для метаданных Teams и дополнительных `conversationUpdate` `channelData` `channelData` `eventType` событий.</span><span class="sxs-lookup"><span data-stu-id="039dd-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="039dd-115">В следующей таблице перечислены события, которые бот может получить и принять меры.</span><span class="sxs-lookup"><span data-stu-id="039dd-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="039dd-116">Тип</span><span class="sxs-lookup"><span data-stu-id="039dd-116">Type</span></span>|<span data-ttu-id="039dd-117">Объект полезной нагрузки</span><span class="sxs-lookup"><span data-stu-id="039dd-117">Payload object</span></span>|<span data-ttu-id="039dd-118">Teams eventType</span><span class="sxs-lookup"><span data-stu-id="039dd-118">Teams eventType</span></span> |<span data-ttu-id="039dd-119">Описание</span><span class="sxs-lookup"><span data-stu-id="039dd-119">Description</span></span>|<span data-ttu-id="039dd-120">Область</span><span class="sxs-lookup"><span data-stu-id="039dd-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="039dd-121">Член, добавленный в команду</span><span class="sxs-lookup"><span data-stu-id="039dd-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="039dd-122">все</span><span class="sxs-lookup"><span data-stu-id="039dd-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="039dd-123">Участник был удален из группы</span><span class="sxs-lookup"><span data-stu-id="039dd-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="039dd-124">Команда была переименована</span><span class="sxs-lookup"><span data-stu-id="039dd-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="039dd-125">Создан канал</span><span class="sxs-lookup"><span data-stu-id="039dd-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="039dd-126">Канал был переименован</span><span class="sxs-lookup"><span data-stu-id="039dd-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="039dd-127">Канал был удален</span><span class="sxs-lookup"><span data-stu-id="039dd-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="039dd-128">Реакция на сообщение бота</span><span class="sxs-lookup"><span data-stu-id="039dd-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="039dd-129">все</span><span class="sxs-lookup"><span data-stu-id="039dd-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="039dd-130">Реакция, удаленная из сообщения бота</span><span class="sxs-lookup"><span data-stu-id="039dd-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="039dd-131">все</span><span class="sxs-lookup"><span data-stu-id="039dd-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="039dd-132">Добавление члена команды или бота</span><span class="sxs-lookup"><span data-stu-id="039dd-132">Team member or bot addition</span></span>

<span data-ttu-id="039dd-133">Событие отправляется вашему боту, когда он получает сведения об обновлениях членства [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) для команд, в которых оно было добавлено.</span><span class="sxs-lookup"><span data-stu-id="039dd-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="039dd-134">Бот также получает обновление при первом добавлении в личную беседу.</span><span class="sxs-lookup"><span data-stu-id="039dd-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="039dd-135">Обратите внимание, что пользовательские сведения () являются уникальными для вашего бота и могут быть кэшными для дальнейшего использования службой, например отправки сообщения `Id` конкретному пользователю.</span><span class="sxs-lookup"><span data-stu-id="039dd-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service, such as, sending a message to a specific user.</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="039dd-136">Бот или пользователь, добавленный в команду</span><span class="sxs-lookup"><span data-stu-id="039dd-136">Bot or user added to a team</span></span>

<span data-ttu-id="039dd-137">Событие с объектом в полезной нагрузке отправляется при добавлении бота в команду или в команду, в которой был добавлен `conversationUpdate` `membersAdded` бот.</span><span class="sxs-lookup"><span data-stu-id="039dd-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="039dd-138">Microsoft Teams также `eventType.teamMemberAdded` добавляется в `channelData` объект.</span><span class="sxs-lookup"><span data-stu-id="039dd-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="039dd-139">Так как это событие отправляется в обоих случаях, необходимо разсмеять объект, чтобы определить, является ли добавление пользователем или `membersAdded` самим ботом.</span><span class="sxs-lookup"><span data-stu-id="039dd-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="039dd-140">В последнем случае лучше всего отправлять [](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) приветствие на канал, чтобы пользователи могли понимать функции, которые предоставляет бот.</span><span class="sxs-lookup"><span data-stu-id="039dd-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="039dd-141">Пример кода. Проверка того, является ли бот добавленным участником</span><span class="sxs-lookup"><span data-stu-id="039dd-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="039dd-142">.NET</span><span class="sxs-lookup"><span data-stu-id="039dd-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="039dd-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="039dd-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="039dd-144">Пример схемы: бот добавлен в команду</span><span class="sxs-lookup"><span data-stu-id="039dd-144">Schema example: Bot added to team</span></span>

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

### <a name="user-added-to-a-meeting"></a><span data-ttu-id="039dd-145">Пользователь, добавленный к собранию</span><span class="sxs-lookup"><span data-stu-id="039dd-145">User Added to a meeting</span></span>

<span data-ttu-id="039dd-146">Событие `conversationUpdate` с объектом в полезной нагрузке отправляется при добавлении пользователя на `membersAdded` закрытое запланированное собрание.</span><span class="sxs-lookup"><span data-stu-id="039dd-146">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when a user is added to a private scheduled meeting.</span></span> <span data-ttu-id="039dd-147">Сведения о событии будут отправлены, даже если анонимные пользователи присоединятся к собранию.</span><span class="sxs-lookup"><span data-stu-id="039dd-147">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="039dd-148">При добавлении анонимного пользователя в собрание объект полезной нагрузки membersAdded не имеет `aadObjectId` поля.</span><span class="sxs-lookup"><span data-stu-id="039dd-148">When an anonymous user is added to a meeting, membersAdded payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="039dd-149">Когда анонимный пользователь добавляется в собрание, объект в полезной нагрузке всегда имеет id организатора собрания, даже если анонимный пользователь был добавлен `from` другим презентером.</span><span class="sxs-lookup"><span data-stu-id="039dd-149">When an anonymous user is added to a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was added by another presenter.</span></span>

#### <a name="schema-example-user-added-to-meeting"></a><span data-ttu-id="039dd-150">Пример схемы: пользователь добавлен в собрание</span><span class="sxs-lookup"><span data-stu-id="039dd-150">Schema example: User added to meeting</span></span>

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

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="039dd-151">Бот, добавленный только для личного контекста</span><span class="sxs-lookup"><span data-stu-id="039dd-151">Bot added for personal context only</span></span>

<span data-ttu-id="039dd-152">Ваш бот получает `conversationUpdate` с, `membersAdded` когда пользователь добавляет его непосредственно для личного чата.</span><span class="sxs-lookup"><span data-stu-id="039dd-152">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="039dd-153">В этом случае полезной нагрузки, получаемой ботом, объект не `channelData.team` содержится.</span><span class="sxs-lookup"><span data-stu-id="039dd-153">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="039dd-154">Вы должны использовать это в качестве фильтра, если вы хотите, чтобы ваш бот предложил другое приветствие [в](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) зависимости от области.</span><span class="sxs-lookup"><span data-stu-id="039dd-154">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="039dd-155">Для личных масштабных ботов боты получают событие несколько раз, даже если бот удален и `conversationUpdate` повторно добавлен.</span><span class="sxs-lookup"><span data-stu-id="039dd-155">For personal scoped bots, your bot will  receive the `conversationUpdate` event multiple times, even if the bot is removed and re-added.</span></span> <span data-ttu-id="039dd-156">Для разработки и тестирования может оказаться полезным добавить функцию помощника, которая позволит полностью сбросить бот.</span><span class="sxs-lookup"><span data-stu-id="039dd-156">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="039dd-157">Дополнительные [ сведения о реализации этого](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts)Node.js или [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) примере.</span><span class="sxs-lookup"><span data-stu-id="039dd-157">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="039dd-158">Пример схемы: бот добавлен в личный контекст</span><span class="sxs-lookup"><span data-stu-id="039dd-158">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="039dd-159">Удален член команды или бот</span><span class="sxs-lookup"><span data-stu-id="039dd-159">Team member or bot removed</span></span>

<span data-ttu-id="039dd-160">Событие с объектом в полезной нагрузке отправляется, когда бот удаляется из группы или пользователь удаляется из команды, в которой был `conversationUpdate` `membersRemoved` добавлен бот.</span><span class="sxs-lookup"><span data-stu-id="039dd-160">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="039dd-161">Microsoft Teams также `eventType.teamMemberRemoved` добавляется в `channelData` объект.</span><span class="sxs-lookup"><span data-stu-id="039dd-161">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="039dd-162">Как и в объекте, необходимо размазить объект для ID приложения вашего бота, чтобы определить, `membersAdded` `membersRemoved` кто был удален.</span><span class="sxs-lookup"><span data-stu-id="039dd-162">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="039dd-163">Пример схемы: удален член команды</span><span class="sxs-lookup"><span data-stu-id="039dd-163">Schema example: Team member removed</span></span>

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

### <a name="user-removed-from-a-meeting"></a><span data-ttu-id="039dd-164">Пользователь, удаленый из собрания</span><span class="sxs-lookup"><span data-stu-id="039dd-164">User removed from a meeting</span></span>

<span data-ttu-id="039dd-165">Событие с объектом в полезной нагрузке отправляется при удалении пользователя из `conversationUpdate` `membersRemoved` закрытого запланированного собрания.</span><span class="sxs-lookup"><span data-stu-id="039dd-165">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when a user is removed from a private scheduled meeting.</span></span> <span data-ttu-id="039dd-166">Сведения о событии будут отправлены, даже если анонимные пользователи присоединятся к собранию.</span><span class="sxs-lookup"><span data-stu-id="039dd-166">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="039dd-167">Когда анонимный пользователь удаляется из собрания, объект полезной нагрузки membersRemoved не имеет `aadObjectId` поля.</span><span class="sxs-lookup"><span data-stu-id="039dd-167">When an anonymous user is removed from a meeting, membersRemoved payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="039dd-168">Когда анонимный пользователь удаляется из собрания, объект в полезной нагрузке всегда имеет id организатора собрания, даже если анонимный пользователь был удален другим `from` презентщиком.</span><span class="sxs-lookup"><span data-stu-id="039dd-168">When an anonymous user is removed from a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was removed by another presenter.</span></span>

#### <a name="schema-example-user-removed-from-meeting"></a><span data-ttu-id="039dd-169">Пример схемы: пользователь удален из собрания</span><span class="sxs-lookup"><span data-stu-id="039dd-169">Schema example: User removed from meeting</span></span>

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

## <a name="team-name-updates"></a><span data-ttu-id="039dd-170">Обновления имени команды</span><span class="sxs-lookup"><span data-stu-id="039dd-170">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="039dd-171">Нет функций для запроса всех имен команд, и имя команды не возвращается в полезной нагрузке из других событий.</span><span class="sxs-lookup"><span data-stu-id="039dd-171">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="039dd-172">Ваш бот уведомлен о переименовании команды, в которая он находится.</span><span class="sxs-lookup"><span data-stu-id="039dd-172">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="039dd-173">Он получает событие `conversationUpdate` в `eventType.teamRenamed` `channelData` объекте.</span><span class="sxs-lookup"><span data-stu-id="039dd-173">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="039dd-174">Обратите внимание, что уведомлений о создании или удалении группы нет, так как боты существуют только в составе групп и не имеют видимости за пределами области, в которую они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="039dd-174">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="039dd-175">Пример схемы: переименована команда</span><span class="sxs-lookup"><span data-stu-id="039dd-175">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="039dd-176">Обновления канала</span><span class="sxs-lookup"><span data-stu-id="039dd-176">Channel updates</span></span>

<span data-ttu-id="039dd-177">Ваш бот уведомлен, когда канал создается, переименовываются или удаляются в команде, в которой он был добавлен.</span><span class="sxs-lookup"><span data-stu-id="039dd-177">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="039dd-178">Снова событие получено, и Teams определенного события отправляется в составе объекта, где данные канала являются GUID для канала, и содержит имя самого `conversationUpdate` `channelData.eventType` `channel.id` `channel.name` канала.</span><span class="sxs-lookup"><span data-stu-id="039dd-178">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="039dd-179">События канала следуют следующим образом:</span><span class="sxs-lookup"><span data-stu-id="039dd-179">The channel events are as follows:</span></span>

* <span data-ttu-id="039dd-180">**channelCreated** &emsp; Пользователь добавляет новый канал в команду.</span><span class="sxs-lookup"><span data-stu-id="039dd-180">**channelCreated**&emsp;A user adds a new channel to the team.</span></span>
* <span data-ttu-id="039dd-181">**ChannelRenamed** &emsp; Пользователь переименовывает существующий канал.</span><span class="sxs-lookup"><span data-stu-id="039dd-181">**channelRenamed**&emsp;A user renames an existing channel.</span></span>
* <span data-ttu-id="039dd-182">**channelDeleted** &emsp; Пользователь удаляет канал.</span><span class="sxs-lookup"><span data-stu-id="039dd-182">**channelDeleted**&emsp;A user removes a channel.</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="039dd-183">Полный пример схемы: channelCreated</span><span class="sxs-lookup"><span data-stu-id="039dd-183">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="039dd-184">Выдержка схемы: channelData для каналаRenamed</span><span class="sxs-lookup"><span data-stu-id="039dd-184">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="039dd-185">Выдержка схемы: channelData для channelDeleted</span><span class="sxs-lookup"><span data-stu-id="039dd-185">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="039dd-186">Реакции</span><span class="sxs-lookup"><span data-stu-id="039dd-186">Reactions</span></span>

<span data-ttu-id="039dd-187">Событие отправляется, когда пользователь добавляет или удаляет свою реакцию на сообщение, которое изначально было `messageReaction` отправлено вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="039dd-187">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="039dd-188">`replyToId` содержит ID конкретного сообщения.</span><span class="sxs-lookup"><span data-stu-id="039dd-188">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="039dd-189">Пример схемы: пользователю нравится сообщение</span><span class="sxs-lookup"><span data-stu-id="039dd-189">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="039dd-190">Пример схемы: пользователю не нравится сообщение</span><span class="sxs-lookup"><span data-stu-id="039dd-190">Schema example: A user un-likes a message</span></span>

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
