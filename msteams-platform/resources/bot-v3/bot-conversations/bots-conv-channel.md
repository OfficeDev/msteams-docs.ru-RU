---
title: Телефонные и групповые беседы чата с ботами
description: Описывает конечный сценарий беседы с ботом в канале в Microsoft Teams
keywords: teams scenarios channels conversation bot
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: 8e4336e8b0db7c6c720b8fb7adcb281685b6a6ba
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157288"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Беседы в каналах и групповых чатах с ботом Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams позволяет пользователям вводить ботов в свои каналы или групповые беседы в чате. Добавляя бота в команду или чат, все пользователи беседы могут воспользоваться функциональными возможностями бота прямо во время беседы. Вы также можете получить доступ Teams в боте, например запрашивать сведения о группе и @mentioning пользователей.

Чат в каналах и групповых чатах отличается от личного чата тем, что пользователю необходимо @mention бота. Если бот используется в нескольких сферах, таких как личный, групповой или канал, необходимо определить область, из какой области пришли сообщения бота, и обработать их соответствующим образом.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Разработка отличного бота для каналов или групп

Боты, добавленные в команду, становятся другими членами группы и @mentioned быть частью беседы. Фактически, боты получают сообщения только при @mentioned, поэтому другие беседы на канале не отправляются боту.

Бот в группе или канале должен предоставлять информацию, соответствующую и соответствующую всем участникам. Хотя ваш бот, безусловно, может предоставить любую информацию, относяную к опыту, имейте в виду, что беседы с ним видны всем. Таким образом, большой бот в группе или канале должен добавить значение для всех пользователей и, конечно, непреднамеренно обмениваться информацией, более подходящей для беседы один к одному.

Ваш бот, как и он есть, может быть полностью актуальным во всех сферах без необходимости дополнительной работы. В Microsoft Teams не ожидается, что ваш бот будет функционировать во всех сферах, но вы должны убедиться, что ваш бот предоставляет пользователю значение в том, в какой области (ы) вы решите поддерживать. Дополнительные сведения о области [см.](~/concepts/build-and-test/app-studio-overview.md)в Microsoft Teams.

Разработка бота, работающего в группах или каналах, использует те же функции, что и личные беседы. Дополнительные события и данные в полезной нагрузке предоставляют Teams группы и канала. Эти различия, а также ключевые различия в общих функциональных возможностях описаны в следующих разделах.

### <a name="creating-messages"></a>Создание сообщений

Дополнительные сведения о ботах, создающих [](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)сообщения в каналах, см. в дополнительных сведениях проактивное сообщение для ботов и, в [частности, создание беседы на канале.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)

### <a name="receiving-messages"></a>Получение сообщений

Для бота в группе или канале, в дополнение к схеме регулярного [сообщения,](https://docs.botframework.com/core-concepts/reference/#activity)ваш бот также получает следующие свойства:

* `channelData`См. [Teams каналов](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)данных. В групповом чате содержится информация, специфическая для этого чата.
* `conversation.id` ID цепочки ответов, состоящий из ИД канала плюс ID первого сообщения в цепочке ответов.
* `conversation.isGroup` Для `true` бот-сообщений в каналах или групповых чатах.
* `conversation.conversationType` Либо `groupChat` или `channel` .
* `entities` Может содержать одно или несколько упоминаний. Дополнительные сведения см. в [руберсах Mentions](#-mentions).

### <a name="replying-to-messages"></a>Ответы на сообщения

Чтобы ответить на существующее сообщение, [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) позвоните в .NET или [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) в Node.js. SDK Bot Builder обрабатывает все сведения.

Если вы решите использовать API REST, вы также можете вызвать [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) конечную точку.

В канале, отвечая на сообщение показывает, как ответ на начало цепочки ответов. Содержит `conversation.id` канал и ID сообщения верхнего уровня. Несмотря на то, что bot Framework заботится о деталях, можно кэширует эти ответы для будущих ответов на этот поток беседы по `conversation.id` мере необходимости.

### <a name="best-practice-welcome-messages-in-teams"></a>Best practice: Welcome messages in Teams

При первом добавлении бота в группу или группу обычно полезно отправить приветствие, в которое будет вводиться бот всем пользователям. В приветовом сообщении должно быть описано функциональные возможности и преимущества бота. В идеале сообщение должно также включать команды для взаимодействия пользователя с приложением. Для этого убедитесь, что бот отвечает на сообщение `conversationUpdate` с `teamsAddMembers` помощью eventType в `channelData` объекте. Убедитесь, что ID — это сам app ID бота, так как одно и то же событие отправляется при добавлении `memberAdded` пользователя в команду. Дополнительные [сведения см. в дополнительных сведениях о](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) члене команды или добавлении бота.

Кроме того, при добавлении бота может потребоваться отправить личное сообщение каждому члену группы. Для этого можно получить список [команд](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) и отправить каждому пользователю [прямое сообщение.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

Рекомендуется не отправлять *боту* приветствие в следующих ситуациях:

* Команда большая (очевидно субъективная, например, более 100 участников). Ваш бот может рассматриваться как "spammy", а добавленный в него пользователь может получать жалобы, если вы четко не сообщаете всем, кто видит приветствие, о ценности вашего бота.
* Ваш бот сначала упоминается в группе или канале, а не добавляется в команду.
* Группа или канал переименованы.
* Член группы добавляется в группу или канал.

## <a name="-mentions"></a>@ Упоминания

Так как боты в группе или канале отвечают только тогда, когда они упоминаются ("@_botname")_ в сообщении, каждое сообщение, полученное ботом в групповом канале, содержит свое имя, и необходимо убедиться, что обработка размывов сообщений обрабатывает это. Кроме того, боты могут сравнений между другими пользователями, упомянутыми в сообщениях, и упоминать их в качестве части сообщений.

### <a name="retrieving-mentions"></a>Получение упоминаний

Упоминания возвращаются в объект в полезной нагрузке и содержат как уникальный ID пользователя, так и, в большинстве случаев, имя `entities` упомянутого пользователя. Вы можете получить все упоминания в сообщении, позвонив функции в SDK bot Builder для .NET, которая возвращает `GetMentions` массив `Mentioned` объектов.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Код примера .NET: проверка упоминания о @bot и @bot

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
> Вы также можете использовать функцию Teams расширения, которая отключит все упоминания, включая `GetTextWithoutMentions` бот.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js пример кода: проверка упоминания о @bot и @bot

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

Вы также можете использовать функцию Teams расширения, которая отключит все упоминания, включая `getTextWithoutMentions` бот.

### <a name="constructing-mentions"></a>Построение упоминаний

Ваш бот может упоминать других пользователей в сообщениях, которые размещены в каналах. Для этого ваше сообщение должно сделать следующее:

* `<at>@username</at>`Включаем в текст сообщения.
* `mention`Включи объект в коллекцию сущностями.

#### <a name="net-example"></a>Пример .NET

В этом примере используется [пакет Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js пример

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Пример. Исходяние сообщения с указанным пользователем

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

## <a name="accessing-groupchat-or-channel-scope"></a>Доступ к groupChat или области каналов

Ваш бот может не только отправлять и получать сообщения в группах и группах. Например, он также может получать список участников, включая сведения о профиле, а также список каналов. Дополнительные сведения см. в [дополнительных сведениях: Получить контекст для Microsoft Teams бота.](~/resources/bot-v3/bots-context.md)

## <a name="see-also"></a>См. также

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
