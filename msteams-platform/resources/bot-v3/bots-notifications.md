---
title: Обработка событий бота
description: Описание обработки событий в ботах для Microsoft Teams
keywords: события командных ботов
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 5a7f7971d7f58af315222933f1c1f192868a4171
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020641"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Обработка событий бота в Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams отправляет уведомления вашему боту об изменениях или событиях, которые происходят в области, в которых активен бот. Эти события можно использовать для запуска логики службы, например следующих:

* Запуск приветствия при добавлении бота в команду
* Сведения о группе запроса и кэша при добавлении бота в групповой чат
* Обновление кэшных сведений о членстве в команде или сведениях о каналах
* Удаление кэшных сведений для группы при удалении бота
* Если сообщение бота нравится пользователю

Каждое событие бота отправляется в качестве объекта, в `Activity` котором `messageType` определяется, какая информация находится в объекте. Для сообщений типа `message` см. [в рублях Отправка и получение сообщений.](~/resources/bot-v3/bot-conversations/bots-conversations.md)

В группах и групповых событиях, которые обычно запускаются с этого типа, в объект передаются дополнительные сведения о событиях Teams, поэтому обработчиве событий должен запрашивать полезное количество команд и дополнительные метаданные, определенные `conversationUpdate` `channelData` `channelData` `eventType` событиями.

В следующей таблице перечислены события, которые бот может получить и принять меры.

|Type|Объект полезной нагрузки|Teams eventType |Описание|Область|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Член, добавленный в команду](#team-member-or-bot-addition)| все |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Участник был удален из группы](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [Команда была переименована](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Создан канал](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Канал был переименован](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Канал был удален](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Реакция на сообщение бота](#reactions)| все |
| `messageReaction` |`reactionsRemoved`|| [Реакция, удаленная из сообщения бота](#reactions)| все |

## <a name="team-member-or-bot-addition"></a>Добавление члена команды или бота

Событие отправляется вашему боту, когда он получает сведения об обновлениях членства [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) для команд, в которых оно было добавлено. Бот также получает обновление при первом добавлении в личную беседу. Обратите внимание, что пользовательские сведения () являются уникальными для вашего бота и могут быть кэшными для дальнейшего использования службой (например, отправки сообщения `Id` конкретному пользователю).

### <a name="bot-or-user-added-to-a-team"></a>Бот или пользователь, добавленный в команду

Событие с объектом в полезной нагрузке отправляется при добавлении бота в команду или в команду, в которой был добавлен `conversationUpdate` `membersAdded` бот. Microsoft Teams также добавляет `eventType.teamMemberAdded` в `channelData` объект.

Так как это событие отправляется в обоих случаях, необходимо разсмеять объект, чтобы определить, является ли добавление пользователем или `membersAdded` самим ботом. В последнем случае лучше всего отправлять [](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) приветствие на канал, чтобы пользователи могли понимать функции, которые предоставляет бот.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Пример кода. Проверка того, является ли бот добавленным участником

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

### <a name="user-added-to-a-meeting"></a>Пользователь, добавленный к собранию

Событие `conversationUpdate` с объектом в полезной нагрузке отправляется при добавлении пользователя на `membersAdded` закрытое запланированное собрание. Сведения о событии будут отправлены, даже если анонимные пользователи присоединятся к собранию. 

> [!NOTE]
>
>* При добавлении анонимного пользователя в собрание объект полезной нагрузки membersAdded не имеет `aadObjectId` поля.
>* Когда анонимный пользователь добавляется в собрание, объект в полезной нагрузке всегда имеет id организатора собрания, даже если анонимный пользователь был добавлен `from` другим презентером.

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

### <a name="bot-added-for-personal-context-only"></a>Бот, добавленный только для личного контекста

Ваш бот получает `conversationUpdate` с, `membersAdded` когда пользователь добавляет его непосредственно для личного чата. В этом случае полезной нагрузки, получаемой ботом, объект не `channelData.team` содержится. Вы должны использовать это в качестве фильтра, если вы хотите, чтобы ваш бот предложил другое приветствие [в](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) зависимости от области.

> [!NOTE]
> Для личных масштабных ботов боты получают событие несколько раз, даже если бот удален и `conversationUpdate` повторно добавлен. Для разработки и тестирования может оказаться полезным добавить функцию помощника, которая позволит полностью сбросить бот. Дополнительные [ сведения о реализации этого](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts)Node.js или [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) примере.

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

## <a name="team-member-or-bot-removed"></a>Удален член команды или бот

Событие с объектом в полезной нагрузке отправляется, когда бот удаляется из группы или пользователь удаляется из команды, в которой был `conversationUpdate` `membersRemoved` добавлен бот. Microsoft Teams также добавляет `eventType.teamMemberRemoved` в `channelData` объект. Как и в объекте, необходимо размазить объект для ID приложения вашего бота, чтобы определить, `membersAdded` `membersRemoved` кто был удален.

### <a name="schema-example-team-member-removed"></a>Пример схемы: удален член команды

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

### <a name="user-removed-from-a-meeting"></a>Пользователь, удаленый из собрания

Событие с объектом в полезной нагрузке отправляется при удалении пользователя из `conversationUpdate` `membersRemoved` закрытого запланированного собрания. Сведения о событии будут отправлены, даже если анонимные пользователи присоединятся к собранию. 

> [!NOTE]
>
>* Когда анонимный пользователь удаляется из собрания, объект полезной нагрузки membersRemoved не имеет `aadObjectId` поля.
>* Когда анонимный пользователь удаляется из собрания, объект в полезной нагрузке всегда имеет id организатора собрания, даже если анонимный пользователь был удален другим `from` презентщиком.

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

## <a name="team-name-updates"></a>Обновления имени команды

> [!NOTE]
> Нет функций для запроса всех имен команд, и имя команды не возвращается в полезной нагрузке из других событий.

Ваш бот уведомлен о переименовании команды, в которая он находится. Он получает событие `conversationUpdate` в `eventType.teamRenamed` `channelData` объекте. Обратите внимание, что уведомлений о создании или удалении группы нет, так как боты существуют только в составе групп и не имеют видимости за пределами области, в которую они были добавлены.

### <a name="schema-example-team-renamed"></a>Пример схемы: переименована команда

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

Ваш бот уведомлен, когда канал создается, переименовываются или удаляются в команде, в которой он был добавлен. Опять же, событие получено, и идентификатор события, определенного teams, отправляется в составе объекта, где данные канала являются GUID для канала, и содержит имя самого `conversationUpdate` `channelData.eventType`  `channel.id` `channel.name` канала.

События канала следуют следующим образом:

* **channelCreated** &emsp; Пользователь добавляет новый канал в команду
* **ChannelRenamed** &emsp; Пользователь переименовывает существующий канал
* **channelDeleted** &emsp; Пользователь удаляет канал

### <a name="full-schema-example-channelcreated"></a>Полный пример схемы: channelCreated

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Выдержка схемы: channelData для каналаRenamed

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Выдержка схемы: channelData для channelDeleted

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

Событие отправляется, когда пользователь добавляет или удаляет свою реакцию на сообщение, которое изначально было `messageReaction` отправлено вашим ботом. `replyToId` содержит ID конкретного сообщения.

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
