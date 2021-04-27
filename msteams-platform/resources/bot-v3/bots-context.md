---
title: Получите контекст для бота Microsoft Teams
description: Описывает, как получить контекст для ботов в Microsoft Teams
keywords: Контекст командных ботов
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 154a276c65987955cfe20e5b7ce4ed2e8973cbfd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020662"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="c19b5-104">Получите контекст для бота Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c19b5-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="c19b5-105">Ваш бот может получить доступ к дополнительному контексту о команде или чате, например к профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="c19b5-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="c19b5-106">Эти сведения можно использовать для обогащения функциональных возможностей бота и предоставления более персонализированного опыта.</span><span class="sxs-lookup"><span data-stu-id="c19b5-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="c19b5-107">API-API для конкретных ботов Microsoft Teams лучше всего получить через наши расширения для SDK-конструктора ботов.</span><span class="sxs-lookup"><span data-stu-id="c19b5-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="c19b5-108">Для C# или .NET скачайте пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.</span><span class="sxs-lookup"><span data-stu-id="c19b5-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="c19b5-109">Для Node.js разработки функциональность Bot Builder for Teams включена в [SDK bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.</span><span class="sxs-lookup"><span data-stu-id="c19b5-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="c19b5-110">Извлечение реестра команды</span><span class="sxs-lookup"><span data-stu-id="c19b5-110">Fetch the team roster</span></span>

<span data-ttu-id="c19b5-111">Бот может запрашивать список членов группы и их основные профили.</span><span class="sxs-lookup"><span data-stu-id="c19b5-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="c19b5-112">Основные профили включают пользовательские ID Teams и сведения Azure Active Directory (AAD), такие как имя и ID объекта.</span><span class="sxs-lookup"><span data-stu-id="c19b5-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="c19b5-113">Эти сведения можно использовать для сопоставления удостоверений пользователей.</span><span class="sxs-lookup"><span data-stu-id="c19b5-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="c19b5-114">Например, проверьте, входит ли пользователь в вкладку с помощью учетных данных AAD.</span><span class="sxs-lookup"><span data-stu-id="c19b5-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="c19b5-115">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="c19b5-115">REST API example</span></span>

<span data-ttu-id="c19b5-116">Непосредственно выдай запрос [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) GET, используя `serviceUrl` значение в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c19b5-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="c19b5-117">Объект можно найти в объекте полезной нагрузки, получаемой ботом в `teamId` `channeldata` следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="c19b5-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="c19b5-118">Когда пользователь передает сообщения или взаимодействует с ботом в контексте группы.</span><span class="sxs-lookup"><span data-stu-id="c19b5-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="c19b5-119">Дополнительные сведения см. [в сообщении о получении сообщений.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)</span><span class="sxs-lookup"><span data-stu-id="c19b5-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="c19b5-120">При добавлении нового пользователя или бота в команду.</span><span class="sxs-lookup"><span data-stu-id="c19b5-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="c19b5-121">Дополнительные сведения см. в [записи бота или пользователя, добавленного в команду.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)</span><span class="sxs-lookup"><span data-stu-id="c19b5-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="c19b5-122">Всегда используйте командный ID при вызове API.</span><span class="sxs-lookup"><span data-stu-id="c19b5-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="c19b5-123">Значение `serviceUrl` имеет тенденцию быть стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="c19b5-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="c19b5-124">По прибытии нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.</span><span class="sxs-lookup"><span data-stu-id="c19b5-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

```json
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members

Response body
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com"
}]
```

### <a name="net-example"></a><span data-ttu-id="c19b5-125">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="c19b5-125">.NET example</span></span>

<span data-ttu-id="c19b5-126">Вызов `GetConversationMembersAsync` с помощью возврата списка `Team.Id` пользовательских ИД.</span><span class="sxs-lookup"><span data-stu-id="c19b5-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

```csharp
// Fetch the members in the current conversation
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));
var teamId = context.Activity.GetChannelData<TeamsChannelData>().Team.Id;
var members = await connector.Conversations.GetConversationMembersAsync(teamId);

// Concatenate information about all members into a string
var sb = new StringBuilder();
foreach (var member in members.AsTeamsChannelAccounts())
{
    sb.AppendFormat(
        "GivenName = {0}, TeamsMemberId = {1}",
        member.Name, member.Id);

    sb.AppendLine();
}

// Post the member info back into the conversation
await context.PostAsync($"People in this conversation: {sb.ToString()}");
```

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="c19b5-127">Node.js или typeScript</span><span class="sxs-lookup"><span data-stu-id="c19b5-127">Node.js or TypeScript example</span></span>

```typescript

[...]
import * as builder from "botbuilder";
[...]

var teamId = session.message.sourceEvent.team.id;
connector.fetchMembers(
  (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is some error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

<span data-ttu-id="c19b5-128">Кроме того, [см. примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="c19b5-128">Also, see [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="c19b5-129">Извлечение профиля пользователя или реестра в личном или групповом чате</span><span class="sxs-lookup"><span data-stu-id="c19b5-129">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="c19b5-130">Вы можете сделать вызов API для любого личного чата, чтобы получить сведения о профиле пользователя в чате с ботом.</span><span class="sxs-lookup"><span data-stu-id="c19b5-130">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="c19b5-131">Вызов API, методы SDK и объект ответа идентичны запросу реестра группы.</span><span class="sxs-lookup"><span data-stu-id="c19b5-131">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="c19b5-132">Единственное отличие состоит в том, что вы передаете вместо `conversationId` `teamId` .</span><span class="sxs-lookup"><span data-stu-id="c19b5-132">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="c19b5-133">Извлечение списка каналов в команде</span><span class="sxs-lookup"><span data-stu-id="c19b5-133">Fetch the list of channels in a team</span></span>

<span data-ttu-id="c19b5-134">Бот может запрашивать список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="c19b5-134">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="c19b5-135">Для локализации возвращается имя общего канала по `null` умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c19b5-135">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="c19b5-136">ID канала для общего канала всегда совпадает с командным ИД.</span><span class="sxs-lookup"><span data-stu-id="c19b5-136">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="c19b5-137">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="c19b5-137">REST API example</span></span>

<span data-ttu-id="c19b5-138">Непосредственно выдай запрос `/teams/{teamId}/conversations/` GET, используя `serviceUrl` значение в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c19b5-138">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="c19b5-139">Единственным источником для `teamId` этого является сообщение из контекста группы.</span><span class="sxs-lookup"><span data-stu-id="c19b5-139">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="c19b5-140">Это сообщение является либо сообщением от пользователя, либо сообщением, которое получает бот при добавлении в команду.</span><span class="sxs-lookup"><span data-stu-id="c19b5-140">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="c19b5-141">Дополнительные сведения см. в [записи бота или пользователя, добавленного в команду.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)</span><span class="sxs-lookup"><span data-stu-id="c19b5-141">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="c19b5-142">Значение `serviceUrl` имеет тенденцию быть стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="c19b5-142">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="c19b5-143">По прибытии нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.</span><span class="sxs-lookup"><span data-stu-id="c19b5-143">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

```json
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```

#### <a name="net-example"></a><span data-ttu-id="c19b5-144">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="c19b5-144">.NET example</span></span>

<span data-ttu-id="c19b5-145">В следующем примере используется вызов из расширений Teams для `FetchChannelList` [SDK bot Builder для .NET:](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="c19b5-145">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="c19b5-146">Node.js пример</span><span class="sxs-lookup"><span data-stu-id="c19b5-146">Node.js example</span></span>

<span data-ttu-id="c19b5-147">В следующем примере используется вызов из расширений Teams для `fetchChannelList` [SDK ](https://www.npmjs.com/package/botbuilder-teams)bot Builder для Node.js:</span><span class="sxs-lookup"><span data-stu-id="c19b5-147">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

```javascript
var teamId = session.message.sourceEvent.team.id;
connector.fetchChannelList(
  (session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is an error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="c19b5-148">Получите clientInfo в контексте бота</span><span class="sxs-lookup"><span data-stu-id="c19b5-148">Get clientInfo in your bot context</span></span>

<span data-ttu-id="c19b5-149">Вы можете получить clientInfo в действии вашего бота.</span><span class="sxs-lookup"><span data-stu-id="c19b5-149">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="c19b5-150">ClientInfo содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="c19b5-150">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="c19b5-151">Locale</span><span class="sxs-lookup"><span data-stu-id="c19b5-151">Locale</span></span>
* <span data-ttu-id="c19b5-152">Страна</span><span class="sxs-lookup"><span data-stu-id="c19b5-152">Country</span></span>
* <span data-ttu-id="c19b5-153">Платформа</span><span class="sxs-lookup"><span data-stu-id="c19b5-153">Platform</span></span>
* <span data-ttu-id="c19b5-154">Timezone</span><span class="sxs-lookup"><span data-stu-id="c19b5-154">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="c19b5-155">Пример JSON</span><span class="sxs-lookup"><span data-stu-id="c19b5-155">JSON example</span></span>

```json
[
    {
        "type": "clientInfo",
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "Asia/Calcutta"
    }
]
```

### <a name="c-example"></a><span data-ttu-id="c19b5-156">C# пример</span><span class="sxs-lookup"><span data-stu-id="c19b5-156">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```
