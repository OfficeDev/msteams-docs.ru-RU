---
title: Обработка событий Bot
description: Описание способов обработки событий в боты для Microsoft Teams
keywords: события Боты Teams
ms.date: 05/20/2019
ms.openlocfilehash: 06da5e6b0668e86012d87af3184493cdeb70aecd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675470"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Обработка событий Bot в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams отправляет уведомления для почтового робота для изменений или событий, происходящих в областях действия ленты. Вы можете использовать эти события для активации логики службы, например:

* Инициация приветственного сообщения при добавлении ленты в группу
* Сведения о группах запросов и кэш-памяти при добавлении ленты в групповой чат
* Обновление кэшированных сведений о членстве в группе или о канале
* Удаление кэшированных данных для команды при удалении ленты.
* Когда пользователю понравится сообщение Bot

Каждое событие Bot передается в `Activity` виде объекта, `messageType` в котором определяется, какая информация находится в объекте. Сообщения типа `message`messages можно просмотреть в разделе [Отправка и получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md).

События Teams и Group, обычно активируемые для `conversationUpdate` типа, имеют дополнительные сведения о событиях Teams, передаваемые `channelData` в рамках объекта, и поэтому обработчик события должен запросить `channelData` полезные данные для Teams `eventType` и дополнительные метаданные, связанные с событиями.

В следующей таблице перечислены события, которые могут получать и предпринимать действия от пользователя Bot.

|Тип|Объект полезных данных|Тип события Teams |Описание|Область|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Участник, добавленный в группу](#team-member-or-bot-addition)| ко |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Участник удален из группы](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [Команда была переименована](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Создан канал](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Канал переименован](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Канал удален](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Реакция на сообщение Bot](#reactions)| ко |
| `messageReaction` |`reactionsRemoved`|| [Реакция, удаленная из сообщения Bot](#reactions)| ко |

## <a name="team-member-or-bot-addition"></a>Добавление участников группы или ленты

[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) Событие отправляется в Bot при получении сведений об обновлениях членства для Teams, где она была добавлена. Он также получает обновление, когда оно добавляется в первый раз специально для личных бесед. Обратите внимание, что сведения`Id`о пользователе () уникальны для почтового робота, и их можно кэшировать для будущего использования службой (например, для отправки сообщения определенному пользователю).

### <a name="bot-or-user-added-to-a-team"></a>Bot или пользователь, добавленный в команду

`conversationUpdate` Событие с `membersAdded` объектом в полезных данных отправляется при добавлении в команду ленты или нового пользователя в группу, в которую добавлен Bot. Microsoft Teams также `eventType.teamMemberAdded` добавляет в `channelData` объект.

Так как это событие отправляется в обоих случаях, необходимо выполнить анализ `membersAdded` объекта, чтобы определить, был ли добавлен пользователь или сам робот. В последнююмся случае рекомендуется отправить [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) на канал, чтобы пользователи могли ознакомиться с функциями, которые предоставляет ваш почтовый робот.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Пример кода: Проверка того, был ли элемент Bot добавлен.

##### <a name="net"></a>.NET

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a>Node.js

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a>Пример схемы: Bot добавлен в группу

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="bot-added-for-personal-context-only"></a>Добавление ленты только для личного контекста

Пользователь Bot получает сведения `conversationUpdate` о `membersAdded` том, когда пользователь добавляет его непосредственно для личного чата. В этом случае полезные данные, получаемые от botа, не `channelData.team` содержат объект. Вы должны использовать этот фильтр в том случае, если вы хотите, чтобы ваш Bot предлагал другое [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) в зависимости от области действия.

> [!NOTE]
> Для личной области Боты ваш робот будет получать `conversationUpdate` событие только один раз, даже при удалении и повторном добавлении ленты. Для разработки и тестирования может потребоваться добавить вспомогательную функцию, которая позволит полностью сбросить объект Bot. Для получения дополнительных сведений о реализации этого [примера, например, Node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) или [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) .

#### <a name="schema-example-bot-added-to-personal-context"></a>Пример схемы: Bot добавлен в личный контекст

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

## <a name="team-member-or-bot-removed"></a>Участник группы или Bot удален

`conversationUpdate` Событие с `membersRemoved` объектом в полезных данных отправляется при удалении ленты из команды или при удалении пользователя из группы, в которую добавлен Bot. Microsoft Teams также `eventType.teamMemberRemoved` добавляет в `channelData` объект. Как и в `membersAdded` случае с объектом, необходимо проанализировать `membersRemoved` объект для идентификатора приложения Bot, чтобы определить, кто был удален.

### <a name="schema-example-team-member-removed"></a>Пример схемы: удален участник группы

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="team-name-updates"></a>Обновления имени команды

> [!NOTE]
> Не существует функции для запроса всех имен команд, а имя команды не возвращается в полезных данных из других событий.

Ваш робот получает уведомление, когда группа, в которую она находится, была переименована. Он получает `conversationUpdate` событие `eventType.teamRenamed` в `channelData` объекте. Обратите внимание, что уведомления о создании или удалении команды не отображаются, так как боты существует только в составе Teams и не отображается за пределами области, в которой они были добавлены.

### <a name="schema-example-team-renamed"></a>Пример схемы: команда переименована

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="channel-updates"></a>Обновления канала

Ваш робот получает уведомление о создании, переименовании или удалении канала в группе, в которой он был добавлен. Опять же, `conversationUpdate` получается событие, а идентификатор события, зависящий от Teams, отправляется в `channelData.eventType` составе объекта, где данные канала `channel.id` являются идентификатором GUID канала, и `channel.name` содержит само имя канала.

Ниже приведены события канала.

* **чаннелкреатед**&emsp;пользователь добавляет новый канал в команду.
* **чаннелренамед**&emsp;пользователь переименовывает существующий канал
* **чаннелделетед**&emsp;пользователь удаляет канал

### <a name="full-schema-example-channelcreated"></a>Пример полной схемы: Чаннелкреатед

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Фрагмент схемы: Чаннелдата для Чаннелренамед

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelRenamed",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Фрагмент схемы: Чаннелдата для Чаннелделетед

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelDeleted",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

## <a name="reactions"></a>Реакция

`messageReaction` Событие отправляется, когда пользователь добавляет или удаляет его реакцию на сообщение, которое изначально было отправлено с помощью робота. `replyToId`содержит идентификатор определенного сообщения.

### <a name="schema-example-a-user-likes-a-message"></a>Пример схемы: пользователю нравится сообщение

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a>Пример схемы: пользователю не нравится сообщение

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```
