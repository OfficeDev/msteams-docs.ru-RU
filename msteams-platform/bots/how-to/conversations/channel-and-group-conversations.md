---
title: Канал и групповые разговоры
author: clearab
description: Отправка, получение и обработка сообщений для программы Bot в канале или группе чата.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ccc27d7638820cfa3c2b7cfe12b91b3a3a9fef1d
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/31/2020
ms.locfileid: "44801525"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Беседы в каналах и группах для общения с помощью робота Microsoft Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Добавление `teams` `groupchat` области или области к интерфейсу робота может быть доступна для установки в команде или группе чата. Это позволяет всем участникам беседы взаимодействовать с роботом. После установки он также будет иметь доступ к метаданным беседы, как к списку участников беседы, а также при установке в группе сведений о команде и полном списке каналов.

Боты в группе или канале получать сообщения только при их упоминании ("@botname"), они не получают никаких других сообщений, отправляемых в беседу.

> [!NOTE]
> Bot должен быть @mentioned напрямую. Программа-робот не получает сообщение при упоминании команды или канала, а также когда кто-то отвечает на сообщение от пользователя Bot, не @mentioning его.

## <a name="design-considerations"></a>Особенности дизайна

Bot должен предоставлять сведения, которые соответствуют всем участникам группы или канала. Беседы с ним видны всем, которые являются частью группы или канала. С помощью хорошо спроектированного почтового робота можно добавить значение ко всем пользователям, не создавая при этом непреднамеренное совместное использование информации в беседе "один к одному". Для сбора информации в беседах, таких как диалоговые окна, следует избегать использования карточек и/или модулей задач.

## <a name="creating-new-conversation-threads"></a>Создание новых потоков беседы

При установке ленты в команду иногда может потребоваться создать новый поток бесед, а не отвечать на него. Это форма [упреждающего обмена сообщениями](~/bots/how-to/conversations/send-proactive-messages.md).

## <a name="working-with-mentions"></a>Работа с упоминаниями

Каждое сообщение для ленты из группы или канала будет содержать @mention с собственным именем в тексте сообщения, поэтому необходимо убедиться, что маркеры синтаксического анализа сообщения. С помощью Bot можно также получить других пользователей, упомянутых в сообщении, и добавить упоминания в сообщения, которые он отправляет.

### <a name="stripping-mentions-from-message-text"></a>Удаление упоминаний из текста сообщения

Может потребоваться изъять @mentions из текста сообщения, полученного от ленты.

### <a name="retrieving-mentions"></a>Получение упоминаний

Упоминания возвращаются в `entities` объекте полезных данных и содержат как уникальный идентификатор пользователя, так и, в большинстве случаев, имя пользователя, указанное пользователем. Текст сообщения также будет содержать упоминание о том, как `<at>@John Smith<at>` . Тем не менее, не следует полагаться на текст в сообщении, чтобы получить сведения о пользователе; пользователь, отправивший сообщение, может изменить его. Вместо этого используйте `entities` объект.

Вы можете получить все упоминания в сообщении, вызвав `GetMentions` функцию в пакете SDK построителя ленты, которая возвращает массив `Mention` объектов.

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

### <a name="adding-mentions-to-your-messages"></a>Добавление упоминания к сообщениям

Ваш Bot может заупоминаниь других пользователей в сообщениях, размещенных в каналах. Для этого сообщение должно выполнить следующие действия:

У `Mention` объекта есть два свойства, которые необходимо задать:

* Включение <at>@username</at> в текст сообщения
* Добавление объекта упоминаемого объекта в коллекцию сущностей

Пакет SDK для ленты предоставляет вспомогательные методы и объекты для упрощения создания упоминания.

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

`text`Поле в объекте в `entities` массиве должно *точно* соответствовать части `text` поля сообщения. В противном случае упоминание будет игнорироваться.

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

При первом добавлении ленты в группу или группу может быть полезно отправить сообщение. Сообщение должно содержать краткое описание функций и их использования. Вы хотите подписаться на `conversationUpdate` событие с помощью `teamMemberAdded` EventType.  Так как событие отправляется при добавлении нового члена группы, необходимо проверить, добавлен ли новый член Bot. Узнайте больше о том, как [Отправить приветственное сообщение новому участнику группы](~/bots/how-to/conversations/send-proactive-messages.md) .

Кроме того, вы можете отправить личное сообщение каждому участнику команды при добавлении ленты. Для этого вы можете получить список участников команды и отправить ему прямое сообщение.

Не рекомендуется отправлять сообщения в следующих ситуациях:

* Команда является большой (субъективно субъективна, но например, более 100 членов). Ваш робот может отображаться как "нежелательный", а пользователь, который добавил его, может получать жалобу, если вы не хотите явно сообщить о значении для пользователя, который видит приветственное сообщение.
* Первый из них упоминается в группе или канале (в отличие от первого добавления в группу).
* Переименование группы или канала
* Участник группы добавляется в группу или канал

## <a name="learn-more"></a>Подробнее

У вас есть доступ к дополнительным сведениям о групповой беседе или группе, в которой он установлен. Ознакомьтесь с [контекстом Get Teams](~/bots/how-to/get-teams-context.md) , чтобы получить дополнительные API, доступные для ленты.

Кроме того, существуют дополнительные события, на которые может подписаться и реагировать ваш робот. Узнайте, как [подписаться на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md) .

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
