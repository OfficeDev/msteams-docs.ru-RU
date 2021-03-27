---
title: Получите определенный контекст team для бота
author: laujan
description: Как получить определенный контекст Microsoft Team для бота, включая список бесед, сведения и список каналов.
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: dfbf5e1638a2397492714b1e1945721450428d63
ms.sourcegitcommit: 0206ed48c6a287d14aec3739540194a91766f0a3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2021
ms.locfileid: "51378338"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="f8bfe-103">Получите определенный контекст team для бота</span><span class="sxs-lookup"><span data-stu-id="f8bfe-103">Get Team's specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="f8bfe-104">Бот может получить доступ к дополнительным данным контекста о установленной команде или чате.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-104">A bot can access additional context data about a team or chat it is installed in.</span></span> <span data-ttu-id="f8bfe-105">Эти сведения можно использовать для обогащения функциональных возможностей бота и предоставления более персонализированного опыта.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetching-the-roster-or-user-profile"></a><span data-ttu-id="f8bfe-106">Извлечение реестра или профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="f8bfe-106">Fetching the roster or user profile</span></span>

<span data-ttu-id="f8bfe-107">Бот может запрашивать список участников и их основные профили, включая ID пользователей Teams и сведения Azure Active Directory (Azure AD), такие как имя и objectId.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-107">Your bot can query for the list of members and their basic profiles, including Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="f8bfe-108">Эти сведения можно использовать для сопоставления удостоверений пользователей, например для проверки того, является ли пользователь, воехав на вкладку с помощью учетных данных Azure AD, членом группы.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-108">You can use this information to correlate user identities, e.g., to check whether a user, logged into a tab through Azure AD credentials, is a member of the team.</span></span> <span data-ttu-id="f8bfe-109">В приведенном ниже примере кода используется страница конечной точки для ирисовки реестра.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-109">The sample code below uses the paged endpoint for retrieving the roster.</span></span> <span data-ttu-id="f8bfe-110">Для получения участников беседы минимальный или максимальный размер страницы зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="f8bfe-111">Размер страницы меньше 50, рассматриваются как 50, а размер страницы больше 500.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-111">Page size less than 50, are treated as 50, and page size greater than 500, are capped at 500.</span></span> <span data-ttu-id="f8bfe-112">Несмотря на то, что вы по-прежнему можете использовать нестандартную версию, она будет ненадежной в больших группах и не должна использоваться.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-112">Although you may still use the non-paged version, it will be unreliable in large teams and should not be used.</span></span> <span data-ttu-id="f8bfe-113">*Дополнительные* [сведения см. в дополнительных](~/resources/team-chat-member-api-changes.md) сведениях об изменениях API bot teams для получения команд или участников чата.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-113">*See* [Changes to Teams Bot APIs for Fetching Team/Chat Members](~/resources/team-chat-member-api-changes.md) for additional information.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f8bfe-114">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f8bfe-114">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var members = new List<TeamsChannelAccount>();
        string continuationToken = null;

        do
        {
            var currentPage = await TeamsInfo.GetPagedMembersAsync(turnContext, 100, continuationToken, cancellationToken);
            continuationToken = currentPage.ContinuationToken;
            members.AddRange(currentPage.Members);
         }
         while (continuationToken != null);
     }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f8bfe-115">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f8bfe-115">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(context, 100, continuationToken);
                continuationToken = pagedMembers.continuationToken;
                members.push(...pagedMembers.members);
            }
            while(continuationToken !== undefined)

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="f8bfe-116">Python</span><span class="sxs-lookup"><span data-stu-id="f8bfe-116">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="f8bfe-117">JSON</span><span class="sxs-lookup"><span data-stu-id="f8bfe-117">JSON</span></span>](#tab/json)

<span data-ttu-id="f8bfe-118">Вы можете напрямую выдавать запрос `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-118">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="f8bfe-119">Значение имеет `serviceUrl` тенденцию быть стабильным, но может изменяться.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-119">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="f8bfe-120">Когда появится новое сообщение, бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="f8bfe-120">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="f8bfe-121">В ответной нагрузке также будет указано, является ли пользователь регулярным или анонимным пользователем.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-121">The response payload will also indicate if the user is a regular or anonymous user.</span></span>

```http
GET /v3/conversations/19:meeting_N2QzYTA3YmItYmMwOC00OTJmLThkYzMtZWMzZGU0NGIyZGI0@thread.v2/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
   "continuationToken":"asdfqwerueiqpiewr",
   "members":[
      {
         "id":"29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
         "name":"Anon1 (Guest)",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"anonymous"
      },
      {
         "id":"29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
         "objectId":"76b0b09f-d410-48fd-993e-84da521a597b",
         "givenName":"John",
         "surname":"Patterson",
         "email":"johnp@fabrikam.com",
         "userPrincipalName":"johnp@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      },
      {
         "id":"29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
         "objectId":"6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
         "givenName":"Rick",
         "surname":"Stevens",
         "email":"Rick.Stevens@fabrikam.com",
         "userPrincipalName":"rstevens@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      }
   ]
}
```

* * *

## <a name="get-single-member-details"></a><span data-ttu-id="f8bfe-122">Получить сведения об одном члене</span><span class="sxs-lookup"><span data-stu-id="f8bfe-122">Get single member details</span></span>

<span data-ttu-id="f8bfe-123">Вы также можете получить сведения о конкретном пользователе с помощью их ID пользователя Teams, UPN или AAD Object Id.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-123">You can also retrieve the details of a particular user using their Teams user Id, UPN, or AAD Object Id.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f8bfe-124">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f8bfe-124">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f8bfe-125">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f8bfe-125">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        const member = await TeamsInfo.getMember(context, encodeURI('someone@somecompany.com'));

        // By calling next() you ensure that the next BotHandler is run.
        await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="f8bfe-126">Python</span><span class="sxs-lookup"><span data-stu-id="f8bfe-126">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="f8bfe-127">JSON</span><span class="sxs-lookup"><span data-stu-id="f8bfe-127">JSON</span></span>](#tab/json)

<span data-ttu-id="f8bfe-128">Вы можете напрямую выдавать запрос `/v3/conversations/{conversationId}/members/{userId}` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-128">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="f8bfe-129">Значение имеет `serviceUrl` тенденцию быть стабильным, но может изменяться.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-129">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="f8bfe-130">Когда появится новое сообщение, бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="f8bfe-130">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="f8bfe-131">Это может быть использовано для обычных пользователей и анонимных пользователей.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-131">This can be used for regular users and anonymous users.</span></span>

<span data-ttu-id="f8bfe-132">Ниже приведен пример ответа для обычного пользователя</span><span class="sxs-lookup"><span data-stu-id="f8bfe-132">Below is a response sample for regular user</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"user"
}
```

<span data-ttu-id="f8bfe-133">Ниже приведен ответ для анонимного пользователя</span><span class="sxs-lookup"><span data-stu-id="f8bfe-133">Below is response for anonymous user</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/<anonymous user id>"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"anonymous"
}
```

* * *

## <a name="get-teams-details"></a><span data-ttu-id="f8bfe-134">Сведения о команде</span><span class="sxs-lookup"><span data-stu-id="f8bfe-134">Get team's details</span></span>

<span data-ttu-id="f8bfe-135">При установке в команде бот может запрашивать метаданные об этой группе, включая группу Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-135">When installed in a team, your bot can query for metadata about that team including the Azure AD groupId.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f8bfe-136">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f8bfe-136">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        TeamDetails teamDetails = await TeamsInfo.GetTeamDetailsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);
        if (teamDetails != null) {
            await turnContext.SendActivityAsync($"The groupId is: {teamDetails.AadGroupId}");
        }
        else {
            await turnContext.SendActivityAsync($"Message did not come from a channel in a team.");
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f8bfe-137">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f8bfe-137">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const teamDetails = await TeamsInfo.getTeamDetails(turnContext);
            if (teamDetails) {
                await turnContext.sendActivity(`The group ID is: ${teamDetails.aadGroupId}`);
            } else {
                await turnContext.sendActivity('This message did not come from a channel in a team.');
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="f8bfe-138">Python</span><span class="sxs-lookup"><span data-stu-id="f8bfe-138">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="f8bfe-139">JSON</span><span class="sxs-lookup"><span data-stu-id="f8bfe-139">JSON</span></span>](#tab/json)

<span data-ttu-id="f8bfe-140">Вы можете напрямую выдавать запрос `/v3/teams/{teamId}` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-140">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="f8bfe-141">Значение имеет `serviceUrl` тенденцию быть стабильным, но может изменяться.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-141">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="f8bfe-142">Когда появится новое сообщение, бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="f8bfe-142">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

* * *

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="f8bfe-143">Получить список каналов в команде</span><span class="sxs-lookup"><span data-stu-id="f8bfe-143">Get the list of channels in a team</span></span>

<span data-ttu-id="f8bfe-144">Бот может запрашивать список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-144">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="f8bfe-145">Для локализации возвращается имя общего канала по `null` умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-145">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="f8bfe-146">ID канала для общего канала всегда совпадает с командным ИД.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-146">The channel ID for the General channel always matches the team ID.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f8bfe-147">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f8bfe-147">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<ChannelInfo> channels = await TeamsInfo.GetTeamChannelsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);

        await turnContext.SendActivityAsync($"The channel count is: {channels.Count()}");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f8bfe-148">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f8bfe-148">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const channels = await TeamsInfo.getTeamChannels(turnContext);

            await turnContext.sendActivity(`The channel count is: ${channels.length}`);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="f8bfe-149">Python</span><span class="sxs-lookup"><span data-stu-id="f8bfe-149">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="f8bfe-150">JSON</span><span class="sxs-lookup"><span data-stu-id="f8bfe-150">JSON</span></span>](#tab/json)

<span data-ttu-id="f8bfe-151">Вы можете напрямую выдавать запрос `/v3/teams/{teamId}/conversations` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-151">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="f8bfe-152">Значение имеет `serviceUrl` тенденцию быть стабильным, но может изменяться.</span><span class="sxs-lookup"><span data-stu-id="f8bfe-152">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="f8bfe-153">Когда появится новое сообщение, бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="f8bfe-153">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
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

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
