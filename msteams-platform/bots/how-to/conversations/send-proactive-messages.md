---
title: Отправлять активные сообщения
author: clearab
description: Отправка активных сообщений с помощью робота Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874851"
---
# <a name="send-proactive-messages"></a>Отправлять активные сообщения

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Упреждающее сообщение — это любое сообщение, отправляемое сервером-роботом, которое не находится в прямом ответе на запрос пользователя. Сюда могут относиться такие сообщения, как:

* Приветственные сообщения
* Уведомления
* Запланированные сообщения

Чтобы ваш робот мог отправлять упреждающее сообщение, он должен иметь доступ к пользователю, группе или группе, которым вы хотите отправить сообщение. Для группового чата или команды это означает, что приложение, которое содержит ваш Bot, должно быть сначала установлено в этом расположении. Вы можете принудительно [установить приложение с помощью Graph](#proactively-install-your-app-using-graph) в группе, если это необходимо, или использовать [политику приложений](/microsoftteams/teams-custom-app-policies-and-settings) для передачи приложений в Teams и пользователей в клиенте. Для пользователей ваше приложение необходимо установить для этого пользователя, или пользователь должен входить в группу, в которой установлено приложение.

Отправка упреждающего сообщения отличается от отправки обычного сообщения в том случае, если вы не будете использовать активное сообщение `turnContext` для ответа. Кроме того, перед отправкой сообщения вам может потребоваться создать беседу (например, новый чат "один к одному" или "новый поток бесед в канале"). Вы не можете создать новый чат группы или новый канал в команде "активные системы обмена сообщениями".

На высоком уровне описаны действия, которые необходимо выполнить для отправки упреждающего сообщения:

1. [Получение идентификатора пользователя или группы или канала](#get-the-user-id-or-teamchannel-id) (при необходимости).
1. [Создайте обсуждение или](#create-the-conversation) цепочку сообщений (при необходимости).
1. [Получение идентификатора беседы](#get-the-conversation-id).
1. [Отправьте сообщение](#send-the-message).

Фрагменты кода, приведенные в разделе " [примеры](#examples) ", предназначены для создания беседы "один к одному", в разделе " [ссылки](#references) " приведены ссылки на готовые рабочие примеры для бесед и групп и каналов "один к одному".

## <a name="get-the-user-id-or-teamchannel-id"></a>Получение идентификатора пользователя или группы или канала

Если вам нужно создать новую беседу или цепочку бесед в канале, сначала необходимо получить правильный идентификатор для создания беседы. Вы можете получить или получить этот идентификатор несколькими способами:

1. Когда приложение устанавливается в каком-либо конкретном контексте, вы получите [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Когда новый пользователь добавляется в контекст, в котором установлено приложение, вы получите [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в группе, в которой установлено приложение.
1. Вы можете получить [список членов](~/bots/how-to/get-teams-context.md) группы, установленной на вашем приложении.
1. Все действия, получаемые с помощью Bot, будут содержать необходимые сведения.

Вне зависимости от того, как вы получаете информацию, вам потребуется хранить `tenantId` и один из, `userId` или, `channelId` чтобы создать новую беседу. Вы также можете использовать `teamId` для создания нового обсуждения в разделе Общие/по умолчанию в канале команды.

`userId`Уникально для идентификатора ленты и определенного пользователя, их нельзя повторно использовать в Боты. `channelId`Является глобальным, однако для отправки упреждающего сообщения каналу _необходимо_ установить его в команде.

## <a name="create-the-conversation"></a>Создание беседы

После получения сведений о пользователе и канале необходимо создать беседу, если она еще не существует (или вы не знаете `conversationId` ). Беседа следует создавать только один раз; обязательно сохраните `conversationId` значение или `conversationReference` объект для использования в будущем.

## <a name="get-the-conversation-id"></a>Получение идентификатора беседы

После создания беседы вы будете использовать `conversationReference` объект, `conversationId` а также и объект `tenantId` для отправки сообщения. Этот идентификатор можно получить с помощью создания беседы или сохранения его из любого действия, отправленного Вам из этого контекста. Убедитесь, что этот идентификатор хранится.

## <a name="send-the-message"></a>Отправка сообщения

Теперь, когда у вас есть нужные сведения об адресе, вы можете отправить сообщение. Если вы используете пакет SDK, то можете использовать этот `continueConversation` метод, а также выполнить `conversationId` `tenantId` прямой вызов API.  Вам потребуется `conversationParameters` правильно настроить успешную отправку сообщения — просмотрите [примеры](#examples) ниже или воспользуйтесь одним из примеров, приведенных в разделе " [ссылки](#references) ".

## <a name="best-practices-for-proactive-messaging"></a>Рекомендации по использованию упреждающего обмена сообщениями

Отправка упреждающих сообщений пользователям может быть очень эффективным способом общения с пользователями. Однако с точки зрения это сообщение может быть полностью нежелательным и, в случае приветственных сообщений, будет использоваться при первом взаимодействии с приложением. Таким образом, очень важно использовать эту функцию экономно (не спама для пользователей) и предоставить достаточно информации, чтобы пользователи могли понимать, почему они помещаются в сообщениях.

### <a name="welcome-messages"></a>Приветственные сообщения

При использовании упреждающего обмена сообщениями для отправки пользователю приветственного сообщения необходимо помнить, что для большинства пользователей, получивших сообщение, не будет контекста для их получения. Это также происходит в первый раз, когда он будет взаимодействовать с вашим приложением; можно создать хорошее первое впечатление. Лучшие приветственные сообщения будут включать:

* **Почему пользователь получает сообщение.** Он должен быть очень очевидным, чтобы пользователь получал сообщение. Если ваш Bot был установлен в канале и вы отправили приветственное сообщение всем пользователям, сообщите им о том, в каком канале он был установлен и кто его установил.
* **Что вы предоставляете.** Что можно делать с приложением? Какое значение можно перенести?
* **Что делать дальше.** Пригласите их, чтобы испытать команду или взаимодействовать с приложением каким бы то ни было способом.

Помните, что неудачные приветственные сообщения могут приводить к блокированию ленты. Вы должны тратить много времени на создание приветственных сообщений и перебирать их, если это не оказывает желаемого результата.

### <a name="notification-messages"></a>Сообщения уведомления

При использовании упреждающего обмена сообщениями для отправки уведомлений необходимо убедиться, что у пользователей есть четко заданный путь, чтобы выполнять общие действия на основе уведомления и ясно понять, почему возникло уведомление. К хорошим сообщениям уведомления обычно относятся:

* **Что случилось.** Четкое указание того, что произошло с причиной уведомления.
* **Каков результат.** Должно быть ясно, какие элементы/вещи были обновлены, чтобы получить уведомление.
* **Кто/что активировал его.** Кто или что приняло действие, вызвавшее отправку уведомления.
* **Что может делать пользователи в ответе.** Облегчить пользователям выполнение действий в соответствии с вашими уведомлениями.
* **Как пользователи могут отказаться.** Необходимо указать путь для пользователей, чтобы отказаться от дополнительных уведомлений.

## <a name="proactively-install-your-app-using-graph"></a>Заактивная установка приложения с помощью Graph

> [!Note]
> Активная установка приложений с помощью Microsoft Graph в настоящее время находится на стадии бета-тестирования.

Иногда это может потребоваться для упреждающего сообщения пользователей, которые ранее не устанавливали приложение или не работали с ним. Например, вы хотите использовать [Communicator компании](~/samples/app-templates.md#company-communicator) для отправки сообщений во всю организацию. В этом сценарии можно использовать API Graph для профилактической установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое `conversationUpdate` получит ваше приложение после установки.

Вы можете устанавливать только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.

Ознакомьтесь с разделом [Установка приложений для пользователей](/graph/teams-proactive-messaging) в документации Graph, а также об [активных установках и обмене сообщениями в Teams с Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). Кроме того, на платформе GitHub существует [пример Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  .

## <a name="examples"></a>Примеры

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[JSON](#tab/json)

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

Необходимо указать идентификатор пользователя и идентификатор клиента. Если вызов завершается успешно, API возвращает следующий объект Response.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="references"></a>Ссылки

Ниже приведены официальные примеры профилактического упреждающего обмена сообщениями.

|  Нет.  | Имя примера           | Описание                                                                      | .NET    | JavaScript   | Python  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|57|Основные сведения о беседах Teams  | Демонстрируются основные принципы бесед в Microsoft Teams, включая отправку одного и того же упреждающего сообщения.|[&nbsp;Ядро .NET](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|58|Запуск нового потока в канале     | Демонстрация создания нового потока в канале. |[&nbsp;Ядро .NET](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

В приведенном ниже примере показано минимальное количество сведений, необходимых для отправки упреждающего сообщения (без использования `conversationReference` объекта). Этот пример может быть полезен, если вы используете вызовы REST API напрямую или не сохраняли полные `conversationReference` объекты.

* [Активные системы обмена сообщениями Teams](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a>Просмотр дополнительного кода
>
> [!div class="nextstepaction"]
> [**Примеры кода для активных сообщений Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>