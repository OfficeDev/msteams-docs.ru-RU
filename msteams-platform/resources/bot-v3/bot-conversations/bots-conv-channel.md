---
title: Разговоры о чате канала и группы с ботами
description: Описывается тот же сценарий разговора с ботом в канале в Microsoft Teams
keywords: команды сценарии каналов разговор бот
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566798"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Беседы в каналах и групповых чатах с ботом Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams позволяет пользователям приносить ботов в свой канал или групповые чаты. Добавив бота в команду или чат, все пользователи разговора могут воспользоваться функциональностью бота прямо в разговоре. Вы также можете получить Teams конкретной функциональности в вашем боте, как запрос информации команды и @mentioning пользователей.

Чат в каналах и групповых чатах отличается от личного чата тем, что пользователю @mention с ботом. Если бот используется в нескольких сферах, таких как личные, groupchat или канал, необходимо определить, из какой области пришли сообщения бота, и обработать их соответствующим образом.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Разработка отличного бота для каналов или групп

Боты, добавленные в команду, становятся еще одним членом команды @mentioned быть использованы в рамках беседы. На самом деле, боты получают сообщения только тогда, @mentioned они находятся в интернете, поэтому другие разговоры на канале не отправляются боту.

Бот в группе или канале должен предоставлять информацию, соответствующую и соответствующую всем участникам. Хотя ваш бот, безусловно, может предоставить любую информацию, относящуюся к опыту, имейте в виду, разговоры с ним видны всем. Таким образом, большой бот в группе или канале должен добавить ценность для всех пользователей, и, конечно, не случайно обмениваться информацией, более подходящей для беседы один к одному.

Ваш бот, как и он есть, может быть полностью релевантным во всех сферах, не требуя дополнительной работы. В Microsoft Teams нет никаких ожиданий, что ваш бот функции во всех сферах, но вы должны убедиться, что ваш бот обеспечивает ценность пользователя в зависимости от сферы (ы) вы решите поддержать. Для получения дополнительной информации о сферах, [см. Приложения в Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).

Разработка бота, который работает в группах или каналах, использует большую часть той же функциональности, что и личные разговоры. Дополнительные события и данные в полезной нагрузке обеспечивают Teams группы и информации о канале. Эти различия, а также ключевые различия в общей функциональности описаны в следующих разделах.

### <a name="creating-messages"></a>Создание сообщений

Для получения дополнительной информации о ботах, создающих сообщения в [каналах, смотрите Proactive сообщения для ботов,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) [и, в частности, Создание канала разговор.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)

### <a name="receiving-messages"></a>Получение сообщений

Для бота в группе или канале, в дополнение к [обычной схеме сообщения,](https://docs.botframework.com/core-concepts/reference/#activity)ваш бот также получает следующие свойства:

* `channelData`Смотрите [Teams данные канала](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data). В групповом чате содержится информация, специфичная для этого чата.
* `conversation.id` Идентификатор цепочки ответов, состоящий из идентификатора канала плюс идентификатор первого сообщения в цепочке ответов.
* `conversation.isGroup` Для `true` бот-сообщений в каналах или групповых чатах.
* `conversation.conversationType` Либо `groupChat` `channel` или .
* `entities` Может содержать одно или несколько упоминаний. Для получения дополнительной информации [см.](#-mentions)

### <a name="replying-to-messages"></a>Ответ на сообщения

Чтобы ответить на существующее сообщение, [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) позвоните в .NET [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) или в Node.js. Bot Builder SDK обрабатывает все детали.

Если вы решите использовать API REST, вы также можете позвонить в [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) конечную точку.

В канале ответ на сообщение показывается как ответ на инициируя цепочку ответов. Содержит `conversation.id` идентификатор сообщения канала и верхнего уровня. Хотя Bot Framework заботится о деталях, вы можете кэшировать это для `conversation.id` будущих ответов на этот поток разговора по мере необходимости.

### <a name="best-practice-welcome-messages-in-teams"></a>Лучшая практика: Приветственные сообщения в Teams

Когда ваш бот впервые добавлен в группу или команду, как правило, полезно отправить приветственное сообщение, представляя бота всем пользователям. Приветственное сообщение должно предоставить описание функциональности бота и преимуществ пользователя. В идеале сообщение должно также включать команды для пользователя, чтобы взаимодействовать с приложением. Для этого убедитесь, что ваш бот реагирует на `conversationUpdate` сообщение, с `teamsAddMembers` eventType в `channelData` объекте. Убедитесь, что `memberAdded` идентификатор является идентификатором App ID бота, потому что то же самое событие отправляется, когда пользователь добавляется в команду. Для [получения более подробной информации смотрите дополнение к команде](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) или боту.

Вы также можете отправить личное сообщение каждому члену команды при добавлении бота. Для этого можно получить [список групп и отправить](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) каждому пользователю [прямое сообщение.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

Мы рекомендуем вашему *боту не* отправлять приветственное сообщение в следующих ситуациях:

* Команда большая (очевидно субъективная, например, более 100 членов). Ваш бот может рассматриваться как "спамми" и человек, который добавил его может получить жалобы, если вы четко сообщить ценностное предложение вашего бота для всех, кто видит приветственное сообщение.
* Ваш бот впервые упоминается в группе или канале, по сравнению с первым добавлением в команду.
* Группа или канал переименованы.
* Член команды добавляется в группу или канал.

## <a name="-mentions"></a>Упоминания

Поскольку боты в группе или канале отвечаюттолько тогда, когда они упоминаются в сообщении («бот-имя»), каждое сообщение, полученное ботом в групповом канале, содержит свое собственное имя, и вы должны убедиться, что ваше сообщение, анализ, обрабатывает это. Кроме того, боты могут анализировать других пользователей, упомянутых и упоминать пользователей как часть своих сообщений.

### <a name="retrieving-mentions"></a>Получение упоминаний

Упоминания возвращаются в объект `entities` полезной нагрузки и содержат как уникальный идентификатор пользователя, так и, в большинстве случаев, имя пользователя, упомянутого. Вы можете получить все упоминания в сообщении, позвонив `GetMentions` функции в Bot Builder SDK для .NET, который возвращает массив `Mentioned` объектов.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Пример .NET: Проверка и полоса @bot упоминания

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
> Вы также можете использовать функцию Teams `GetTextWithoutMentions` расширения, которая удаляет все упоминания, включая бота.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js пример: Проверьте и сыпьйте @bot упоминание

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

Вы также можете использовать функцию Teams `getTextWithoutMentions` расширения, которая удаляет все упоминания, включая бота.

### <a name="constructing-mentions"></a>Строительство упоминаний

Ваш бот может упоминать других пользователей в сообщениях, размещенных в каналах. Для этого ваше сообщение должно сделать следующее:

* Включите `<at>@username</at>` в текст сообщения.
* Включите `mention` объект в коллекцию сущностей.

#### <a name="net-example"></a>Пример .NET

В этом примере [используется пакет Microsoft.Bot.connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet microsoft.

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Пример: Исходящие сообщения с упомянутым пользователем

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

## <a name="accessing-groupchat-or-channel-scope"></a>Доступ к групповому чату или области канала

Ваш бот может делать больше, чем отправлять и получать сообщения в группах и группах. Например, он также может получить список участников, включая их информацию о профиле, а также список каналов. Для получения дополнительной [информации, см Получить контекст для вашего Microsoft Teams бота](~/resources/bot-v3/bots-context.md).

## <a name="see-also"></a>См. также

[Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
