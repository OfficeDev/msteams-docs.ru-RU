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
# <a name="get-context-for-your-microsoft-teams-bot"></a>Получите контекст для Microsoft Teams бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Ваш бот может получить доступ к дополнительному контексту о команде или чате, например к профиле пользователя. Эти сведения можно использовать для обогащения функциональных возможностей бота и предоставления более персонализированного опыта.

> [!NOTE]
>
> * Microsoft Teams API бота лучше всего получать через наши расширения для SDK-конструктора ботов.
> * Для C# или .NET скачайте пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.
> * Для Node.js разработки функциональность bot Builder для Teams включена в [SDK bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>Извлечение реестра команды

Бот может запрашивать список членов группы и их основные профили. Основные профили включают Teams и Azure Active Directory (AAD), такие как имя и ID объекта. Эти сведения можно использовать для сопоставления удостоверений пользователей. Например, проверьте, входит ли пользователь в вкладку с помощью учетных данных AAD.

### <a name="rest-api-example"></a>Пример API REST

Непосредственно выдай запрос [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) GET, используя `serviceUrl` значение в качестве конечной точки.

Объект можно найти в объекте полезной нагрузки, получаемой ботом в `teamId` `channeldata` следующих сценариях:

* Когда пользователь передает сообщения или взаимодействует с ботом в контексте группы. Дополнительные сведения см. [в сообщении о получении сообщений.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)
* При добавлении нового пользователя или бота в команду. Дополнительные сведения см. в [записи бота или пользователя, добавленного в команду.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)

> [!NOTE]
>
>* Всегда используйте командный ID при вызове API.
>* Значение `serviceUrl` имеет тенденцию быть стабильным, но может измениться. По прибытии нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.

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

Вызов `GetConversationMembersAsync` с помощью возврата списка `Team.Id` пользовательских ИД.

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

### <a name="nodejs-or-typescript-example"></a>Node.js или typeScript

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Извлечение профиля пользователя или реестра в личном или групповом чате

Вы можете сделать вызов API для любого личного чата, чтобы получить сведения о профиле пользователя в чате с ботом.

Вызов API, методы SDK и объект ответа идентичны запросу реестра группы. Единственное отличие состоит в том, что вы передаете вместо `conversationId` `teamId` .

## <a name="fetch-the-list-of-channels-in-a-team"></a>Извлечение списка каналов в команде

Бот может запрашивать список каналов в команде.

> [!NOTE]
>
>* Для локализации возвращается имя общего канала по `null` умолчанию.
>* ID канала для общего канала всегда совпадает с командным ИД.

### <a name="rest-api-example"></a>Пример API REST

Непосредственно выдай запрос `/teams/{teamId}/conversations/` GET, используя `serviceUrl` значение в качестве конечной точки.

Единственным источником для `teamId` этого является сообщение из контекста группы. Это сообщение является либо сообщением от пользователя, либо сообщением, которое получает бот при добавлении в команду. Дополнительные сведения см. в [записи бота или пользователя, добавленного в команду.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)

> [!NOTE]
> Значение `serviceUrl` имеет тенденцию быть стабильным, но может измениться. По прибытии нового сообщения бот должен проверить его сохраненное `serviceUrl` значение.

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

В следующем примере используется вызов из расширений Teams для `FetchChannelList` [SDK bot Builder для .NET:](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js пример

В следующем примере используется вызов из расширений Teams для `fetchChannelList` [SDK ](https://www.npmjs.com/package/botbuilder-teams)bot Builder для Node.js:

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

## <a name="get-clientinfo-in-your-bot-context"></a>Получите clientInfo в контексте бота

Вы можете получить clientInfo в действии вашего бота. ClientInfo содержит следующие свойства:

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

## <a name="see-also"></a>См. также

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).