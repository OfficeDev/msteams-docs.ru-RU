---
title: Получение контекста для Microsoft Teams бота
description: В этом модуле вы узнаете, как получить контекст для ботов в Microsoft Teams, получить список команд и профиль пользователя или список в личном или групповом чате.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 3fd75e063f9b12c09bc4dded167bd8cdaead6b7a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143118"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Получение контекста для Microsoft Teams бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Бот может получить доступ к дополнительному контексту о команде или чате, например к профилю пользователя. Эти сведения можно использовать для обогащения функциональности бота и обеспечения более персонализированного взаимодействия.

> [!NOTE]
>
> * Microsoft Teams API ботов лучше всего получить через наши расширения для пакета SDK Bot Builder.
> * Для C# или .NET скачайте наш [пакет Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.
> * Для Node.js разработки функция Bot Builder для Teams включена в пакет [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) версии 4.6.

## <a name="fetch-the-team-roster"></a>Получение сведений о списке команд

Бот может запрашивать список участников команды и их базовые профили. Основные профили включают Teams идентификаторы пользователей и Microsoft Azure Active Directory (Azure AD), такие как имя и идентификатор объекта. Эти сведения можно использовать для сопоставления удостоверений пользователей. Например, проверьте, входит ли пользователь на вкладку с помощью учетных данных Microsoft Azure Active Directory (Azure AD) является членом команды.

### <a name="rest-api-example"></a>Пример REST API

Напрямую выполните запрос [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)GET, используя значение `serviceUrl` в качестве конечной точки.

Его `teamId` можно найти в объекте `channeldata` полезных данных действия, которые бот получает в следующих сценариях:

* Когда пользователь отправляет сообщения или взаимодействует с ботом в контексте команды. Дополнительные сведения см [. в статье о получении сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).
* При добавлении нового пользователя или бота в команду. Дополнительные сведения см. в [описании бота или пользователя, добавленного в команду](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).

> [!NOTE]
>
>* Всегда используйте идентификатор команды при вызове API.
>* Значение `serviceUrl` , как правило, стабильное, но может измениться. Когда приходит новое сообщение, бот должен проверить его сохраненное `serviceUrl` значение.

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

Вызов `GetConversationMembersAsync` с `Team.Id` помощью функции возврата списка идентификаторов пользователей.

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Получение профиля пользователя или списков в личном или групповом чате

Вы можете выполнить вызов API для любого личного чата, чтобы получить сведения о профиле пользователя, который общался с ботом.

Вызов API, методы пакета SDK и объект ответа идентичны выборке списков команд. Единственным отличием является то, что вы передаете `conversationId` вместо `teamId`.

## <a name="fetch-the-list-of-channels-in-a-team"></a>Получение списка каналов в команде

Бот может запрашивать список каналов в команде.

> [!NOTE]
>
>* Имя общего канала по умолчанию возвращается в качестве `null`, чтобы разрешить локализацию.
>* Идентификатор канала для общего канала всегда совпадает с идентификатором команды.

### <a name="rest-api-example"></a>Пример REST API

Напрямую выполните запрос `/teams/{teamId}/conversations/`GET, используя значение `serviceUrl` в качестве конечной точки.

Единственным источником является `teamId` сообщение из контекста команды. Это сообщение от пользователя или сообщение, которое бот получает при добавлении в команду. Дополнительные сведения см. в [описании бота или пользователя, добавленного в команду](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).

> [!NOTE]
> Значение `serviceUrl` , как правило, стабильное, но может измениться. Когда приходит новое сообщение, бот должен проверить его сохраненное `serviceUrl` значение.

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

В следующем примере используется `FetchChannelList` вызов из [расширений Teams для пакета SDK Bot Builder для .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Пример Node.js

В следующем примере `fetchChannelList` используется вызов из [расширений Teams для пакета SDK Bot Builder для Node.js](https://www.npmjs.com/package/botbuilder-teams):

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

## <a name="get-clientinfo-in-your-bot-context"></a>Получение clientInfo в контексте бота

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

### <a name="c-example"></a>C# пример

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a>Дополнительные ресурсы

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
