---
title: События хваской бота
description: Описывает, как обрабатывать события в ботах для Microsoft Teams
keywords: команды ботов событий
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: da624ea0e92e193f4ad7f334d958349d542dd6e0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566469"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Обработать бот-события в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams отправляет уведомления вашему боту об изменениях или событиях, которые происходят в тех сферах, где ваш бот активен. Эти события можно использовать для запуска логики обслуживания, например:

* Запустите приветственное сообщение, когда ваш бот будет добавлен в команду.
* Информация о группе запросов и кэша при добавлении бота в групповой чат.
* Обновление кэшированной информации о членстве в команде или информации о канале.
* Удалите кэшированную информацию для команды, если бот будет удален.
* Когда сообщение бота нравится пользователю.

Каждое событие бота отправляется как `Activity` объект, в `messageType` котором определяется, какая информация находится в объекте. Для сообщений `message` типа, см [Отправка и получение сообщений](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Teams и групповые события, обычно запускаемые из `conversationUpdate` типа, имеют дополнительную информацию о событиях `channelData` Teams, передаваемую как часть объекта, и поэтому обработчик событий должен `channelData` запросить полезную нагрузку для Teams и `eventType` дополнительные метаданные, связанные с событиями.

В следующей таблице перечислены события, которые ваш бот может получить и принять меры.

|Тип|Объект полезной нагрузки|Teams eventType |Описание|Область|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Член, добавленный в команду](#team-member-or-bot-addition)| все |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Участник был удален из команды](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [Команда была переименована](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Создан канал](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Канал был переименован](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Канал был удален](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Реакция на сообщение бота](#reactions)| все |
| `messageReaction` |`reactionsRemoved`|| [Реакция удалена из сообщения бота](#reactions)| все |

## <a name="team-member-or-bot-addition"></a>Добавление члена команды или бота

Событие [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) отправляется вашему боту, когда он получает информацию об обновлениях членства для команд, где оно было добавлено. Бот также получает обновление при первом добавлении в личную беседу. Обратите внимание, что пользовательскую информацию () уникальна для вашего бота и может быть кэширована для использования `Id` в будущем вашим сервисом, например, отправка сообщения конкретному пользователю.

### <a name="bot-or-user-added-to-a-team"></a>Бот или пользователь добавлен в команду

Событие `conversationUpdate` с объектом `membersAdded` в полезной нагрузке отправляется, когда в команду добавляется бот или новый пользователь, который добавляется в группу, в которую был добавлен бот. Microsoft Teams добавляет в `eventType.teamMemberAdded` `channelData` объект.

Поскольку это событие отправляется в обоих случаях, следует разобрать `membersAdded` объект, чтобы определить, было ли дополнение пользователем или ботом. Для последнего наилучшей практикой является отправка [приветственного сообщения каналу,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) чтобы пользователи могли понять функции, которые предоставляет ваш бот.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Пример кода: Проверка того, был ли бот добавленным участником

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

#### <a name="schema-example-bot-added-to-team"></a>Пример Schema: Bot добавлен в команду

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

### <a name="user-added-to-a-meeting"></a>Пользователь добавлен на собрание

Событие `conversationUpdate` с объектом `membersAdded` в полезной нагрузке отправляется, когда пользователь добавляется к частному запланированной встрече. Детали мероприятия будут отправлены даже тогда, когда анонимные пользователи присоединятся к собранию. 

> [!NOTE]
>
>* Когда анонимный пользователь добавляется к собранию, у объекта полезной нагрузки нет `aadObjectId` поля.
>* Когда анонимный пользователь добавляется на собрание, объект в `from` полезной нагрузке всегда имеет идентификатор организатора собрания, даже если анонимный пользователь был добавлен другим докладчиком.

#### <a name="schema-example-user-added-to-meeting"></a>Пример Schema: Пользователь добавлен к собранию

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

Ваш бот получает `conversationUpdate` с, `membersAdded` когда пользователь добавляет его непосредственно для личного чата. В этом случае полезная нагрузка, которую получает ваш бот, не содержит `channelData.team` объекта. Вы должны использовать это в качестве фильтра в случае, если вы хотите, чтобы ваш бот предложить различные [приветственные сообщения в зависимости](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) от сферы.

> [!NOTE]
> Для личных ботов боты, ваш бот `conversationUpdate` будет получать событие несколько раз, даже если бот удаляется и повторно добавлен. Для разработки и тестирования вы можете найти полезным добавить функцию помощник, который позволит вам сбросить ваш бот полностью. Более [ подробную информациюNode.js этом](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) [можно получить в](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) качестве примера или примера C-A.

#### <a name="schema-example-bot-added-to-personal-context"></a>Пример Schema: бот добавлен в личный контекст

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

## <a name="team-member-or-bot-removed"></a>Член команды или бот удален

Событие `conversationUpdate` с объектом в полезной нагрузке отправляется, когда либо ваш бот удаляется из команды, либо `membersRemoved` пользователь удаляется из команды, где был добавлен бот. Microsoft Teams добавляет в `eventType.teamMemberRemoved` `channelData` объект. Как и в `membersAdded` случае с объектом, вы должны разобрать объект для App `membersRemoved` ID вашего бота, чтобы определить, кто был удален.

### <a name="schema-example-team-member-removed"></a>Пример Schema: удален член команды

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

### <a name="user-removed-from-a-meeting"></a>Пользователь удален с собрания

Событие `conversationUpdate` с объектом `membersRemoved` в полезной нагрузке отправляется, когда пользователь удаляется из частного запланированного собрания. Детали мероприятия будут отправлены даже тогда, когда анонимные пользователи присоединятся к собранию. 

> [!NOTE]
>
>* Когда анонимный пользователь удаляется с собрания, у объекта полезной нагрузки membersRemoved нет `aadObjectId` поля.
>* Когда анонимный пользователь удаляется с собрания, объект в `from` полезной нагрузке всегда имеет идентификатор организатора собрания, даже если анонимный пользователь был удален другим докладчиком.

#### <a name="schema-example-user-removed-from-meeting"></a>Пример Schema: Пользователь удален с собрания

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

## <a name="team-name-updates"></a>Обновления имен команд

> [!NOTE]
> Нет функциональности для запроса всех имен команд, и имя команды не возвращается в полезных нагрузках из других событий.

Ваш бот уведомляется о переименовании команды, в ней находится. Он получает `conversationUpdate` событие с в `eventType.teamRenamed` `channelData` объекте. Обратите внимание, что нет никаких уведомлений о создании или удалении команды, поскольку боты существуют только как часть команд и не имеют видимости вне области, в которую они были добавлены.

### <a name="schema-example-team-renamed"></a>Пример Schema: Команда переименована

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

## <a name="channel-updates"></a>Обновления каналов

Ваш бот уведомляется о том, что канал создается, переименован или удаляется в команде, где он был добавлен. Опять `conversationUpdate` же, событие получено, и Teams-специфический идентификатор события отправляется как часть объекта, где данные `channelData.eventType` `channel.id` канала является GUID для канала, `channel.name` и содержит само название канала.

События канала таковы:

* **каналСоздается** &emsp; Пользователь добавляет новый канал в команду.
* **канал переименован** &emsp; Пользователь переименовывает существующий канал.
* **каналДелетирован** &emsp; Пользователь удаляет канал.

### <a name="full-schema-example-channelcreated"></a>Полный пример схемы: каналСоздается

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Схема отрывок: channelData для канала Переименован

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Схема отрывок: channelData для channelDeleted

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

Событие `messageReaction` отправляется, когда пользователь добавляет или удаляет свою реакцию на сообщение, которое было первоначально отправлено вашим ботом. `replyToId` содержит идентификатор конкретного сообщения.

### <a name="schema-example-a-user-likes-a-message"></a>Пример Schema: Пользователю нравится сообщение

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

### <a name="schema-example-a-user-un-likes-a-message"></a>Пример Schema: пользователь не любит сообщение

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
