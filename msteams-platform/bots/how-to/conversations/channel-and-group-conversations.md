---
title: Телефонные и групповые беседы с ботом
author: clearab
description: Отправка, получение и обработка сообщений для бота в канале или групповом чате.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 2d7eece1fc74781456024f6dcb9414fefbadb8f4
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075754"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>Телефонные и групповые беседы в чате с ботом

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Чтобы установить бот Microsoft Teams в командном или групповом чате, добавьте область или область `teams` `groupchat` в бот. В результате все участники беседы взаимодействовать с вашим ботом. После установки бота он имеет доступ к метаданным о беседе, например к списку участников беседы. Кроме того, при установке в команде бот имеет доступ к сведениям об этой группе и полном списке каналов.

Боты в группе или канале получают сообщения только при `@botname` упоминаний. Они не получают никаких других сообщений, отправленных в беседу.

> [!NOTE]
> Бот должен быть `@mentioned` напрямую. Ваш бот не получает сообщение, когда команда или канал упоминаются, или когда кто-то отвечает на сообщение от вашего бота без @mentioning его.

## <a name="design-guidelines"></a>Рекомендации по дизайну

В отличие от личных чатов, в групповых чатах и каналах бот должен предоставить быстрое введение. Необходимо следовать этим и дополнительным рекомендациям по разработке ботов. Дополнительные сведения о разработке ботов в Teams см. в том, как создать беседы ботов [в каналах и чатах.](~/bots/design/bots.md)

Теперь вы можете создавать новые потоки бесед и легко управлять различными беседами в каналах.

## <a name="create-new-conversation-threads"></a>Создание новых потоков беседы

При установке бота в команде необходимо создать новый поток беседы, а не отвечать на существующий. Иногда трудно различать два разговора. Если беседа потоковая, проще организовать и управлять различными беседами в каналах. Это форма [активного обмена сообщениями.](~/bots/how-to/conversations/send-proactive-messages.md)

Далее можно получить упоминания с помощью объекта и добавить упоминания в `entities` сообщения с помощью `Mention` объекта.

## <a name="work-with-mentions"></a>Работа с упоминаниями

Каждое сообщение боту из группы или канала содержит @mention с его именем в тексте сообщения. Убедитесь, что обработка сообщений @mention. Кроме того, бот может получать другие пользователи, упомянутые в сообщении, и добавлять упоминания в любые сообщения, которые он отправляет.

Кроме того, необходимо @mentions из содержимого сообщения, которое получает бот.

### <a name="retrieve-mentions"></a>Извлечение упоминаний

Упоминания возвращаются в объекте в полезной нагрузке и содержат как уникальный ID пользователя, так и имя `entities` упомянутого пользователя. В тексте сообщения также содержится упоминание, например `<at>@John Smith<at>` . Однако не следует полагаться на текст в сообщении для получения сведений о пользователе. Это возможно для человека, отправляя сообщение, чтобы изменить его. Поэтому используйте `entities` объект.

Вы можете получить все упоминания в сообщении, позвонив функции в SDK Bot Builder, которая возвращает `GetMentions` массив `Mention` объектов.

В следующем коде показан пример упоминаний о том, как следующую возможность:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

### <a name="add-mentions-to-your-messages"></a>Добавление упоминаний в сообщения

Ваш бот может упоминать других пользователей в сообщениях, которые размещены в каналах.

Объект `Mention` имеет два свойства, которые необходимо установить, используя следующее:

* <at>Включи @username</at> в текст сообщения.
* Включай объект упоминания в коллекцию сущностями.

SDK Bot Framework предоставляет дополнительные методы и объекты для создания упоминаний.

В следующем коде показан пример добавления упоминаний в сообщения:

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Поле объекта в массиве должно `text` `entities` соответствовать части поля `text` сообщений. Если этого не происходит, упоминание игнорируется.

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

Теперь вы можете отправить сообщение о вводе при первом установке или добавлении бота в группу или группу.

## <a name="send-a-message-on-installation"></a>Отправка сообщения при установке

При первом добавлении бота в группу или группу необходимо отправить вводное сообщение. В сообщении должно быть краткое описание функций бота и их использования. Необходимо подписаться на `conversationUpdate` событие с `teamMemberAdded` помощью eventType.  Событие отправляется при добавлении любого нового члена команды. Проверьте, является ли добавленный новый участник ботом. Дополнительные сведения см. [в тексте отправки приветствия новому члену группы.](~/bots/how-to/conversations/send-proactive-messages.md)

Отправьте личное сообщение каждому члену группы при добавлении бота. Для этого получите список команд и отправьте каждому пользователю прямое сообщение.

Не отправлять сообщение в следующих случаях:

* Группа большая, например, более 100 участников. Ваш бот может рассматриваться как спам, а добавленный в него человек может получать жалобы. Необходимо четко донести предложение о ценности бота до всех, кто увидит приветствие.
* Сначала бот упоминается в группе или канале, а не в команде.
* Группа или канал переименованы.
* Член группы добавляется в группу или канал.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a>См. также

[Контекст Get Teams](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Подписка на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
