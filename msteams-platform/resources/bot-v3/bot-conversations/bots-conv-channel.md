---
title: Беседы в каналах и группах для общения с Боты
description: Описывает сквозной сценарий, в котором беседа с Bot в канале в Microsoft Teams
keywords: сценарии команд каналы ленты
ms.date: 06/25/2019
ms.openlocfilehash: 168abd1e3894b95983eec01541d470f1b5384a66
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675220"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Беседы в каналах и группах для общения с помощью робота Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams позволяет пользователям перенести боты в беседы по каналам или группового чата. Добавляя робота в группу или чат, все пользователи беседы могут воспользоваться всеми преимуществами функции Bot в беседе. Вы также можете получать доступ к функциям, зависящим от Teams, в вашей почтовой среде, запрашивают сведения о команде и @mentioning пользователей.

Чат в каналах и беседах групп отличается от личного разговора тем, что пользователь должен @mention Bot. Если используется в нескольких областях (личное, groupchat или Channel), необходимо определить область, из которой поступило сообщение Bot, и обработать их соответствующим образом.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Разработка отличного канала Bot для каналов или групп

Боты, добавленный в команду, становится другим участником группы, который может быть @mentioned в составе беседы. На самом деле Боты получают сообщения только при @mentioned, поэтому другие беседы по каналу не отправляются в Bot.

> [!NOTE]
> Для удобства при ответе на сообщения Bot в канале имя Bot добавляется в поле создать сообщение автоматически.

В группе или канале Bot должна предоставляться информация, соответствующая всем участникам. В то время как ваш Bot может предоставить любую информацию, относящуюся к опыту, следует учитывать, что беседы видны всем пользователям. Таким образом, с помощью удобного обмена сведениями в группе или канале может быть достаточно добавить значение ко всем пользователям и, безусловно, непреднамеренно использовать информацию в беседе "один к одному".

Ваш робот может быть полностью связан со всеми областями как есть, и не требуется значительных дополнительных действий, чтобы ваш робот мог работать над ними. В Microsoft Teams не предполагается, что функция Bot во всех областях, но вы должны убедиться, что у ленты есть пользовательское значение в любой области, которую вы выбрали для поддержки. Для получения дополнительных сведений об областях обратитесь к разделу [приложения в Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).

Разработка ленты, которая работает в группах или каналах, использует многие функции личных бесед. Дополнительные события и данные в полезных данных содержат сведения о группах и каналах Teams. Эти отличия, а также ключевые отличия в общих функциональных возможностях описаны в следующих разделах.

### <a name="creating-messages"></a>Создание сообщений

Дополнительные сведения о Боты создании сообщений в каналах см в статье [Active Messaging for Боты](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)и специальном [создании беседы с каналом](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).

### <a name="receiving-messages"></a>Получение сообщений

В дополнение к [схеме обычных сообщений](https://docs.botframework.com/core-concepts/reference/#activity)для Bot в группе или канале Bot также получают следующие свойства:

* `channelData`Ознакомьтесь с [данными канала Teams](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data). В сеансе групповой беседы содержит сведения, относящиеся к этому разговору.
* `conversation.id`ИДЕНТИФИКАТОР цепочки ответа, состоящий из идентификатора канала и идентификатора первого сообщения в цепочке ответа.
* `conversation.isGroup`Предназначено `true` для сообщений Bot в каналах или групповых беседах
* `conversation.conversationType`Один `groupChat` или`channel`
* `entities`Может содержать одно или несколько упоминаний (см. [упоминание](#-mentions))

### <a name="replying-to-messages"></a>Ответ на сообщения

Чтобы ответить на существующее сообщение, вызовите [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) его в .NET [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) или Node. js. Пакет SDK построителя построителя обрабатывает все подробные сведения.

Если вы решили использовать REST API, вы также можете вызвать [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) конечную точку.

В канале ответ на сообщение отображается как ответ на инициированную цепь ответа. `conversation.id` Содержит канал и идентификатор сообщения верхнего уровня. Несмотря на то, что `conversation.id` у Bot Framework есть сведения, вы можете кэшировать их для будущих ответов на этот поток беседы по мере необходимости.

### <a name="best-practice-welcome-messages-in-teams"></a>Советы и рекомендации: приветственные сообщения в Teams

При первом добавлении ленты в группу или команду, как правило, полезно отправить приветственное сообщение для всех пользователей. Приветственное сообщение должно содержать описание функции и преимуществ пользователя Bot. В идеале сообщение также должно включать команды для взаимодействия пользователя с приложением. Для этого необходимо убедиться, что в `conversationUpdate` `teamsAddMembers` `channelData` объекте Bot реагирует на сообщение с параметром EventType в объекте. Убедитесь, что `memberAdded` идентификатор является СОБСТВЕНно идентификатором приложения-робота, так как при добавлении пользователя в команду отправляется то же самое событие. Дополнительные сведения см. в разделе " [участник группы" или "Добавление ленты](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) ".

Кроме того, вы можете отправить личное сообщение каждому участнику команды при добавлении ленты. Для этого вы можете получить список [команд](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) и отправить каждому пользователю [прямое сообщение](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

*Не* рекомендуется отправлять приветственное сообщение в следующих ситуациях:

* Команда является большой (субъективно субъективна, но например, более 100 членов). Ваш робот может отображаться как "нежелательный", а пользователь, который добавил его, может получать жалобу, если вы не хотите явно сообщить о значении для пользователя, который видит приветственное сообщение.
* Первый из них упоминается в группе или канале (в отличие от первого добавления в группу).
* Переименование группы или канала
* Участник группы добавляется в группу или канал

## <a name="-mentions"></a>@ Упоминания

Так как боты в группе или канале отвечают только на то, что они упоминаются ("@_ботнаме_") в сообщении, каждое сообщение, полученное в канале группы "bot", содержит собственное имя, и вы должны убедиться в том, что дескрипторы синтаксического анализа сообщений. Кроме того, Боты может проанализировать других пользователей, упомянутых и упомянутых пользователям, в составе своих сообщений.

### <a name="retrieving-mentions"></a>Получение упоминаний

Упоминания возвращаются в `entities` объекте полезных данных и содержат как уникальный идентификатор пользователя, так и, в большинстве случаев, имя пользователя, указанное пользователем. Вы можете получить все упоминания в сообщении, вызвав `GetMentions` функцию в пакете SDK построителя построителя для .NET, которая возвращает массив `Mentioned` объектов.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Пример кода .NET: Поиск и чередование @bot упоминаний

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
> Вы также можете использовать функцию `GetTextWithoutMentions`расширения Teams, которая выполнит все упоминания, включая Bot.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Пример кода Node. js: Поиск и чередование @bot упоминаний

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

Вы также можете использовать функцию `getTextWithoutMentions`расширения Teams, которая выполнит все упоминания, включая Bot.

### <a name="constructing-mentions"></a>Создание упоминаний

Ваш Bot может заупоминаниь других пользователей в сообщениях, размещенных в каналах. Для этого сообщение должно выполнить следующие действия:

* Включить `<at>@username</at>` в текст сообщения
* Включение `mention` объекта в коллекцию сущностей

#### <a name="net-example"></a>Пример .NET

В этом примере используется пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Пример Node. js

В этом примере используется пакет NPM [ботбуилдер — Teams](https://www.npmjs.com/package/botbuilder-teams) .

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Пример: исходящее сообщение с указанным пользователем

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

## <a name="accessing-groupchat-or-channel-scope"></a>Доступ к области groupChat или канала

Ваш робот может выполнять больше, чем отправлять и получать сообщения в группах и в Teams. Например, он также может получить список элементов, включая сведения о их профилях, а также список каналов. Чтобы узнать больше, ознакомьтесь со [статьей получение контекста для робота Microsoft Teams](~/resources/bot-v3/bots-context.md) .
