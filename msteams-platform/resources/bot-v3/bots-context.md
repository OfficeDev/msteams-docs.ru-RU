---
title: Получите контекст для Microsoft Teams бота
description: Описывает, как получить контекст для ботов в Microsoft Teams
keywords: Контекст командных ботов
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: cda2e24816330964342b097f52bb955c8846c54a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566490"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="ac3a5-104">Получите контекст для Microsoft Teams бота</span><span class="sxs-lookup"><span data-stu-id="ac3a5-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ac3a5-105">Ваш бот может получить доступ к дополнительному контексту о команде или чате, например к профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="ac3a5-106">Эти сведения можно использовать для обогащения функциональных возможностей бота и предоставления более персонализированного опыта.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="ac3a5-107">Microsoft Teams API бота лучше всего получать через наши расширения для SDK-конструктора ботов.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="ac3a5-108">Для C# или .NET скачайте пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="ac3a5-109">Для Node.js разработки функциональность bot Builder для Teams включена в [SDK bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="ac3a5-110">Извлечение реестра команды</span><span class="sxs-lookup"><span data-stu-id="ac3a5-110">Fetch the team roster</span></span>

<span data-ttu-id="ac3a5-111">Бот может запрашивать список членов группы и их основные профили.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="ac3a5-112">Основные профили включают Teams и Azure Active Directory (AAD), такие как имя и ID объекта.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="ac3a5-113">Эти сведения можно использовать для сопоставления удостоверений пользователей.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="ac3a5-114">Например, проверьте, входит ли пользователь в вкладку с помощью учетных данных AAD.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="ac3a5-115">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="ac3a5-115">REST API example</span></span>

<span data-ttu-id="ac3a5-116">Непосредственно выдай запрос [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) GET, используя `serviceUrl` значение в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="ac3a5-117">Объект можно найти в объекте полезной нагрузки, получаемой ботом в `teamId` `channeldata` следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="ac3a5-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="ac3a5-118">Когда пользователь передает сообщения или взаимодействует с ботом в контексте группы.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="ac3a5-119">Дополнительные сведения см. [в сообщении о получении сообщений.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)</span><span class="sxs-lookup"><span data-stu-id="ac3a5-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="ac3a5-120">При добавлении нового пользователя или бота в команду.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="ac3a5-121">Дополнительные сведения см. в [записи бота или пользователя, добавленного в команду.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)</span><span class="sxs-lookup"><span data-stu-id="ac3a5-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="ac3a5-122">Всегда используйте командный ID при вызове API.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="ac3a5-123">Значение `serviceUrl` имеет тенденцию быть стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="ac3a5-124">По прибытии нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="ac3a5-125">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="ac3a5-125">.NET example</span></span>

<span data-ttu-id="ac3a5-126">Вызов `GetConversationMembersAsync` с помощью возврата списка `Team.Id` пользовательских ИД.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="ac3a5-127">Node.js или typeScript</span><span class="sxs-lookup"><span data-stu-id="ac3a5-127">Node.js or TypeScript example</span></span>

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="ac3a5-128">Извлечение профиля пользователя или реестра в личном или групповом чате</span><span class="sxs-lookup"><span data-stu-id="ac3a5-128">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="ac3a5-129">Вы можете сделать вызов API для любого личного чата, чтобы получить сведения о профиле пользователя в чате с ботом.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-129">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="ac3a5-130">Вызов API, методы SDK и объект ответа идентичны запросу реестра группы.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-130">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="ac3a5-131">Единственное отличие состоит в том, что вы передаете вместо `conversationId` `teamId` .</span><span class="sxs-lookup"><span data-stu-id="ac3a5-131">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="ac3a5-132">Извлечение списка каналов в команде</span><span class="sxs-lookup"><span data-stu-id="ac3a5-132">Fetch the list of channels in a team</span></span>

<span data-ttu-id="ac3a5-133">Бот может запрашивать список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-133">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="ac3a5-134">Для локализации возвращается имя общего канала по `null` умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-134">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="ac3a5-135">ID канала для общего канала всегда совпадает с командным ИД.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-135">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="ac3a5-136">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="ac3a5-136">REST API example</span></span>

<span data-ttu-id="ac3a5-137">Непосредственно выдай запрос `/teams/{teamId}/conversations/` GET, используя `serviceUrl` значение в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-137">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="ac3a5-138">Единственным источником для `teamId` этого является сообщение из контекста группы.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-138">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="ac3a5-139">Это сообщение является либо сообщением от пользователя, либо сообщением, которое получает бот при добавлении в команду.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-139">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="ac3a5-140">Дополнительные сведения см. в [записи бота или пользователя, добавленного в команду.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)</span><span class="sxs-lookup"><span data-stu-id="ac3a5-140">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="ac3a5-141">Значение `serviceUrl` имеет тенденцию быть стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-141">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="ac3a5-142">По прибытии нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-142">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="ac3a5-143">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="ac3a5-143">.NET example</span></span>

<span data-ttu-id="ac3a5-144">В следующем примере используется вызов из расширений Teams для `FetchChannelList` [SDK bot Builder для .NET:](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="ac3a5-144">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="ac3a5-145">Node.js пример</span><span class="sxs-lookup"><span data-stu-id="ac3a5-145">Node.js example</span></span>

<span data-ttu-id="ac3a5-146">В следующем примере используется вызов из расширений Teams для `fetchChannelList` [SDK ](https://www.npmjs.com/package/botbuilder-teams)bot Builder для Node.js:</span><span class="sxs-lookup"><span data-stu-id="ac3a5-146">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

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

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="ac3a5-147">Получите clientInfo в контексте бота</span><span class="sxs-lookup"><span data-stu-id="ac3a5-147">Get clientInfo in your bot context</span></span>

<span data-ttu-id="ac3a5-148">Вы можете получить clientInfo в действии вашего бота.</span><span class="sxs-lookup"><span data-stu-id="ac3a5-148">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="ac3a5-149">ClientInfo содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="ac3a5-149">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="ac3a5-150">Locale</span><span class="sxs-lookup"><span data-stu-id="ac3a5-150">Locale</span></span>
* <span data-ttu-id="ac3a5-151">Страна</span><span class="sxs-lookup"><span data-stu-id="ac3a5-151">Country</span></span>
* <span data-ttu-id="ac3a5-152">Платформа</span><span class="sxs-lookup"><span data-stu-id="ac3a5-152">Platform</span></span>
* <span data-ttu-id="ac3a5-153">Timezone</span><span class="sxs-lookup"><span data-stu-id="ac3a5-153">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="ac3a5-154">Пример JSON</span><span class="sxs-lookup"><span data-stu-id="ac3a5-154">JSON example</span></span>

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

### <a name="c-example"></a><span data-ttu-id="ac3a5-155">C# пример</span><span class="sxs-lookup"><span data-stu-id="ac3a5-155">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a><span data-ttu-id="ac3a5-156">См. также</span><span class="sxs-lookup"><span data-stu-id="ac3a5-156">See also</span></span>

<span data-ttu-id="ac3a5-157">[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="ac3a5-157">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>