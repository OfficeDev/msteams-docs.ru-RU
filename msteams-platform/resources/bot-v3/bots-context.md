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
# <a name="get-context-for-your-microsoft-teams-bot"></a>Получите контекст для бота Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Бот может получить доступ к дополнительному контексту команды или чата, например к профилю пользователя. Эти сведения можно использовать для того, чтобы расширить функциональные возможности бота и обеспечить более персонализированное впечатление.

> [!NOTE]
>
> * Доступ к API ботов для Microsoft Teams лучше всего получить с помощью наших расширений для SDK построитель ботов.
> * Для C# или .NET скачайте пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.
> * Для Node.js разработки функции построитель ботов для Teams включены в [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) 4.6.

## <a name="fetch-the-team-roster"></a>Получить список команд

Бот может запрашивать список участников команды и их базовые профили. Основные профили включают в себя ИД пользователей Teams и данные Azure Active Directory (AAD), такие как имя и ид объекта. Эти сведения можно использовать для сопоставления удостоверений пользователей. Например, проверьте, является ли пользователь, во время входа на вкладку с помощью учетных данных AAD, участником группы.

### <a name="rest-api-example"></a>Пример API REST

Напрямую выдают запрос [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) GET, используя `serviceUrl` значение в качестве конечной точки.

Его можно найти в объекте полезной нагрузки действия, получаемой ботом в `teamId` `channeldata` следующих сценариях:

* Когда пользователь сообщает или взаимодействует с ботом в контексте команды. Дополнительные сведения [см. в получении сообщений.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)
* При добавлении нового пользователя или бота в команду. Дополнительные сведения см. в [добавлении бота](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)или пользователя в команду.

> [!NOTE]
>
>* Всегда используйте ИД команды при вызове API.
>* Значение `serviceUrl` обычно является стабильным, но может изменяться. После поступления нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.

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

### <a name="net-example"></a>Пример .NET

Вызов, `GetConversationMembersAsync` который используется для возврата списка `Team.Id` пользовательских ИД.

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

### <a name="nodejs-or-typescript-example"></a>Node.js или TypeScript

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

См. также примеры [Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Извлечение профиля пользователя или группы в личном или групповом чате

Вы можете сделать вызов API для любого личного чата, чтобы получить сведения профиля пользователя, который общается с ботом.

ВызовЫ API, методы SDK и объект ответа идентичны запросу в составе команды. Единственное отличие заключается в том, что вы `conversationId` передаете вместо `teamId` .

## <a name="fetch-the-list-of-channels-in-a-team"></a>Получить список каналов в команде

Бот может запросить список каналов в команде.

> [!NOTE]
>
>* Возвращается имя общего канала по умолчанию для `null` локализации.
>* ИД канала для общего канала всегда совпадает с ИД команды.

### <a name="rest-api-example"></a>Пример API REST

Напрямую выдают запрос `/teams/{teamId}/conversations/` GET, используя `serviceUrl` значение в качестве конечной точки.

Единственным источником является `teamId` сообщение из контекста команды. Это либо сообщение от пользователя, либо сообщение, которое бот получает при добавлении в команду. Дополнительные сведения см. в [добавлении бота](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)или пользователя в команду.

> [!NOTE]
> Значение `serviceUrl` обычно является стабильным, но может изменяться. После поступления нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.

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

#### <a name="net-example"></a>Пример .NET

В следующем примере используется вызов из расширений Teams для `FetchChannelList` [SDK построитель ботов для .NET:](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js примере

В следующем примере используется вызов из расширений Teams для `fetchChannelList` [SDK построитель ботов для Node.js: ](https://www.npmjs.com/package/botbuilder-teams)

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

## <a name="get-clientinfo-in-your-bot-context"></a>Получить clientInfo в контексте бота

Вы можете получить clientInfo в действии бота. ClientInfo содержит следующие свойства:

* Locale
* Страна
* Платформа
* Timezone

### <a name="json-example"></a>Пример JSON

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

### <a name="c-example"></a>Пример C#

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```