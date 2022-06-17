---
title: Обработка событий бота
description: В этом модуле вы узнаете, как обрабатывать события в ботах для Microsoft Teams, Teams участника или бота, удаленного участника команды или бота и т. д.
ms.date: 05/20/2019
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 30ccb4ee8810154e2b36311d15217205de87b413
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142761"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Обработка событий бота в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams отправляет вашему боту уведомления об изменениях или событиях в тех областях, где этот бот активен. Эти события можно использовать для активации логики службы, например:

* Отправка приветственного сообщения при добавлении бота в команду.
* Запрос и кэширование сведений о группе при добавлении бота в групповой чат.
* Обновление кэшированных сведений об участии в команде или сведений о канале.
* Удаление кэшированных сведений для команды, если бот удален.
* Когда пользователь ставит сообщению бота отметку "Нравится".

Каждое событие бота отправляется в виде объекта `Activity`, в котором `messageType` определяет, какие сведения содержатся в объекте. Сведения о сообщениях типа `message` см. в статье [Отправка и получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Teams события и события группы, `conversationUpdate` активированные вне типа, содержат больше сведений о `channelData` событиях Teams, передаваемых как часть объекта, `channelData` `eventType` и поэтому обработчик событий должен запросить полезные данные для Teams и метаданных, связанных с событиями.

В следующей таблице перечислены события, которые бот может получать и с которыми может выполнять действия.

|Тип|Объект полезных данных|Teams eventType |Описание|Область|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Участник добавлен в команду](#team-member-or-bot-addition)| все |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Участник удален из команды](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [Команда переименована](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Канал создан](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Канал переименован](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Канал удален](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Реакция на сообщение бота](#reactions)| все |
| `messageReaction` |`reactionsRemoved`|| [Реакция удалена из сообщения бота](#reactions)| все |

## <a name="team-member-or-bot-addition"></a>Добавление участника команды или бота

Событие [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) отправляется боту, когда он получает сведения об обновлении участия в командах, куда он добавлен. Бот также получает обновление при первом добавлении в личную беседу. Сведения о пользователе (`Id`) уникальны для вашего бота и могут быть кэшироваться для дальнейшего использования службой, например отправки сообщения конкретному пользователю.

### <a name="bot-or-user-added-to-a-team"></a>Бот или пользователь добавлен в команду

Событие `conversationUpdate` с объектом `membersAdded` в полезных данных отправляется при добавлении бота в команду или при добавлении нового пользователя в команду, в которую был добавлен бот. Microsoft Teams также добавляет `eventType.teamMemberAdded` в объект `channelData`.

Так как это событие отправляется в обоих случаях, необходимо проанализировать объект `membersAdded`, чтобы определить, добавляется ли пользователь или бот. В последнем случае рекомендуется отправить [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) в канал, чтобы пользователи могли понять функции, которые предоставляет ваш бот.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Пример кода: проверка того, является ли бот добавленным участником

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

#### <a name="schema-example-bot-added-to-team"></a>Пример схемы: бот добавлен в команду

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a>Пользователь добавлен в собрание

Событие `conversationUpdate` с объектом `membersAdded` в полезных данных отправляется при добавлении пользователя в закрытое запланированное собрание. Сведения о событии отправляются даже при присоединении анонимных пользователей к собранию.

> [!NOTE]
>
>* При добавлении анонимного пользователя в собрание объект полезных данных membersAdded не содержит поле `aadObjectId`.
>* При добавлении анонимного пользователя в собрание объект `from` в полезных данных всегда содержит идентификатор организатора собрания, даже если анонимный пользователь был добавлен другим выступающим.

#### <a name="schema-example-user-added-to-meeting"></a>Пример схемы: пользователь добавлен в собрание

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a>Бот добавлен только для личного контекста

Бот получает `conversationUpdate` с `membersAdded`, когда пользователь добавляет его непосредственно для личного чата. В этом случае полезные данные, получаемые ботом, не содержат объект `channelData.team`. Это следует использовать в качестве фильтра, если вы хотите, чтобы ваш бот предлагал другое [приветственное сообщение](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) в зависимости от области.

> [!NOTE]
> Для личной области ваш бот будет получать событие `conversationUpdate` несколько раз, даже если бот удален и добавлен повторно. Для разработки и тестирования может оказаться полезным добавить вспомогательную функцию, которая позволит полностью сбросить бот. Дополнительные сведения о реализации этого см. в [примере Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) или [примере C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238).

#### <a name="schema-example-bot-added-to-personal-context"></a>Пример схемы: бот добавлен в личный контекст

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

## <a name="team-member-or-bot-removed"></a>Удален участник команды или бот

Событие `conversationUpdate` с объектом `membersRemoved` в полезных данных отправляется при удалении бота из команды или при удалении пользователя из команды, в которую был добавлен бот. Microsoft Teams также добавляет `eventType.teamMemberRemoved` в объект `channelData`. Как и в случае с объектом `membersAdded`, необходимо проанализировать объект `membersRemoved` на наличие идентификатора приложения бота, чтобы определить объект удаления.

### <a name="schema-example-team-member-removed"></a>Пример схемы: удален участник команды

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

### <a name="user-removed-from-a-meeting"></a>Пользователь удален из собрания

Событие `conversationUpdate` с объектом `membersRemoved` в полезных данных отправляется при удалении пользователя из закрытого запланированного собрания. Сведения о событии отправляются даже при присоединении анонимных пользователей к собранию.

> [!NOTE]
>
>* При удалении анонимного пользователя из собрания объект полезных данных membersRemoved не содержит поле `aadObjectId`.
>* При удалении анонимного пользователя из собрания объект `from` в полезных данных всегда содержит идентификатор организатора собрания, даже если анонимный пользователь был удален другим выступающим.

#### <a name="schema-example-user-removed-from-meeting"></a>Пример схемы: пользователь удален из собрания

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a>Обновление имени команды

> [!NOTE]
> Нет функций для запроса имен всех команд, и имя команды не возвращается в полезных данных из других событий.

Бот получает уведомление при переименовании команды, в которой он находится. Он получает событие `conversationUpdate` с `eventType.teamRenamed` в объекте `channelData`. Обратите внимание, что уведомления о создании или удалении команды отсутствуют, так как боты существуют только в составе команд и не имеют видимости за пределами области, в которую они были добавлены.

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

## <a name="channel-updates"></a>Обновление каналов

Бот получает уведомление при создании, переименовании или удалении канала в команде, в которую он был добавлен. И вновь будет получено событие `conversationUpdate` и отправлен идентификатор события, связанный с Teams, как часть объекта `channelData.eventType`. При этом параметр `channel.id` данных канала является GUID канала, а `channel.name` содержит имя самого канала.

Ниже перечислены события канала.

* **channelCreated**&emsp;. Пользователь добавляет новый канал в команду.
* **channelRenamed**&emsp;. Пользователь переименовывает существующий канал.
* **channelDeleted**&emsp;. Пользователь удаляет канал.

### <a name="full-schema-example-channelcreated"></a>Пример полной схемы: channelCreated

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Фрагмент схемы: channelData для channelRenamed

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Фрагмент схемы: channelData для channelDeleted

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

## <a name="reactions"></a>Реакции

Событие `messageReaction` отправляется, когда пользователь добавляет или удаляет свою реакцию на сообщение, которое изначально было отправлено ботом. `replyToId` содержит идентификатор конкретного сообщения.

### <a name="schema-example-a-user-likes-a-message"></a>Пример схемы: пользователь ставит отметку "Нравится" для сообщения

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

### <a name="schema-example-a-user-un-likes-a-message"></a>Пример схемы: пользователь удаляет отметку "Нравится" для сообщения

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
