---
title: Получите контекст для бота Microsoft Teams
description: Описание получения контекста для ботов в Microsoft Teams
keywords: контекст ботов teams
ms.date: 05/20/2019
ms.openlocfilehash: 1465e6624b4eaadd73e2d4d9cf87fccedc002e52
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231555"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="7f907-104">Получите контекст для бота Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="7f907-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="7f907-105">Бот может получить доступ к дополнительному контексту команды или чата, например к профилю пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f907-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="7f907-106">Эти сведения можно использовать для того, чтобы расширить функциональные возможности бота и обеспечить более персонализированное впечатление.</span><span class="sxs-lookup"><span data-stu-id="7f907-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="7f907-107">Доступ к API ботов для Microsoft Teams лучше всего получить с помощью наших расширений для SDK построитель ботов.</span><span class="sxs-lookup"><span data-stu-id="7f907-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="7f907-108">Для C# или .NET скачайте пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.</span><span class="sxs-lookup"><span data-stu-id="7f907-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="7f907-109">Для Node.js разработки функции построитель ботов для Teams включены в [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) 4.6.</span><span class="sxs-lookup"><span data-stu-id="7f907-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="7f907-110">Получить список команд</span><span class="sxs-lookup"><span data-stu-id="7f907-110">Fetch the team roster</span></span>

<span data-ttu-id="7f907-111">Бот может запрашивать список участников команды и их базовые профили.</span><span class="sxs-lookup"><span data-stu-id="7f907-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="7f907-112">Основные профили включают в себя ИД пользователей Teams и данные Azure Active Directory (AAD), такие как имя и ид объекта.</span><span class="sxs-lookup"><span data-stu-id="7f907-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="7f907-113">Эти сведения можно использовать для сопоставления удостоверений пользователей.</span><span class="sxs-lookup"><span data-stu-id="7f907-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="7f907-114">Например, проверьте, является ли пользователь, во время входа на вкладку с помощью учетных данных AAD, участником группы.</span><span class="sxs-lookup"><span data-stu-id="7f907-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="7f907-115">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="7f907-115">REST API example</span></span>

<span data-ttu-id="7f907-116">Напрямую выдают запрос [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) GET, используя `serviceUrl` значение в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="7f907-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="7f907-117">Его можно найти в объекте полезной нагрузки действия, получаемой ботом в `teamId` `channeldata` следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="7f907-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="7f907-118">Когда пользователь сообщает или взаимодействует с ботом в контексте команды.</span><span class="sxs-lookup"><span data-stu-id="7f907-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="7f907-119">Дополнительные сведения [см. в получении сообщений.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)</span><span class="sxs-lookup"><span data-stu-id="7f907-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="7f907-120">При добавлении нового пользователя или бота в команду.</span><span class="sxs-lookup"><span data-stu-id="7f907-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="7f907-121">Дополнительные сведения см. в [добавлении бота](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)или пользователя в команду.</span><span class="sxs-lookup"><span data-stu-id="7f907-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="7f907-122">Всегда используйте ИД команды при вызове API.</span><span class="sxs-lookup"><span data-stu-id="7f907-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="7f907-123">Значение `serviceUrl` обычно является стабильным, но может изменяться.</span><span class="sxs-lookup"><span data-stu-id="7f907-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="7f907-124">После поступления нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.</span><span class="sxs-lookup"><span data-stu-id="7f907-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="7f907-125">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="7f907-125">.NET example</span></span>

<span data-ttu-id="7f907-126">Вызов, `GetConversationMembersAsync` который используется для возврата списка `Team.Id` пользовательских ИД.</span><span class="sxs-lookup"><span data-stu-id="7f907-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="7f907-127">Node.js или TypeScript</span><span class="sxs-lookup"><span data-stu-id="7f907-127">Node.js or TypeScript example</span></span>

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

<span data-ttu-id="7f907-128">См. также примеры [Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="7f907-128">Also, see [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="7f907-129">Извлечение профиля пользователя или группы в личном или групповом чате</span><span class="sxs-lookup"><span data-stu-id="7f907-129">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="7f907-130">Вы можете сделать вызов API для любого личного чата, чтобы получить сведения профиля пользователя, который общается с ботом.</span><span class="sxs-lookup"><span data-stu-id="7f907-130">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="7f907-131">ВызовЫ API, методы SDK и объект ответа идентичны запросу в составе команды.</span><span class="sxs-lookup"><span data-stu-id="7f907-131">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="7f907-132">Единственное отличие заключается в том, что вы `conversationId` передаете вместо `teamId` .</span><span class="sxs-lookup"><span data-stu-id="7f907-132">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="7f907-133">Получить список каналов в команде</span><span class="sxs-lookup"><span data-stu-id="7f907-133">Fetch the list of channels in a team</span></span>

<span data-ttu-id="7f907-134">Бот может запросить список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="7f907-134">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="7f907-135">Возвращается имя общего канала по умолчанию для `null` локализации.</span><span class="sxs-lookup"><span data-stu-id="7f907-135">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="7f907-136">ИД канала для общего канала всегда совпадает с ИД команды.</span><span class="sxs-lookup"><span data-stu-id="7f907-136">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="7f907-137">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="7f907-137">REST API example</span></span>

<span data-ttu-id="7f907-138">Напрямую выдают запрос `/teams/{teamId}/conversations/` GET, используя `serviceUrl` значение в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="7f907-138">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="7f907-139">Единственным источником является `teamId` сообщение из контекста команды.</span><span class="sxs-lookup"><span data-stu-id="7f907-139">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="7f907-140">Это либо сообщение от пользователя, либо сообщение, которое бот получает при добавлении в команду.</span><span class="sxs-lookup"><span data-stu-id="7f907-140">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="7f907-141">Дополнительные сведения см. в [добавлении бота](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)или пользователя в команду.</span><span class="sxs-lookup"><span data-stu-id="7f907-141">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="7f907-142">Значение `serviceUrl` обычно является стабильным, но может изменяться.</span><span class="sxs-lookup"><span data-stu-id="7f907-142">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="7f907-143">После поступления нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.</span><span class="sxs-lookup"><span data-stu-id="7f907-143">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="7f907-144">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="7f907-144">.NET example</span></span>

<span data-ttu-id="7f907-145">В следующем примере используется вызов из расширений Teams для `FetchChannelList` [SDK построитель ботов для .NET:](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="7f907-145">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="7f907-146">Node.js примере</span><span class="sxs-lookup"><span data-stu-id="7f907-146">Node.js example</span></span>

<span data-ttu-id="7f907-147">В следующем примере используется вызов из расширений Teams для `fetchChannelList` [SDK построитель ботов для Node.js: ](https://www.npmjs.com/package/botbuilder-teams)</span><span class="sxs-lookup"><span data-stu-id="7f907-147">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

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

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="7f907-148">Получить clientInfo в контексте бота</span><span class="sxs-lookup"><span data-stu-id="7f907-148">Get clientInfo in your bot context</span></span>

<span data-ttu-id="7f907-149">Вы можете получить clientInfo в действии бота.</span><span class="sxs-lookup"><span data-stu-id="7f907-149">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="7f907-150">ClientInfo содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="7f907-150">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="7f907-151">Locale</span><span class="sxs-lookup"><span data-stu-id="7f907-151">Locale</span></span>
* <span data-ttu-id="7f907-152">Страна</span><span class="sxs-lookup"><span data-stu-id="7f907-152">Country</span></span>
* <span data-ttu-id="7f907-153">Платформа</span><span class="sxs-lookup"><span data-stu-id="7f907-153">Platform</span></span>
* <span data-ttu-id="7f907-154">Timezone</span><span class="sxs-lookup"><span data-stu-id="7f907-154">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="7f907-155">Пример JSON</span><span class="sxs-lookup"><span data-stu-id="7f907-155">JSON example</span></span>

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

### <a name="c-example"></a><span data-ttu-id="7f907-156">Пример C#</span><span class="sxs-lookup"><span data-stu-id="7f907-156">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```