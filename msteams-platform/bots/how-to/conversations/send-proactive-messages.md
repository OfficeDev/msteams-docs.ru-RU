---
title: Отправка упреждающих сообщений
description: В этой статье описано, как отправлять упреждающие сообщения с помощью бота Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: high
Keywords: отправить сообщение получить ИД пользователя ИД канала ИД беседы
ms.openlocfilehash: 15d564af900e0b13024d051ef4711025c4b16060
ms.sourcegitcommit: fb10a8b14acdba5cc48d2b31dec6f8e6d4ad99ba
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/18/2022
ms.locfileid: "62896329"
---
# <a name="proactive-messages"></a>Упреждающие сообщения

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Упреждающее сообщение — это любое сообщение, отправленное ботом, которое не является ответом на запрос пользователя. Это могут быть следующие сообщения.

* Приветствия
* Уведомления
* Запланированные сообщения

Чтобы бот мог отправлять упреждающие сообщения пользователю, групповому чату или команде, он должен иметь доступ для отправки сообщения. В случае группового чата или команды приложение, содержащее бота, должно быть сначала установлено в этом расположении. Вы можете [заранее установить приложение с помощью Microsoft Graph](#proactively-install-your-app-using-graph) в команде, если это необходимо, или использовать [политику приложений](/microsoftteams/teams-custom-app-policies-and-settings), чтобы передавать приложения командам и пользователям в вашем клиенте. В случае пользователей ваше приложение должно быть установлено для пользователя или пользователь должен быть частью команды, в которой установлено ваше приложение.

Отправка упреждающего сообщения отличается от отправки обычного сообщения. Нет активного `turnContext` для использования в ответе. Перед отправкой сообщения необходимо создать беседу. Например, новый личный чат или новая цепочка беседы в канале. Вы не можете создать новый групповой чат или новый канал в команде с упреждающими сообщениями.

**Отправка упреждающих сообщений**

1. [Получение ИД пользователя, ИД команды или ИД канала](#get-the-user-id-team-id-or-channel-id) при необходимости.
1. [Создание беседы](#create-the-conversation) при необходимости.
1. [Получение ИД беседы](#get-the-conversation-id).
1. [Отправка сообщения](#send-the-message).

Фрагменты кода в разделе [образцы](#samples) для создания личной беседы. Ссылки на полные рабочие примеры для личных бесед и групп или каналов см. в [примерах кода](#code-sample).

Для эффективного использования упреждающих сообщений см. [рекомендации по упреждающим сообщениям](#best-practices-for-proactive-messaging). В некоторых сценариях необходима [упреждающая установка приложения с помощью Graph](#proactively-install-your-app-using-graph). Фрагменты кода в разделе [образцы](#samples) для создания личной беседы. Полные рабочие примеры для личных бесед и групп или каналов см. в [примерах кода](#code-sample).

## <a name="get-the-user-id-team-id-or-channel-id"></a>Получение ИД пользователя, ИД команды или ИД канала

Чтобы создать беседу или цепочку бесед в канале, необходимо иметь правильный ИД. Вы можете получить или извлечь этот ИД с помощью любого из следующих методов.

* При установке приложения в любом определенном контексте вы получаете [`onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* При добавлении нового пользователя в контекст, в котором установлено приложение, вы получаете [`onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в команде, где установлено приложение.
* Вы можете получить [список участников](~/bots/how-to/get-teams-context.md) команды, где установлено приложение.
* Все действия, получаемые ботом, должны содержать требуемую информацию.

Независимо от того, как вы получаете информацию, необходимо сохранить `tenantId` и либо `userId`, либо `channelId`, чтобы создать новую беседу. Вы также можете использовать `teamId`, чтобы создать новую беседу в общем или стандартном канале команды.

`userId` является уникальным для идентификатора бота и определенного пользователя. Вы не можете повторно использовать `userId` между ботами. `channelId` — глобальный параметр. Однако перед отправкой упреждающего сообщения в канал необходимо установить бота в команде.

После получения сведений о пользователе или канале необходимо создать беседу.

## <a name="create-the-conversation"></a>Создание беседы

Если беседы не существует или вы не знаете `conversationId`, следует создать беседу. Беседу следует создать всего один раз и сохранить значение `conversationId`или объект `conversationReference`.

После создания беседы необходимо получить ее ИД.

## <a name="get-the-conversation-id"></a>Получение ИД беседы

Используйте объект `conversationReference` или `conversationId` и `tenantId` для отправки сообщения. Вы можете получить этот ИД, создав беседу или сохранив ее, из любого действия, отправленного вам из этого контекста. Сохраните этот ИД для справки.

Получив соответствующие сведения об адресе, вы можете отправить сообщение.

## <a name="send-the-message"></a>Отправка сообщения

Теперь, когда у вас есть правильные сведения об адресе, вы можете отправить сообщение. Если вы используете пакет SDK, необходимо использовать метод `continueConversation`, а также `conversationId` и `tenantId` для прямого вызова API. Необходимо настроить `conversationParameters` для успешной отправки сообщения. См. раздел с [образцами](#samples) или воспользуйтесь одним из примеров, перечисленных в разделе с [примерами кода](#code-sample).

Теперь, когда вы отправили упреждающее сообщение, необходимо следовать этим рекомендациям при отправке упреждающих сообщений для улучшения обмена информацией между пользователями и ботом.

## <a name="best-practices-for-proactive-messaging"></a>Рекомендации по упреждающим сообщениям

Отправка упреждающих сообщений пользователям может быть эффективным способом общения с ними. Однако с точки зрения пользователя сообщение отображается без причины. Если есть приветственное сообщение, это будет первый раз, когда пользователь взаимодействует с вашим приложением. Важно использовать эту функциональность и предоставить пользователю полную информацию, чтобы он понял назначение этого сообщения.

### <a name="welcome-messages"></a>Приветствия

Если для отправки приветствия пользователю используется упреждающее сообщение, контекст для причины его получения отсутствует. Кроме того, это первый раз, когда пользователи взаимодействуют с вашим приложением. Это возможность создать хорошее первое впечатление. Лучшие приветствия должны включать следующее.

* Причина, по которой пользователь получает сообщение: пользователю должно быть четко понятно, почему он получает сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, сообщите, в каком канале он был установлен и кто его установил.
* Что вы предлагаете: пользователи должны иметь возможность определить, что они могут делать с вашим приложением и какую ценность вы можете им предоставить.
* Что следует делать дальше: пригласите пользователей опробовать команду или взаимодействовать с вашим приложением.
Сообщения с приветствием могут привести к блокировке бота пользователями. Приветствие должно быть понятным и без лишних слов. Пробуйте разные приветствия, если они не оказывают нужного эффекта.

### <a name="notification-messages"></a>Уведомления

Чтобы отправлять уведомления с помощью упреждающих сообщений, убедитесь, что у пользователей есть четкий путь для выполнения общих действий на основе вашего уведомления. Убедитесь, что пользователи четко понимают, почему они получили уведомление. К хорошим уведомлениям обычно относится следующее.

* Что произошло: четкое указание того, что стало причиной получения уведомления.
* Результат: должно быть понятно, какой элемент обновлен для получения уведомления.
* Кто или что вызвало уведомление: кто или какие действия привели к отправлению оповещения.
* Что пользователи могут делать в ответ: сделайте так, чтобы на основе ваших уведомлений было удобно совершать действия.
* Как отказаться от получения: необходимо предоставить пользователям способ отказа от дополнительных уведомлений.

Для отправки сообщений большой группе пользователей, например в организацию, заранее установите приложение с помощью Graph.

### <a name="scheduled-messages"></a>Запланированные сообщения

При использовании упреждающих сообщений для отправки запланированных сообщений пользователям убедитесь, что часовой пояс соответствует их часовому поясу. Это гарантирует доставку сообщений пользователям в подходящее время. Как правило, запланированные сообщения включают следующее.

* Почему пользователь получает сообщение: сделайте так, чтобы пользователи могли легко понять причину, по которой они получают сообщение.
* Что пользователь может сделать дальше: пользователи могут выполнить требуемое действие на основе содержимого сообщения.

## <a name="proactively-install-your-app-using-graph"></a>Заранее установите приложение с помощью Graph

Заблаговременно отправляйте сообщение пользователям, которые не установили приложение или ранее не взаимодействовали с ним. Например, вы хотите использовать [корпоративный коммуникатор](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. В этом случае вы можете использовать API Graph, чтобы заранее установить ваше приложение для пользователей. Кэшируйте необходимые значения из события `conversationUpdate`, которое ваше приложение получает после установки.

Вы можете устанавливать только приложения, которые находятся в каталоге приложений организации или магазине приложений Teams.

См. сведения об [установке приложений для пользователей](/graph/api/userteamwork-post-installedapps) в документации Graph и [упреждающей установке бота и отправке сообщения в Teams с помощью Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). На платформе GitHub также есть [пример Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="samples"></a>Примеры

В следующем коде показано, как отправлять упреждающие сообщения.

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

Необходимо предоставить ИД пользователя и ИД клиента. В случае успешного вызова API возвращает следующий объект отклика:

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a>Пример кода

В следующей таблице приводится простой пример кода, который включает базовый поток бесед в приложение Teams и описывает, как создать цепочку бесед в канале в Teams:

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Основы бесед в Teams  | Демонстрирует основы бесед в Teams, в том числе отправку личных упреждающих сообщений.| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Запуск новой цепочки в канале | Демонстрирует создание новой цепочки в канале. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| Упреждающая установка приложений и отправка упреждающих уведомлений | В этом примере показано, как использовать упреждающую установку приложений для пользователей и отправлять упреждающие уведомления, вызывая API Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | |

### <a name="additional-code-sample"></a>Дополнительный пример кода

> [!div class="nextstepaction"]
> [Примеры кода упреждающих сообщений в Teams](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговым инструкциям](../../../sbs-send-proactive.yml), которые помогают отправлять упреждающие сообщения от бота.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Формат сообщений бота](~/bots/how-to/format-your-bot-messages.md)

## <a name="see-also"></a>См. также

* [**Примеры кода упреждающих сообщений в Teams**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
* [Беседы с бото в канале и групповом чате](~/bots/how-to/conversations/channel-and-group-conversations.md)
* [Ответ на действие отправки модуля задач](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
