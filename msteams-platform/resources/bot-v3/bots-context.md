---
title: Получение контекста для ленты
description: Сведения о том, как получить контекст для боты в Microsoft Teams
keywords: контекст Боты Teams
ms.date: 05/20/2019
ms.openlocfilehash: 8f054661664850ffb843714230e209c8e4737f0a
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796164"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="d7c6f-104">Получение контекста для ленты Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d7c6f-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d7c6f-105">Ваш робот может получить доступ к дополнительному контексту для команды или чата, например для профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="d7c6f-106">Эти сведения можно использовать, чтобы расширить функциональные возможности Bot и предоставить более персонализированный интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
> <span data-ttu-id="d7c6f-107">&ndash;Для этих специальных API-интерфейсов ленты Microsoft Teams можно получить доступ через свои расширения для пакета SDK для Bot Builder.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-107">These Microsoft Teams&ndash;specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span> <span data-ttu-id="d7c6f-108">Для C#/.нет Скачайте наш пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="d7c6f-108">For C#/.NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="d7c6f-109">Для Node.js разработки функция Ботбуилдер для Microsoft Teams встроена в [пакет SDK для Bot Framework](https://github.com/microsoft/botframework-sdk) версии 4.6.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-109">For Node.js development, the BotBuilder for Microsoft Teams functionality has been incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) as of v4.6.</span></span>

## <a name="fetching-the-team-roster"></a><span data-ttu-id="d7c6f-110">Получение списка команд</span><span class="sxs-lookup"><span data-stu-id="d7c6f-110">Fetching the team roster</span></span>

<span data-ttu-id="d7c6f-111">Ваш робот может запросить список участников группы и их базовые профили, в том числе идентификаторы пользователей Teams и Azure Active Directory (Azure AD), такие как Name и objectId.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-111">Your bot can query for the list of team members and their basic profiles, which includes Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="d7c6f-112">Эти сведения можно использовать для сопоставления удостоверений пользователей; Например, чтобы проверить, является ли пользователь, вошедший на вкладку с помощью учетных данных Azure AD, участником команды.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-112">You can use this information to correlate user identities; for example, to check whether a user logged into a tab through Azure AD credentials is a member of the team.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="d7c6f-113">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="d7c6f-113">REST API example</span></span>

<span data-ttu-id="d7c6f-114">Вы можете отправить запрос GET напрямую [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , используя значение в `serviceUrl` качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-114">You can directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="d7c6f-115">`teamId`Можно найти в `channeldata` объекте полезных данных действия, который получит ваш почтовый робот в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="d7c6f-115">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>
* <span data-ttu-id="d7c6f-116">Когда пользователь получает сообщения или взаимодействует с Bot в контексте команды (см. [Получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span><span class="sxs-lookup"><span data-stu-id="d7c6f-116">When a user messages or interacts with your bot in a team context (see [Receiving Messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span></span>
* <span data-ttu-id="d7c6f-117">Добавление нового пользователя или ленты в команду (см. [пользователь, добавленный в группу](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span><span class="sxs-lookup"><span data-stu-id="d7c6f-117">When a new user or bot is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span></span>

> [!NOTE]
>* <span data-ttu-id="d7c6f-118">Обязательно используйте идентификатор команды при вызове API</span><span class="sxs-lookup"><span data-stu-id="d7c6f-118">Make sure to use the team id when calling the api</span></span>
>* <span data-ttu-id="d7c6f-119">Значение " `serviceUrl` является стабильным, но может измениться".</span><span class="sxs-lookup"><span data-stu-id="d7c6f-119">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="d7c6f-120">Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="d7c6f-120">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="d7c6f-121">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="d7c6f-121">.NET example</span></span>

<span data-ttu-id="d7c6f-122">Call `GetConversationMembersAsync` using `Team.Id` для возврата списка идентификаторов пользователей.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-122">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejstypescript-example"></a><span data-ttu-id="d7c6f-123">Пример Node.js/Типескрипт</span><span class="sxs-lookup"><span data-stu-id="d7c6f-123">Node.js/TypeScript example</span></span>

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

<span data-ttu-id="d7c6f-124">В этой статье *также приведены* [примеры кода Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d7c6f-124">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="d7c6f-125">Получение профиля пользователя или списка в личном или группом чате</span><span class="sxs-lookup"><span data-stu-id="d7c6f-125">Fetching user profile or roster in personal or group chat</span></span>

<span data-ttu-id="d7c6f-126">Вы также можете выполнить один вызов API для любого личного чата, чтобы получить сведения о профиле пользователя в чате.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-126">You can also make the same API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="d7c6f-127">Вызовы API и методы SDK идентичны получению списка команд, как и объект Response.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-127">The API call and SDK methods are identical to fetching the team roster, as is the response object.</span></span> <span data-ttu-id="d7c6f-128">Единственное отличие заключается в том, что вместо него передается значение `conversationId` `teamId` .</span><span class="sxs-lookup"><span data-stu-id="d7c6f-128">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetching-the-list-of-channels-in-a-team"></a><span data-ttu-id="d7c6f-129">Получение списка каналов в команде</span><span class="sxs-lookup"><span data-stu-id="d7c6f-129">Fetching the list of channels in a team</span></span>

<span data-ttu-id="d7c6f-130">Ваш робот может запросить список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-130">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="d7c6f-131">По умолчанию возвращается имя общего канала, `null` позволяющее выполнять локализацию.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-131">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="d7c6f-132">Идентификатор канала для общего канала всегда соответствует ИДЕНТИФИКАТОРу группы.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-132">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="d7c6f-133">Пример API REST</span><span class="sxs-lookup"><span data-stu-id="d7c6f-133">REST API example</span></span>

<span data-ttu-id="d7c6f-134">Вы можете отправить запрос GET напрямую `/teams/{teamId}/conversations/` , используя значение в `serviceUrl` качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d7c6f-134">You can directly issue a GET request on `/teams/{teamId}/conversations/`, using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="d7c6f-135">Единственный источник `teamId` — это сообщение от контекста команды — либо сообщение от пользователя, либо сообщение, которое поступает от пользователя Bot при его добавлении в команду (см. [пользователь или пользователь, добавленный в команду](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span><span class="sxs-lookup"><span data-stu-id="d7c6f-135">The only source for `teamId` is a message from the team context - either a message from a user or the message that your bot receives when it is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span></span>

> [!NOTE]
> <span data-ttu-id="d7c6f-136">Значение " `serviceUrl` является стабильным, но может измениться".</span><span class="sxs-lookup"><span data-stu-id="d7c6f-136">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="d7c6f-137">Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="d7c6f-137">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="d7c6f-138">Пример .NET</span><span class="sxs-lookup"><span data-stu-id="d7c6f-138">.NET example</span></span>

<span data-ttu-id="d7c6f-139">В следующем примере используется `FetchChannelList` вызов из [расширений Microsoft Teams для пакета SDK построителя построителя для .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span><span class="sxs-lookup"><span data-stu-id="d7c6f-139">The following example uses the `FetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="d7c6f-140">Пример Node.js</span><span class="sxs-lookup"><span data-stu-id="d7c6f-140">Node.js example</span></span>

<span data-ttu-id="d7c6f-141">В следующем примере используется `fetchChannelList` вызов из [расширений Microsoft Teams для пакета SDK построителя для Node.js](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="d7c6f-141">The following example uses `fetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

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
