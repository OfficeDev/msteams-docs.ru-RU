---
title: Беседы с ботами в канале и группе
author: surbhigupta
description: Как отправлять, получать и обрабатывать сообщения для бота в канале или групповом чате. Статья содержит сведения о рекомендациях по проектированию, создании потоков беседы, использовании @упоминаний и примеры программного кода
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 6b3adf491ccfed2401308f0b6d283047f24f91e2
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757180"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>Беседы с бото в канале и групповом чате

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Чтобы установить Microsoft Teams бота в чате группы или команды, добавьте боту область `teams` или `groupchat`. В результате все участники беседы взаимодействовать с вашим ботом. После установки бот получает доступ к метаданным беседы, например к списку участников. Кроме того, при установке в команде бот получает доступ к сведениям об этой команде и полному списку каналов.

Боты в группе или канале получают сообщения только при упоминаемых @botname. Другие сообщения, отправленные в беседу, не отправляются. Бот должен быть @упомянут непосредственно. Бот не получает сообщение, когда упоминается команда или канал, или когда кто-то отвечает на сообщение от бота, @mentioning его.

> [!NOTE]
> В настоящее время эта функция предлагается только в [общедоступной предварительной версии для разработчиков](../../../resources/dev-preview/developer-preview-intro.md).
>
> Используя согласие для конкретного ресурса (RSC), боты могут получать все сообщения каналов в командах, в которых они установлены, даже без @упоминания. Дополнительные сведения см. в статье [Получение всех сообщений канала с помощью RSC](channel-messages-with-rsc.md).
>
> Публикация сообщений или адаптивных карточек в частном канале в настоящее время не поддерживается.

## <a name="design-guidelines"></a>Рекомендации по дизайну

В отличие от личных чатов, в групповых чатах и каналах бот после добавления должен кратко представиться. Обязательно следуйте этим и другим рекомендациям по проектированию ботов. Подробнее о разработке ботов в Teams см. в статье[ Проектирование бесед ботов в каналах и чатах](~/bots/design/bots.md).

Теперь вы можете создавать новые цепочки бесед и легко управлять различными беседами в каналах.

## <a name="create-new-conversation-threads"></a>Создание цепочки беседы

При установке бота в команде необходимо создать новый поток беседы, а не отвечать на существующий. Иногда трудно различать две беседы. Если беседа является потоковой, проще упорядочить различные беседы и управлять ими в каналах. Это форма [упреждающего обмена сообщениями](~/bots/how-to/conversations/send-proactive-messages.md).

Затем можно получить упоминания с помощью объекта `entities` и добавить упоминания в сообщения с помощью объекта `Mention`.

## <a name="work-with-mentions"></a>Работа с @упоминаниями

Каждое сообщение боту из группы или канала будет содержать @упоминание с его именем в тексте сообщения. Бот также может получать имена других пользователей, упоминаемых в таких сообщениях, и добавлять упоминания во все отправляемые им сообщения.

Иногда бывает необходимо выделить @упоминания из текста сообщения, которое получает бот.

### <a name="retrieve-mentions"></a>Получение упоминаний

Упоминания возвращаются в полезных данных объекта `entities` и содержат как уникальный ИД пользователя, так и имя упомянутого пользователя. Текст сообщения также содержит упоминание, например `<at>@John Smith<at>`. Однако не следует полагаться на текст в сообщении для получения сведений о пользователе. Пользователь, отправляющий сообщение, может изменить его. Поэтому используйте объект `entities`.

Вы можете получить все упоминания в сообщении, вызвав функцию `GetMentions` в пакете SDK Bot Builder, которая возвращает массив объектов `Mention`.

В следующем фрагменте программного кода показан пример получения упоминаний:

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

Бот может упоминать других пользователей в сообщениях, опубликованных в каналах.

Объект `Mention` имеет два свойства, которые необходимо задать с помощью следующих элементов:

* Включите *@имя_пользователя* в текст сообщения.
* Включите объект упоминания в коллекцию сущностей.

Пакет SDK Bot Framework предоставляет вспомогательные методы и объекты для создания упоминаний.

В следующем фрагменте программного кода показан пример добавления упоминаний в сообщения:

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

Поле `text` в объекте в массиве `entities` должно соответствовать части поля сообщения `text`. Если это не так, упоминание игнорируется.

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

Теперь ваш бот может представиться при первой установке или добавлении в группу или команду.

## <a name="send-a-message-on-installation"></a>Отправка сообщения при установке

При первом добавлении бота в группу или команду необходимо отправить начальное приветственное сообщение. Сообщение должно содержать краткое описание функций бота и способы их использования. Необходимо подписаться на событие `conversationUpdate` с помощью eventType `teamMemberAdded`.  Событие отправляется при добавлении нового участника команды. Проверьте, является ли добавленный новый участник ботом. Подробнее см. в статье [Отправка приветственного сообщения новому участнику команды](~/bots/how-to/conversations/send-proactive-messages.md).

При добавлении бота отправьте личное сообщение каждому участнику команды. Для этого получите список личного состава команды и отправьте каждому участнику прямое сообщение.

Не отправляйте сообщение в следующих случаях:

* Команда большая, например, более 100 участников. Бот может быть сочтен распространителем спама, а пользователь, который добавил его, может получать жалобы. Необходимо четко сообщить о полезности бота всем, кто видит приветственное сообщение.
* Бот упоминается в группе или канале раньше, чем добавлен в команду.
* Группа или канал переименованы.
* Участник команды добавляется в группу или канал.

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговым инструкциям](../../../sbs-teams-conversation-bot.yml) по созданию бота беседы Teams.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Подписка на события беседы](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="see-also"></a>Дополнительные ресурсы

[Получение контекста в Teams](~/bots/how-to/get-teams-context.md).
