---
title: Беседы в чатах каналов и групп с ботами
description: Описание всего сценария беседы с ботом в канале в Microsoft Teams
keywords: бот беседы каналов teams сценариев
ms.date: 06/25/2019
ms.openlocfilehash: e556eb006257a83ddf93adb62f79857201d6a9ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231633"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Беседы в чатах каналов и групп с помощью бота Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams позволяет пользователям вводить ботов в свои каналы или групповые беседы чата. Добавляя бота в команду или чат, все пользователи беседы могут воспользоваться функциями бота прямо в беседе. Вы также можете получить доступ к функциям Teams в боте, например запрашивать сведения о команде и @mentioning пользователям.

Чат в каналах и групповых чатах отличается от личного чата тем, что пользователю необходимо @mention бота. Если бот используется в нескольких сферах (личных, групповых или каналов), необходимо определить область, из которых поступили сообщения бота, и обработать их соответствующим образом.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Разработка отличного бота для каналов или групп

Боты, добавленные в команду, становятся другими членами команды и @mentioned быть частью беседы. На самом деле боты получают сообщения только @mentioned, поэтому другие беседы в канале не отправляются боту.

Бот в группе или канале должен предоставлять сведения, релевантные и подходящие для всех участников. Несмотря на то что бот может предоставить любую информацию, относяную к опытом, помните, что беседы с ним видны всем. Таким образом, отличный бот в группе или канале должен добавить значение для всех пользователей и, конечно, не случайно поделиться информацией, более подходящей для беседы "один к одному".

Ваш бот, как и он есть, может быть полностью релевантн во всех сферах без необходимости дополнительной работы. В Microsoft Teams нет ожидания, что ваш бот будет работать во всех сферах, но следует убедиться, что бот предоставляет пользователю значение в зависимости от областей, которые вы выбрали для поддержки. Дополнительные сведения об области см. в [приложениях в Microsoft Teams.](~/concepts/build-and-test/app-studio-overview.md)

Разработка бота, работающего в группах или каналах, использует те же функции, что и личные беседы. Дополнительные события и данные в полезной нагрузке предоставляют сведения о группах и каналах Teams. Эти различия, а также основные различия в общих функциях описаны в следующих разделах.

### <a name="creating-messages"></a>Создание сообщений

Дополнительные сведения о ботах, создающих [](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)сообщения в каналах, см. в упреждающих сообщениях для ботов и, в частности, о создании [беседы в канале.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)

### <a name="receiving-messages"></a>Получение сообщений

Бот в группе или канале помимо [](https://docs.botframework.com/core-concepts/reference/#activity)обычной схемы сообщений также получает следующие свойства:

* `channelData`См. [данные канала Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data) В групповом чате содержит сведения, характерные для этого чата.
* `conversation.id` ИД цепочки ответов, состоящий из ИД канала и первого сообщения в цепочке ответов
* `conversation.isGroup` Is `true` for bot messages in channels or group chats
* `conversation.conversationType` Один `groupChat` или несколько `channel`
* `entities`Может содержать одно или несколько упоминаний (см. ["Упоминания")](#-mentions)

### <a name="replying-to-messages"></a>Ответ на сообщения

Чтобы ответить на существующее сообщение, вызовите [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .NET [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) или Node.js. SDK построитель ботов обрабатывает все сведения.

Если вы решили использовать REST API, можно также вызвать [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) конечную точку.

В канале ответ на сообщение показывается как ответ на инициированную цепочку ответов. Содержит `conversation.id` канал и ИД сообщения верхнего уровня. Несмотря на то, что Bot Framework берет на себя все сведения, вы можете кэширует их для будущих ответов на беседу при `conversation.id` необходимости.

### <a name="best-practice-welcome-messages-in-teams"></a>Best practice: Welcome messages in Teams

При первом добавлении бота в группу или команду, как правило, полезно отправить приветствие с ботом всем пользователям. В приветствуемом сообщении должно быть описание функций и преимуществ бота. В идеале сообщение должно также включать команды для взаимодействия пользователя с приложением. Для этого убедитесь, что бот отвечает на сообщение `conversationUpdate` с `teamsAddMembers` помощью eventType в `channelData` объекте. Убедитесь, что этот ИД является самим идом приложения бота, так как то же событие отправляется при добавлении пользователя `memberAdded` в команду. Дополнительные [сведения см. в добавлении участника команды](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) или бота.

Вы также можете отправить личное сообщение каждому участнику команды при добавлении бота. Для этого можно получить список команд и [отправить](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) каждому пользователю [прямое сообщение.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

Мы рекомендуем боту не *отправлять* приветствие в следующих ситуациях:

* Команда большая (очевидно, что она субъективна, но, например, более 100 участников). Ваш бот может быть виден как "спам", а добавлявший его пользователь может получить жалобы, если вы не ясно сообщаете о преимуществах вашего бота всем, кто видит приветствие.
* Ваш бот впервые упоминается в группе или канале (по сравнению с первым добавлением в команду)
* Группа или канал переименовываются
* Участник команды добавляется в группу или канал

## <a name="-mentions"></a>@ Упоминания

Так как боты в группе или канале отвечают, только когда они упомянуты ("@_botname")_ в сообщении, каждое сообщение, полученное ботом в канале группы, содержит собственное имя, и вы должны убедиться, что ваш разберегающий сообщения обрабатывает его. Кроме того, боты могут высмеять других пользователей, упомянутых в сообщениях, и упоминать их.

### <a name="retrieving-mentions"></a>Искомые упоминания

Упоминания возвращаются в объекте в полезной нагрузке и содержат как уникальный ИД пользователя, так и, в большинстве случаев, имя `entities` упомянутого пользователя. Вы можете получить все упоминания в сообщении, вызывая функцию в SDK построщика ботов для .NET, которая возвращает `GetMentions` массив `Mentioned` объектов.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Пример кода .NET: проверка и @bot упоминания

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> Вы также можете использовать функцию расширения Teams, которая отключит все упоминания, включая `GetTextWithoutMentions` бота.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js пример кода: проверка и @bot упоминания

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

Вы также можете использовать функцию расширения Teams, которая отключит все упоминания, включая `getTextWithoutMentions` бота.

### <a name="constructing-mentions"></a>Создание упоминаний

Бот может упоминать других пользователей в сообщениях, которые были опубликованы в каналах. Для этого ваше сообщение должно сделать следующее:

* Включить `<at>@username</at>` в текст сообщения
* Включить `mention` объект в коллекцию сущностями

#### <a name="net-example"></a>Пример .NET

В этом примере используется [пакет NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js примере

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a>Пример: исходяние сообщения с указанным пользователем

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

## <a name="accessing-groupchat-or-channel-scope"></a>Доступ к groupChat или области канала

Бот может не только отправлять и получать сообщения в группах и командах. Например, он также может получить список участников, включая сведения об их профилях, а также список каналов. Дополнительные [дополнительные узнать в контексте программы-робота Microsoft Teams](~/resources/bot-v3/bots-context.md) см. в этой теме.

*См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
