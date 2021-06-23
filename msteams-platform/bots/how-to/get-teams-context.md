---
title: Получите Teams контекст для бота
author: surbhigupta
description: Как получить определенный контекст Microsoft Team для бота, включая список бесед, сведения и список каналов.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: ccbc04cbc1b2eb3162e886cd77273a4a0c37a6ec
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068975"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="d7558-103">Получите Teams контекст для бота</span><span class="sxs-lookup"><span data-stu-id="d7558-103">Get Teams specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="d7558-104">Бот может получить доступ к дополнительным данным контекста о группе или чате, где она установлена.</span><span class="sxs-lookup"><span data-stu-id="d7558-104">A bot can access additional context data about a team or chat where it is installed.</span></span> <span data-ttu-id="d7558-105">Эти сведения можно использовать для обогащения функциональных возможностей бота и предоставления более персонализированного опыта.</span><span class="sxs-lookup"><span data-stu-id="d7558-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetch-the-roster-or-user-profile"></a><span data-ttu-id="d7558-106">Извлечение реестра или профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="d7558-106">Fetch the roster or user profile</span></span>

<span data-ttu-id="d7558-107">Бот может запрашивать список участников и их базовые профили пользователей, включая Teams и сведения Azure Active Directory (AAD), такие как имя и objectId.</span><span class="sxs-lookup"><span data-stu-id="d7558-107">Your bot can query for the list of members and their basic user profiles, including Teams user IDs and Azure Active Directory (AAD) information, such as name and objectId.</span></span> <span data-ttu-id="d7558-108">Эти сведения можно использовать для сопоставления удостоверений пользователей.</span><span class="sxs-lookup"><span data-stu-id="d7558-108">You can use this information to correlate user identities.</span></span> <span data-ttu-id="d7558-109">Например, чтобы проверить, входит ли пользователь в вкладку с помощью учетных данных AAD, является членом группы.</span><span class="sxs-lookup"><span data-stu-id="d7558-109">For example, to check whether a user logged into a tab through AAD credentials, is a member of the team.</span></span> <span data-ttu-id="d7558-110">Для получения участников беседы минимальный или максимальный размер страницы зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="d7558-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="d7558-111">Размер страницы меньше 50, рассматриваются как 50 и более 500, имеют ограничения на уровне 500.</span><span class="sxs-lookup"><span data-stu-id="d7558-111">Page size less than 50, are treated as 50, and greater than 500, are capped at 500.</span></span> <span data-ttu-id="d7558-112">Даже если вы используете ненастоячивую версию, она ненадежна в больших группах и не должна использоваться.</span><span class="sxs-lookup"><span data-stu-id="d7558-112">Even if you use the non-paged version, it is unreliable in large teams and must not be used.</span></span> <span data-ttu-id="d7558-113">Дополнительные сведения см. [в Teams API-Teams для получения участников группы или чата.](~/resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="d7558-113">For more information, see [changes to Teams Bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="d7558-114">В следующем примере кода используется страница конечной точки для получения реестра:</span><span class="sxs-lookup"><span data-stu-id="d7558-114">The following sample code uses the paged endpoint for fetching the roster:</span></span>

# <a name="c"></a>[<span data-ttu-id="d7558-115">C#</span><span class="sxs-lookup"><span data-stu-id="d7558-115">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="d7558-116">TypeScript</span><span class="sxs-lookup"><span data-stu-id="d7558-116">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="d7558-117">Python</span><span class="sxs-lookup"><span data-stu-id="d7558-117">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="d7558-118">JSON</span><span class="sxs-lookup"><span data-stu-id="d7558-118">JSON</span></span>](#tab/json)

<span data-ttu-id="d7558-119">Вы можете напрямую выдавать запрос `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d7558-119">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="d7558-120">Значение является `serviceUrl` стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="d7558-120">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="d7558-121">По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="d7558-121">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="d7558-122">В ответной нагрузке также указывается, является ли пользователь регулярным или анонимным пользователем.</span><span class="sxs-lookup"><span data-stu-id="d7558-122">The response payload also indicates if the user is a regular or anonymous user.</span></span>

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

<span data-ttu-id="d7558-123">После получения реестра или профиля пользователя можно получить сведения об одном члене.</span><span class="sxs-lookup"><span data-stu-id="d7558-123">After you fetch the roster or user profile, you can get details of a single member.</span></span> <span data-ttu-id="d7558-124">В настоящее время для получения сведений для одного или более членов чата или группы используйте API Microsoft Teams бота для C# или `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API TypeScript.</span><span class="sxs-lookup"><span data-stu-id="d7558-124">Currently, to retrieve information for one or more members of a chat or team, use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript APIs.</span></span>

## <a name="get-single-member-details"></a><span data-ttu-id="d7558-125">Получить сведения об одном члене</span><span class="sxs-lookup"><span data-stu-id="d7558-125">Get single member details</span></span>

<span data-ttu-id="d7558-126">Вы также можете получить сведения о конкретном пользователе с помощью Teams, upN или AAD Object ID.</span><span class="sxs-lookup"><span data-stu-id="d7558-126">You can also retrieve the details of a particular user using their Teams user ID, UPN, or AAD Object ID.</span></span>

<span data-ttu-id="d7558-127">Для получения сведений об одном члене используется следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d7558-127">The following sample code is used to get single member details:</span></span>

# <a name="c"></a>[<span data-ttu-id="d7558-128">C#</span><span class="sxs-lookup"><span data-stu-id="d7558-128">C#</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="d7558-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="d7558-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="d7558-130">Python</span><span class="sxs-lookup"><span data-stu-id="d7558-130">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="d7558-131">JSON</span><span class="sxs-lookup"><span data-stu-id="d7558-131">JSON</span></span>](#tab/json)

<span data-ttu-id="d7558-132">Вы можете напрямую выдавать запрос `/v3/conversations/{conversationId}/members/{userId}` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d7558-132">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="d7558-133">Значение является `serviceUrl` стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="d7558-133">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="d7558-134">По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="d7558-134">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="d7558-135">Это может быть использовано для обычных пользователей и анонимных пользователей.</span><span class="sxs-lookup"><span data-stu-id="d7558-135">This can be used for regular users and anonymous users.</span></span>

<span data-ttu-id="d7558-136">Ниже приводится пример ответа для обычного пользователя:</span><span class="sxs-lookup"><span data-stu-id="d7558-136">The following is the response sample for regular user:</span></span>

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

<span data-ttu-id="d7558-137">Ниже приводится пример ответа для анонимного пользователя:</span><span class="sxs-lookup"><span data-stu-id="d7558-137">The following is the response sample for anonymous user:</span></span>

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

<span data-ttu-id="d7558-138">После получения сведений об одном члене вы можете получить сведения о команде.</span><span class="sxs-lookup"><span data-stu-id="d7558-138">After you get details of a single member, you can get details of the team.</span></span> <span data-ttu-id="d7558-139">В настоящее время для получения сведений для группы используйте API Microsoft Teams бота для C# или `TeamsInfo.GetMemberDetailsAsync` `TeamsInfo.getTeamDetails` typeScript.</span><span class="sxs-lookup"><span data-stu-id="d7558-139">Currently, to retrieve information for a team, use the Microsoft Teams bot APIs `TeamsInfo.GetMemberDetailsAsync` for C# or `TeamsInfo.getTeamDetails` for TypeScript.</span></span>

## <a name="get-teams-details"></a><span data-ttu-id="d7558-140">Сведения о команде</span><span class="sxs-lookup"><span data-stu-id="d7558-140">Get team's details</span></span>

<span data-ttu-id="d7558-141">При установке в команде бот может запрашивать метаданные о группе, включая ID группы AAD.</span><span class="sxs-lookup"><span data-stu-id="d7558-141">When installed in a team, your bot can query for metadata about that team including the AAD group ID.</span></span>

<span data-ttu-id="d7558-142">Для получения сведений о команде используется следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d7558-142">The following sample code is used to get team's details:</span></span>

# <a name="c"></a>[<span data-ttu-id="d7558-143">C#</span><span class="sxs-lookup"><span data-stu-id="d7558-143">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="d7558-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="d7558-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="d7558-145">Python</span><span class="sxs-lookup"><span data-stu-id="d7558-145">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="d7558-146">JSON</span><span class="sxs-lookup"><span data-stu-id="d7558-146">JSON</span></span>](#tab/json)

<span data-ttu-id="d7558-147">Вы можете напрямую выдавать запрос `/v3/teams/{teamId}` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d7558-147">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="d7558-148">Значение является `serviceUrl` стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="d7558-148">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="d7558-149">По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="d7558-149">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

<span data-ttu-id="d7558-150">После получения сведений о команде вы можете получить список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="d7558-150">After you get details of the team, you can get the list of channels in a team.</span></span> <span data-ttu-id="d7558-151">В настоящее время для получения сведений о списке каналов в группе используйте API Microsoft Teams для C# или `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` API TypeScript.</span><span class="sxs-lookup"><span data-stu-id="d7558-151">Currently, to retrieve information for a list of channels in a team, use the Microsoft Teams bot APIs `TeamsInfo.GetTeamChannelsAsync` for C# or `TeamsInfo.getTeamChannels` for TypeScript APIs.</span></span>

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="d7558-152">Получить список каналов в команде</span><span class="sxs-lookup"><span data-stu-id="d7558-152">Get the list of channels in a team</span></span>

<span data-ttu-id="d7558-153">Бот может запрашивать список каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="d7558-153">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
> * <span data-ttu-id="d7558-154">Для локализации возвращается имя общего канала по `null` умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d7558-154">The name of the default General channel is returned as `null` to allow for localization.</span></span>
> * <span data-ttu-id="d7558-155">ID канала для общего канала всегда совпадает с командным ИД.</span><span class="sxs-lookup"><span data-stu-id="d7558-155">The channel ID for the General channel always matches the team ID.</span></span>

<span data-ttu-id="d7558-156">Для получения списка каналов в команде используется следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="d7558-156">The following sample code is used to get the list of channels in a team:</span></span>

# <a name="c"></a>[<span data-ttu-id="d7558-157">C#</span><span class="sxs-lookup"><span data-stu-id="d7558-157">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="d7558-158">TypeScript</span><span class="sxs-lookup"><span data-stu-id="d7558-158">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="d7558-159">Python</span><span class="sxs-lookup"><span data-stu-id="d7558-159">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="d7558-160">JSON</span><span class="sxs-lookup"><span data-stu-id="d7558-160">JSON</span></span>](#tab/json)

<span data-ttu-id="d7558-161">Вы можете напрямую выдавать запрос `/v3/teams/{teamId}/conversations` GET, используя значение `serviceUrl` в качестве конечной точки.</span><span class="sxs-lookup"><span data-stu-id="d7558-161">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="d7558-162">Значение является `serviceUrl` стабильным, но может измениться.</span><span class="sxs-lookup"><span data-stu-id="d7558-162">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="d7558-163">По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl` для .</span><span class="sxs-lookup"><span data-stu-id="d7558-163">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

## <a name="next-step"></a><span data-ttu-id="d7558-164">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="d7558-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7558-165">Отправка и получение файлов через бот</span><span class="sxs-lookup"><span data-stu-id="d7558-165">Send and receive files through the bot</span></span>](~/bots/how-to/bots-filesv4.md)
