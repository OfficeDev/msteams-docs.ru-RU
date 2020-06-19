---
title: Получение контекста для ленты
description: Сведения о том, как получить контекст для боты в Microsoft Teams
keywords: контекст Боты Teams
ms.date: 05/20/2019
ms.openlocfilehash: 8f054661664850ffb843714230e209c8e4737f0a
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801228"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Получение контекста для ленты Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Ваш робот может получить доступ к дополнительному контексту для команды или чата, например для профиля пользователя. Эти сведения можно использовать, чтобы расширить функциональные возможности Bot и предоставить более персонализированный интерфейс.

> [!NOTE]
> &ndash;Для этих специальных API-интерфейсов ленты Microsoft Teams можно получить доступ через свои расширения для пакета SDK для Bot Builder. Для C#/.нет Скачайте наш пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) . Для Node.js разработки функция Ботбуилдер для Microsoft Teams встроена в [пакет SDK для Bot Framework](https://github.com/microsoft/botframework-sdk) версии 4.6.

## <a name="fetching-the-team-roster"></a>Получение списка команд

Ваш робот может запросить список участников группы и их базовые профили, в том числе идентификаторы пользователей Teams и Azure Active Directory (Azure AD), такие как Name и objectId. Эти сведения можно использовать для сопоставления удостоверений пользователей; Например, чтобы проверить, является ли пользователь, вошедший на вкладку с помощью учетных данных Azure AD, участником команды.

### <a name="rest-api-example"></a>Пример API REST

Вы можете отправить запрос GET напрямую [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , используя значение в `serviceUrl` качестве конечной точки.

`teamId`Можно найти в `channeldata` объекте полезных данных действия, который получит ваш почтовый робот в следующих сценариях:
* Когда пользователь получает сообщения или взаимодействует с Bot в контексте команды (см. [Получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))
* Добавление нового пользователя или ленты в команду (см. [пользователь, добавленный в группу](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))

> [!NOTE]
>* Обязательно используйте идентификатор команды при вызове API
>* Значение " `serviceUrl` является стабильным, но может измениться". Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl` .

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

Call `GetConversationMembersAsync` using `Team.Id` для возврата списка идентификаторов пользователей.

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

### <a name="nodejstypescript-example"></a>Пример Node.js/Типескрипт

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

В этой статье *также приведены* [примеры кода Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a>Получение профиля пользователя или списка в личном или группом чате

Вы также можете выполнить один вызов API для любого личного чата, чтобы получить сведения о профиле пользователя в чате.

Вызовы API и методы SDK идентичны получению списка команд, как и объект Response. Единственное отличие заключается в том, что вместо него передается значение `conversationId` `teamId` .

## <a name="fetching-the-list-of-channels-in-a-team"></a>Получение списка каналов в команде

Ваш робот может запросить список каналов в команде.

> [!NOTE]
>
>* По умолчанию возвращается имя общего канала, `null` позволяющее выполнять локализацию.
>* Идентификатор канала для общего канала всегда соответствует ИДЕНТИФИКАТОРу группы.

### <a name="rest-api-example"></a>Пример API REST

Вы можете отправить запрос GET напрямую `/teams/{teamId}/conversations/` , используя значение в `serviceUrl` качестве конечной точки.

Единственный источник `teamId` — это сообщение от контекста команды — либо сообщение от пользователя, либо сообщение, которое поступает от пользователя Bot при его добавлении в команду (см. [пользователь или пользователь, добавленный в команду](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).

> [!NOTE]
> Значение " `serviceUrl` является стабильным, но может измениться". Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl` .

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

В следующем примере используется `FetchChannelList` вызов из [расширений Microsoft Teams для пакета SDK построителя построителя для .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Пример Node.js

В следующем примере используется `fetchChannelList` вызов из [расширений Microsoft Teams для пакета SDK построителя для Node.js](https://www.npmjs.com/package/botbuilder-teams).

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
