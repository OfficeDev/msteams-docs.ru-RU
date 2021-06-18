---
title: Отправка упреждающих сообщений
description: Описывает, как отправлять упреждающие сообщения с помощью бота Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: отправка сообщения получить ID-ID-ID канала для беседы
ms.openlocfilehash: 56411fe381a05318d0e12d6876cf26138baba42c
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994219"
---
# <a name="send-proactive-messages"></a>Отправка упреждающих сообщений

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Проактивное сообщение — это любое сообщение, отправленное ботом, которое не является ответом на запрос пользователя. Это может включать такие сообщения, как:

* Приветствия
* Уведомления
* Запланированные сообщения

Для того чтобы бот отправил проактивное сообщение пользователю, групповому чату или группе, он должен иметь доступ к отправке сообщения. Для группового чата или группы приложение с ботом должно быть сначала установлено в этом расположении. Вы можете активно устанавливать приложение с помощью [Microsoft Graph](#proactively-install-your-app-using-graph) в команде, если это необходимо, или использовать политику приложения для оттеснки приложений к группам и пользователям в клиенте. [](/microsoftteams/teams-custom-app-policies-and-settings) Для пользователей ваше приложение либо должно быть установлено для пользователя, либо пользователь должен быть частью команды, в которой установлено ваше приложение.

Отправка упреждающего сообщения отличается от обычного сообщения. Нет активного `turnContext` использования для ответа. Перед отправкой сообщения необходимо создать беседу. Например, новый чат один к одному или новый поток беседы в канале. Невозможно создать новый групповой чат или новый канал в команде с активной передачей сообщений.

**Отправка проактивного сообщения**

1. При необходимости получите пользовательский [ИД, командный или канал.](#get-the-user-id-team-id-or-channel-id)
1. [Создайте беседу,](#create-the-conversation)если потребуется.
1. [Получите ID беседы](#get-the-conversation-id).
1. [Отправка сообщения](#send-the-message).

Фрагменты кода в разделе [примеры](#samples) для создания беседы один к одному. Ссылки на полные рабочие примеры для бесед и групп или каналов см. в [примере кода.](#code-sample)

Для эффективного использования упреждающих сообщений см. [в переупреждающихся практиках для активного обмена сообщениями.](#best-practices-for-proactive-messaging) Для определенных сценариев необходимо активно установить приложение с [помощью Graph.](#proactively-install-your-app-using-graph) Фрагменты кода в разделе [примеры](#samples) для создания беседы один к одному. Полные рабочие примеры для бесед и групп или каналов см. в [примере кода.](#code-sample)

## <a name="get-the-user-id-team-id-or-channel-id"></a>Получите пользовательский ИД, командный или каналный ИД

Чтобы создать новый поток беседы или беседы в канале, необходимо иметь правильный ID. Вы можете получить или получить этот ID с помощью любого из следующих ниже.

* Когда ваше приложение установлено в любом конкретном контексте, вы получаете [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* При добавлении нового пользователя в контекст, в котором установлено приложение, вы получаете [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в команде, где установлено ваше приложение.
* Вы можете получить [список членов группы,](~/bots/how-to/get-teams-context.md) в которой установлено ваше приложение.
* Каждое действие, получаемые ботом, должно содержать необходимые сведения.

Независимо от того, как вы получаете информацию, необходимо сохранить или создать `tenantId` `userId` новый `channelId` разговор. Вы также можете использовать этот поток для создания нового потока беседы в общем или по умолчанию `teamId` канале группы.

Уникальный `userId` для вашего бот-ИД и определенного пользователя. Нельзя повторно использовать между `userId` ботами. `channelId`Глобальный. Однако перед отправкой проактивного сообщения на канал необходимо установить бот в команде.

После получения сведений о пользователе или канале необходимо создать беседу.

## <a name="create-the-conversation"></a>Создание беседы

Вы должны создать беседу, если она не существует или вы не знаете `conversationId` . Необходимо создать беседу только один раз и сохранить `conversationId` значение или `conversationReference` объект.

После создания беседы необходимо получить ID беседы.

## <a name="get-the-conversation-id"></a>Получить ID беседы

Используйте объект `conversationReference` или `conversationId` отправить `tenantId` сообщение. Этот ID можно получить, создав беседу или храня ее из любого действия, отправленного вам из этого контекста. Храните этот ID для справки.

После получения соответствующей адресной информации можно отправить сообщение.

## <a name="send-the-message"></a>Отправка сообщения

Теперь, когда у вас есть правильные сведения о адресе, вы можете отправить свое сообщение. Если вы используете SDK, необходимо использовать метод, а также и сделать `continueConversation` `conversationId` `tenantId` прямой вызов API. Чтобы успешно отправить сообщение, необходимо правильно `conversationParameters` установить. См. [раздел примеры](#samples) или используйте один из примеров, перечисленных в [примере](#code-sample) кода.

Теперь, когда вы отправили проактивное сообщение, вы должны следовать этим лучшим практикам, отправляя проактивные сообщения для улучшения обмена информацией между пользователями и ботом.

## <a name="best-practices-for-proactive-messaging"></a>Лучшие практики для активного обмена сообщениями

Отправка активных сообщений пользователям — это очень эффективный способ общения с пользователями. Однако с их точки зрения это сообщение может отображаться совершенно незащищенным, и в случае приветствия сообщений это первый раз, когда они взаимодействуют с вашим приложением. Поэтому очень важно использовать упреждающий обмен сообщениями, а не нежелательной почты пользователей, а также предоставлять достаточно информации, чтобы пользователи могли понять, почему они получают сообщения.

### <a name="welcome-messages"></a>Приветствия

Если для отправки приветствия пользователю используется проактивный обмен сообщениями, нет контекста, по которым пользователи получают сообщение. Кроме того, пользователи впервые взаимодействуют с вашим приложением. Это возможность создать хорошее первое впечатление. Лучшие приветствия должны включать в себя:

* Почему пользователь получает сообщение: пользователю должно быть ясно, почему он получает сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.
* Что вы предлагаете. Пользователи должны быть в состоянии определить, что они могут сделать с вашим приложением и какое значение вы можете принести к ним.
* Что они должны делать дальше: предложить пользователям опробовать команду или взаимодействовать с приложением.

Неудовлетворительные приветствия могут привести к блокировке бота пользователями. Напишите в точку и ясно приветствуя сообщения. Итерировать на приветствие сообщений, если они не имеют желаемого эффекта.

### <a name="notification-messages"></a>Уведомления

Чтобы отправлять уведомления с помощью активного обмена сообщениями, убедитесь, что у пользователей есть четкий путь к общим действиям на основе вашего уведомления. Убедитесь, что у пользователей есть четкое представление о том, почему они получили уведомление. Хорошие сообщения уведомлений обычно включают в себя следующие:

* Что произошло: четкое указание на то, что стало причиной уведомления.
* Каков был результат: необходимо четко знать, какой элемент был обновлен, чтобы вызвать уведомление.
* Кто или что вызвало его: кто или какие действия привели к отправлению уведомления.
* Что пользователи могут сделать в ответ: у вас будет легко принимать меры на основе уведомлений.
* Как пользователи могут отказаться от этого. Необходимо предоставить пользователям путь к отказу от дополнительных уведомлений.

Для отправки сообщений большой группе пользователей, например в организацию, упреждайте установку приложения с помощью Graph.

### <a name="scheduled-messages"></a>Запланированные сообщения

При использовании активных сообщений для отправки запланированных сообщений пользователям убедитесь, что часовой пояс обновляется до часового пояса. Это обеспечивает доставку сообщений пользователям в соответствующее время. Расписание сообщений обычно включает в себя:

* Почему пользователь получает сообщение: чтобы пользователям было легко понять причину получения сообщения.
* Что может сделать пользователь далее: пользователи могут принять необходимые действия на основе контента сообщения.

## <a name="proactively-install-your-app-using-graph"></a>Активная установка приложения с помощью Graph

> [!Note]
> Активная установка приложений с помощью Graph в настоящее время находится в бета-версии.

Активно сообщайте пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением. Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. В этом случае для активной установки приложения для пользователей можно использовать API Graph. Кэшйте необходимые значения из события, которое `conversationUpdate` ваше приложение получает при установке.

Можно установить только приложения, которые находятся в каталоге организационных приложений или в Магазине приложений Teams.

Об [установке приложений для пользователей см. в](/graph/api/userteamwork-post-installedapps) документации Graph, а также в упреждающих установках ботов и обмена сообщениями [в Teams with Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) На платформе GitHub также имеется пример фреймворка [Microsoft.NET.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)

## <a name="samples"></a>Примеры

В следующем коде показан простой пример кода, который активно устанавливает приложение с помощью Graph:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Необходимо предоставить пользовательский ИД и ИД клиента. Если вызов удался, API возвращает следующий объект ответа:

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

> [!NOTE]
> В настоящее время боты не могут создавать групповой чат с помощью API или Graph. `createConversation` доступен только для чатов 1:1.

## <a name="code-sample"></a>Пример кода

В следующей таблице приводится простой пример кода, который включает основной поток беседы в приложение Teams и способ создания нового потока беседы в канале в Teams:

| **Имя образца** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Teams Основы беседы  | Демонстрирует основы бесед в Teams, в том числе отправку одно к одному упреждающих сообщений.| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Запуск нового потока в канале | Демонстрирует создание нового потока в канале. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a>Дополнительный пример кода

> [!div class="nextstepaction"]
> [Teams примеры кода проактивных сообщений](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="see-also"></a>См. также

[**Teams примеры кода проактивных сообщений**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Формат сообщений бота](~/bots/how-to/format-your-bot-messages.md)
