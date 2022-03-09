---
title: Получите Teams контекст для бота
author: surbhigupta
description: Как получить определенный контекст Microsoft Team для бота, включая список бесед, сведения о одном члене или команде, список каналов, примеры кода.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
keywords: список каналов профилей пользователей в контексте бота
ms.openlocfilehash: ee931be0d84dadf518ee35625c6339c7880eb4d2
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398598"
---
# <a name="get-teams-specific-context-for-your-bot"></a>Получите Teams контекст для бота

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Бот может получить доступ к дополнительным данным контекста о группе или чате, где она установлена. Эти сведения можно использовать для обогащения функциональных возможностей бота и предоставления более персонализированного опыта.

## <a name="fetch-the-roster-or-user-profile"></a>Извлечение реестра или профиля пользователя

Бот может запрашивать список участников и их базовые профили пользователей, включая Teams и сведения Microsoft Azure Active Directory (Azure AD), такие как имя и objectId. Эти сведения можно использовать для сопоставления удостоверений пользователей. Например, чтобы проверить, входит ли пользователь в вкладку с помощью учетных данных Azure AD, является членом группы. Для получения участников беседы минимальный или максимальный размер страницы зависит от реализации. Размер страницы меньше 50, рассматриваются как 50 и более 500, имеют ограничения на уровне 500. Даже если вы используете ненастоячивую версию, она ненадежна в больших группах и не должна использоваться. Дополнительные сведения см. [в Teams API-Teams для получения участников группы или чата](~/resources/team-chat-member-api-changes.md).

В следующем примере кода используется страница конечной точки для получения реестра:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(turnContext, 100, continuationToken);
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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[JSON](#tab/json)

Вы можете напрямую выдавать запрос GET, `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`используя значение в качестве `serviceUrl` конечной точки. Значение является стабильным `serviceUrl` , но может измениться. По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl`для . В ответной нагрузке также указывается, является ли пользователь регулярным или анонимным пользователем.

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

После получения реестра или профиля пользователя можно получить сведения об одном члене. В настоящее `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` время для получения сведений для одного или более членов чата или группы используйте API Microsoft Teams ботов для C# или API TypeScript.

## <a name="get-single-member-details"></a>Получить сведения об одном члене

Вы также можете получить сведения о конкретном пользователе с помощью Teams, upN или Azure AD Object ID.

Для получения сведений об одном члене используется следующий пример кода:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const member = await TeamsInfo.getMember(turnContext, encodeURI('someone@somecompany.com'));

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[JSON](#tab/json)

Вы можете напрямую выдавать запрос GET, `/v3/conversations/{conversationId}/members/{userId}`используя значение в качестве `serviceUrl` конечной точки. Значение является стабильным `serviceUrl` , но может измениться. По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl`для . Это может быть использовано для обычных пользователей и анонимных пользователей.

Ниже приводится пример ответа для обычного пользователя:

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

Ниже приводится пример ответа для анонимного пользователя:

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

После получения сведений об одном члене вы можете получить сведения о команде. В настоящее время `TeamsInfo.GetMemberDetailsAsync` `TeamsInfo.getTeamDetails` для получения сведений для группы используйте API Microsoft Teams бота для C# или typeScript.

## <a name="get-teams-details"></a>Сведения о команде

При установке в команде бот может запрашивать метаданные об этой группе, включая ID группы Azure AD.

Для получения сведений о команде используется следующий пример кода:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

Вы можете напрямую выдавать запрос GET, `/v3/teams/{teamId}`используя значение в качестве `serviceUrl` конечной точки. Значение является стабильным `serviceUrl` , но может измениться. По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl`для .

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

После получения сведений о команде вы можете получить список каналов в команде. В настоящее `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` время для получения сведений о списке каналов в группе используйте API Microsoft Teams для C# или API TypeScript.

## <a name="get-the-list-of-channels-in-a-team"></a>Получить список каналов в команде

Бот может запрашивать список каналов в команде.

> [!NOTE]
>
> * Для локализации `null` возвращается имя общего канала по умолчанию.
> * ID канала для общего канала всегда совпадает с командным ИД.

Для получения списка каналов в команде используется следующий пример кода:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

Вы можете напрямую выдавать запрос GET, `/v3/teams/{teamId}/conversations`используя значение в качестве `serviceUrl` конечной точки. Значение является стабильным `serviceUrl` , но может измениться. По прибытии нового сообщения бот должен проверить его сохраненное значение `serviceUrl`для .

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

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Отправка и получение файлов через бот](~/bots/how-to/bots-filesv4.md)
