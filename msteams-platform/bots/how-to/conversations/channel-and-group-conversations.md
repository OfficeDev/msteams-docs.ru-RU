---
title: Каналы и групповые беседы с ботом
author: clearab
description: Отправка, получение и обработка сообщений для бота в канале или групповом чате.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797843"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Беседы в каналах и групповых чатах с помощью бота Microsoft Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Добавляя область или область в бот, ее можно установить в групповом или `teams` `groupchat` командном чате. Это позволяет всем участникам беседы взаимодействовать с ботом. После установки он также получит доступ к метаданным беседы, например к списку участников беседы, а также при установке в команде сведений о команде и полного списка каналов.

Боты в группе или канале получают сообщения, только когда они упоминаются (@botname), они не получают других сообщений, отправленных в беседу.

> [!NOTE]
> Бот должен быть @mentioned непосредственно. Бот не получит сообщение, если команда или канал упомянуты, или когда кто-то отвечает на сообщение от вашего бота, не @mentioning его.

## <a name="design-guidelines"></a>Рекомендации по дизайну

Узнайте, как [разработать беседы ботов в каналах и чатах.](~/bots/design/bots.md)

## <a name="creating-new-conversation-threads"></a>Создание новых потоков беседы

При установке бота в команде иногда может быть необходимо создать цепочку бесед, а не отвечать на существующий. Это форма упреждающего [обмена сообщениями.](~/bots/how-to/conversations/send-proactive-messages.md)

## <a name="working-with-mentions"></a>Работа с упоминаниями

Каждое сообщение, отобратое боту из группы или канала, будет содержать @mention с собственным именем в тексте сообщения, поэтому вам потребуется убедиться, что личные работки обработки сообщений обрабатываются таким образом. Бот также может получить других пользователей, упомянутых в сообщении, и добавить упоминания в любые отправляемые сообщения.

### <a name="stripping-mentions-from-message-text"></a>Замещение упоминаний из текста сообщения

Возможно, вам потребуется @mentions из текста сообщения, которое получает бот.

### <a name="retrieving-mentions"></a>Искомые упоминания

Упоминания возвращаются в объекте в полезной нагрузке и содержат как уникальный ИД пользователя, так и, в большинстве случаев, имя `entities` упомянутого пользователя. Текст сообщения также будет включать упоминание, например `<at>@John Smith<at>` . Однако не следует полагаться на текст в сообщении для получения каких-либо сведений о пользователе; отправляя сообщение, он может изменить его. Вместо этого используйте `entities` объект.

Вы можете получить все упоминания в сообщении, вызывая функцию в SDK построитель ботов, которая возвращает `GetMentions` массив `Mention` объектов.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
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

# <a name="python"></a>[Python](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="adding-mentions-to-your-messages"></a>Добавление упоминаний в сообщения

Бот может упоминать других пользователей в сообщениях, которые были опубликованы в каналах. Для этого ваше сообщение должно сделать следующее:

У `Mention` объекта есть два свойства, которые необходимо настроить:

* Включить <at>@username</at> в текст сообщения
* Включить объект упоминания в коллекцию сущностями

SDK Bot Framework предоставляет дополнительные методы и объекты, упрощающие создание упоминания.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[JSON](#tab/json)

Поле в объекте массива должно точно `text` `entities` соответствовать части поля  `text` сообщения. Если этого не сделать, упоминание будет проигнорировано.

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
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

# <a name="python"></a>[Python](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

## <a name="sending-a-message-on-installation"></a>Отправка сообщения при установке

При первом добавлении бота в группу или команду может быть полезно отправить сообщение с его введением. В сообщении должно быть краткое описание функций бота и их использования. Вы захотите подписаться на `conversationUpdate` событие с помощью `teamMemberAdded` eventType.  Так как событие отправляется при добавлении нового участника группы, необходимо проверить, является ли новый участник ботом. Дополнительные [сведения см.](~/bots/how-to/conversations/send-proactive-messages.md) в сообщении о том, как отправить приветствие новому участнику группы.

Вы также можете отправить личное сообщение каждому участнику команды при добавлении бота. Для этого можно получить список команд и отправить каждому пользователю прямое сообщение.

Не рекомендуется отправлять сообщение в следующих ситуациях:

* Команда большая (очевидно, что она субъективна, но, например, более 100 участников). Ваш бот может быть виден как "спам", а добавлявший его пользователь может получить жалобы, если вы не ясно сообщаете о преимуществах вашего бота всем, кто видит приветствие.
* Ваш бот впервые упоминается в группе или канале (по сравнению с первым добавлением в команду)
* Группа или канал переименовываются
* Участник команды добавляется в группу или канал

## <a name="learn-more"></a>Подробнее

У бота есть доступ к дополнительным сведениям о групповом чате или команде, в которую он установлен. Дополнительные [API,](~/bots/how-to/get-teams-context.md) доступные для бота, см. в контексте команды.

Кроме того, бот может подписаться на дополнительные события и ответить на них. См. [подписку на события бесед,](~/bots/how-to/conversations/subscribe-to-conversation-events.md) чтобы узнать, как это сделать.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
