---
title: Получение контекста для ленты
description: Сведения о том, как получить контекст для боты в Microsoft Teams
keywords: контекст Боты Teams
ms.date: 05/20/2019
ms.openlocfilehash: 2dea6fd51e7274fa899d9ae882441a21618d7e09
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675653"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="c7989-104">Получение контекста для ленты Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c7989-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="c7989-105">Ваш робот может получить доступ к дополнительному контексту для команды или чата, например для профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="c7989-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="c7989-106">Эти сведения можно использовать, чтобы расширить функциональные возможности Bot и предоставить более персонализированный интерфейс.</span><span class="sxs-lookup"><span data-stu-id="c7989-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
> <span data-ttu-id="c7989-107">Для этих специальных&ndash;API-интерфейсов ленты Microsoft Teams можно получить доступ через свои расширения для пакета SDK для Bot Builder.</span><span class="sxs-lookup"><span data-stu-id="c7989-107">These Microsoft Teams&ndash;specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span> <span data-ttu-id="c7989-108">Для C#/.нет Скачайте наш пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="c7989-108">For C#/.NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="c7989-109">Для разработки Node. js можно установить пакет NPM [ботбуилдер — Teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="c7989-109">For Node.js development, you can install the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span> <span data-ttu-id="c7989-110">Оба комплекта предназначены для целевого построителя ленты v3.</span><span class="sxs-lookup"><span data-stu-id="c7989-110">Both SDKs target Bot Builder v3.</span></span>

## <a name="fetching-the-team-roster"></a><span data-ttu-id="c7989-111">Получение списка команд</span><span class="sxs-lookup"><span data-stu-id="c7989-111">Fetching the team roster</span></span>

<span data-ttu-id="c7989-112">Ваш робот может запросить список участников группы и их базовые профили, в том числе идентификаторы пользователей Teams и Azure Active Directory (Azure AD), такие как Name и objectId.</span><span class="sxs-lookup"><span data-stu-id="c7989-112">Your bot can query for the list of team members and their basic profiles, which includes Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="c7989-113">Эти сведения можно использовать для сопоставления удостоверений пользователей; Например, чтобы проверить, является ли пользователь, вошедший на вкладку с помощью учетных данных Azure AD, участником команды.</span><span class="sxs-lookup"><span data-stu-id="c7989-113">You can use this information to correlate user identities; for example, to check whether a user logged into a tab through Azure AD credentials is a member of the team.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="c7989-114">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="c7989-114">REST API example</span></span>

<span data-ttu-id="c7989-115">Вы можете отправить запрос GET напрямую [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), используя значение в `serviceUrl` качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c7989-115">You can directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="c7989-116">`teamId` Можно найти в `channeldata` объекте полезных данных действия, который получит ваш почтовый робот в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="c7989-116">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>
* <span data-ttu-id="c7989-117">Когда пользователь получает сообщения или взаимодействует с Bot в контексте команды (см. [Получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span><span class="sxs-lookup"><span data-stu-id="c7989-117">When a user messages or interacts with your bot in a team context (see [Receiving Messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span></span>
* <span data-ttu-id="c7989-118">Добавление нового пользователя или ленты в команду (см. [пользователь, добавленный в группу](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span><span class="sxs-lookup"><span data-stu-id="c7989-118">When a new user or bot is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span></span>

> [!NOTE]
>* <span data-ttu-id="c7989-119">Обязательно используйте идентификатор команды при вызове API</span><span class="sxs-lookup"><span data-stu-id="c7989-119">Make sure to use the team id when calling the api</span></span>
>* <span data-ttu-id="c7989-120">Значение `serviceUrl` "является стабильным, но может измениться".</span><span class="sxs-lookup"><span data-stu-id="c7989-120">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="c7989-121">Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="c7989-121">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="c7989-122">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="c7989-122">.NET example</span></span>

<span data-ttu-id="c7989-123">Call `GetConversationMembersAsync` using `Team.Id` для возврата списка идентификаторов пользователей.</span><span class="sxs-lookup"><span data-stu-id="c7989-123">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejstypescript-example"></a><span data-ttu-id="c7989-124">Пример Node. js/TypeScript</span><span class="sxs-lookup"><span data-stu-id="c7989-124">Node.js/TypeScript example</span></span>

<span data-ttu-id="c7989-125">В следующем примере используются [расширения Microsoft Teams для пакета SDK построителя ленты для Node. js](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="c7989-125">The following example uses the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

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

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="c7989-126">Получение профиля пользователя или списка в личном или группом чате</span><span class="sxs-lookup"><span data-stu-id="c7989-126">Fetching user profile or roster in personal or group chat</span></span>

<span data-ttu-id="c7989-127">Вы также можете выполнить один вызов API для любого личного чата, чтобы получить сведения о профиле пользователя в чате.</span><span class="sxs-lookup"><span data-stu-id="c7989-127">You can also make the same API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="c7989-128">Вызовы API и методы SDK идентичны получению списка команд, как и объект Response.</span><span class="sxs-lookup"><span data-stu-id="c7989-128">The API call and SDK methods are identical to fetching the team roster, as is the response object.</span></span> <span data-ttu-id="c7989-129">Единственное отличие заключается в том, что `conversationId` вместо него `teamId`передается значение.</span><span class="sxs-lookup"><span data-stu-id="c7989-129">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetching-the-list-of-channels-in-a-team"></a><span data-ttu-id="c7989-130">Получение списка каналов в команде</span><span class="sxs-lookup"><span data-stu-id="c7989-130">Fetching the list of channels in a team</span></span>

<span data-ttu-id="c7989-131">Ваш робот может запросить список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="c7989-131">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="c7989-132">По умолчанию возвращается `null` имя общего канала, позволяющее выполнять локализацию.</span><span class="sxs-lookup"><span data-stu-id="c7989-132">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="c7989-133">Идентификатор канала для общего канала всегда соответствует ИДЕНТИФИКАТОРу группы.</span><span class="sxs-lookup"><span data-stu-id="c7989-133">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="c7989-134">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="c7989-134">REST API example</span></span>

<span data-ttu-id="c7989-135">Вы можете отправить запрос GET напрямую `/teams/{teamId}/conversations/`, используя значение в `serviceUrl` качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="c7989-135">You can directly issue a GET request on `/teams/{teamId}/conversations/`, using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="c7989-136">Единственный источник `teamId` — это сообщение от контекста команды — либо сообщение от пользователя, либо сообщение, которое поступает от пользователя Bot при его добавлении в команду (см. [пользователь или пользователь, добавленный в команду](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span><span class="sxs-lookup"><span data-stu-id="c7989-136">The only source for `teamId` is a message from the team context - either a message from a user or the message that your bot receives when it is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span></span>

> [!NOTE]
> <span data-ttu-id="c7989-137">Значение `serviceUrl` "является стабильным, но может измениться".</span><span class="sxs-lookup"><span data-stu-id="c7989-137">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="c7989-138">Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl`.</span><span class="sxs-lookup"><span data-stu-id="c7989-138">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="c7989-139">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="c7989-139">.NET example</span></span>

<span data-ttu-id="c7989-140">В следующем примере используется `FetchChannelList` вызов из [расширений Microsoft TEAMS для пакета SDK построителя построителя для .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span><span class="sxs-lookup"><span data-stu-id="c7989-140">The following example uses the `FetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="c7989-141">Пример Node. js</span><span class="sxs-lookup"><span data-stu-id="c7989-141">Node.js example</span></span>

<span data-ttu-id="c7989-142">В следующем примере используется `fetchChannelList` вызов из [расширений Microsoft TEAMS для пакета SDK построителя ленты для Node. js](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="c7989-142">The following example uses `fetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

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
