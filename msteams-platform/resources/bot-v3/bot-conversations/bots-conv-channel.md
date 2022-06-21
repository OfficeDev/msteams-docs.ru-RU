---
title: Беседы в каналах и групповых чатах с ботом Microsoft Teams
description: В этом модуле вы узнаете сквозной сценарий общения с ботом в канале в Microsoft Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e93b6cc18e38da4f6307fda3d30968bfa709dbf1
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190179"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Беседы в каналах и групповых чатах с ботом Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams позволяет пользователям вводить ботов в беседы в канале или групповом чате. При добавлении бота в команду или чат все участники беседы могут пользоваться функциями бота прямо в беседе. Через бота можно также получать доступ к специфичным функциям Teams, например запрашивать сведения о команде и @упоминать пользователей.

Чат в каналах и групповых чатах отличается от личного чата тем, что пользователю необходимо @mention бота. Если бот используется в нескольких областях, таких как личный, групповой чат или канал, необходимо определить, из какой области поступили сообщения бота, и обработать их соответствующим образом.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Проектирование качественного бота для каналов и групп

Бот, добавленный в группу, становится еще одним участником команды, и его можно @упоминать в ходе беседы. На самом деле боты получают сообщения только при @mentioned, поэтому другие беседы в канале не отправляются боту.

Бот в группе или канале должен предоставлять информацию, своевременную и подходящую всем участникам. Бот может предоставить любые сведения, относящиеся к делу, но помните, что беседы с ним видны всем. Таким образом, отличный бот в группе или канале должен приносить пользу всем участникам и, конечно, не выдавать спонтанно информацию, более подходящую для беседы один на один.

Ваш бот, как и он есть, может быть полностью актуальным во всех областях, не требуя дополнительной работы. В Teams не ожидается, что бот будет работать во всех областях, но следует убедиться, что бот предоставляет значение пользователя в любой области, которую вы выбрали для поддержки. Подробнее об областях см. в разделе [Приложения в Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).

Разработка бота для группвых бесед или каналов использует те же функции, что и при разработке бота для личных бесед. Дополнительные события и данные в полезных данных предоставляют Teams информацию о группах и каналах. Эти различия, а также основные различия в общих функциях описаны в следующих разделах.

### <a name="creating-messages"></a>Создание сообщений

Дополнительные сведения о ботах, создающих сообщения в каналах, [](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)см. в статьях "Упреждающее обмен сообщениями для ботов" и "Создание [беседы по каналу"](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).

### <a name="receiving-messages"></a>Получение сообщений

Бот в группе или канале помимо [обычной схемы сообщений](https://docs.botframework.com/core-concepts/reference/#activity)также получает следующие свойства:

* `channelData`См. [Данные каналов Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data). В групповом чате бот содержит следующие сведения, относящиеся к конкретному чату.
* `conversation.id` Идентификатор цепочки ответов, состоящий из идентификатора канала и идентификатора первого сообщения в цепочке ответов.
* Значение `conversation.isGroup` равно `true` для сообщений бота в каналах и групповых чатах.
* Возможные значения `conversation.conversationType`: `groupChat` или `channel`.
* `entities` Может содержать одно или несколько упоминаний. Дополнительные сведения см. в разделе [Упоминания](#-mentions).

### <a name="replying-to-messages"></a>Ответ на сообщения

Чтобы ответить на существующее сообщение, вызовите [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) в .NET или [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) в Node.js. Пакет SDK Bot Builder обрабатывает все сведения.

Если вы решили использовать REST API, можно также вызвать конечную точку [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply).

В канале ответ на сообщение виден как ответ на инициированную цепочку ответов. `conversation.id` содержит идентификатор канала и идентификатор сообщения верхнего уровня. Хотя всеми деталями занимается Bot Framework, `conversation.id` можно кэшировать для будущих ответов на этот поток беседы по мере необходимости.

### <a name="best-practice-welcome-messages-in-teams"></a>Рекомендация. Приветственные сообщения в Teams

При первом добавлении бота в группу или команду полезно отправить приветственное сообщение со сведениями о боте всем пользователям. Приветственное сообщение должно содержать описание функциональных возможностей бота и пользы, которую он принесет участникам. В идеале сообщение должно также содержать команды для взаимодействия пользователя с приложением. Для этого убедитесь, что бот отвечает на сообщение `conversationUpdate` отправкой eventType `teamsAddMembers` в объекте `channelData`. Убедитесь, что идентификатор `memberAdded` является идентификатором приложения бота, так как то же событие отправляется при добавлении пользователя в команду. Дополнительные сведения см. в [разделе "Добавление участника команды или бота](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) ".

Кроме того, при добавлении бота бывает нужно отправить личное сообщение каждому участнику команды. Для этого можно получить [список команды](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) и отправить каждому пользователю [прямое сообщение](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

Мы рекомендуем боту *не* отправлять приветственное сообщение в следующих ситуациях:

* Команда большая (очевидно, что это субъективный критерий - ну, например, если в ней более 100 участников). Ваш бот может рассматриваться как "отправитель спама", а пользователь, который добавил его, может получать жалобы, если вы не сообщите о ценности бота явным образом всем, кто видит приветственное сообщение.
* Ваш бот упоминается в группе или канале раньше, чем добавлен в команду.
* Группа или канал переименованы.
* Участник команды добавляется в группу или канал.

## <a name="-mentions"></a>@Упоминания

Так как боты в группе или канале отвечают только в том случае, если они упомянуты в сообщении ("@*botname*"), каждое сообщение, полученное ботом в канале группы, содержит собственное имя, и необходимо убедиться, что анализ сообщений обрабатывает это. Кроме того, боты могут извлекать посредством анализа имена других пользователей, упомянутых в сообщениях, и упоминать их в собственных сообщениях.

### <a name="retrieving-mentions"></a>Получение упоминаний

Упоминания возвращаются в полезных данных объекта `entities` и содержат как уникальный ИД пользователя, так и, в большинстве случаев, имя упомянутого пользователя. Вы можете получить все упоминания в сообщении, вызвав функцию в`GetMentions` из пакета SDK Bot Builder для .NET, которая возвращает массив объектов `Mentioned` .

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Пример кода .NET: проверка наличия упоминаний @bot и удаление их

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
> Можно также использовать функцию расширения Teams `GetTextWithoutMentions`, которая позволяет удалить все упоминания, включая упоминания бота.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Пример кода Node.js: проверка наличия упоминаний @bot и удаление их

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

Можно также использовать функцию расширения Teams `getTextWithoutMentions`, которая позволяет удалить все упоминания, включая упоминания бота.

### <a name="constructing-mentions"></a>Создание упоминаний

Бот может упоминать других пользователей в сообщениях, опубликованных в каналах. Для этого выполните следующие шаги.

* Включите `<at>@username</at>` в текст сообщения.
* Включите объект `mention` в коллекцию сущностей.

#### <a name="net-example"></a>Пример .NET

В этом примере используется пакет NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Пример Node.js

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Пример: исходящее сообщение, в котором упомянут пользователь

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

## <a name="accessing-groupchat-or-channel-scope"></a>Доступ к области группового чата или канала

Бот может не только отправлять и получать сообщения в группах и командах. Например, он может получить список участников со сведениями из профиля, а также список каналов. Дополнительные сведения см. в разделе [Получение контекста для бота Microsoft Teams](~/resources/bot-v3/bots-context.md).

## <a name="see-also"></a>Дополнительные ресурсы

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
