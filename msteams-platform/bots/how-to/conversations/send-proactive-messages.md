---
title: отправка упреждающих сообщений
description: описывает, как отправлять упреждающие сообщения с помощью бота Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: send a message get user ID channel ID conversation ID
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103607"
---
# <a name="send-proactive-messages"></a>Отправлять активные сообщения

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Упреждающие сообщения — это любое сообщение, отправленное ботом, которое не является прямым ответом на запрос пользователя. Это может включать следующие сообщения:

* Приветствия
* Уведомления
* Запланированные сообщения

Чтобы бот мог отправить упреждающие сообщения, он должен иметь доступ к пользователю, групповому чату или команде, в которую вы хотите отправить сообщение. Для группового чата или команды это означает, что приложение, содержа которое содержит бота, должно быть сначала установлено в этом расположении. Вы можете [заблаговременно установить](#proactively-install-your-app-using-graph) приложение с помощью Graph в команде, если это необходимо, или использовать политику приложений для раздатки приложений командам и пользователям в клиенте. [](/microsoftteams/teams-custom-app-policies-and-settings) Для пользователей ваше приложение либо должно быть установлено для пользователя, либо пользователь должен быть частью команды, в которой установлено ваше приложение.

Отправка упреждающего сообщения отличается от отправки обычного сообщения. При этом нет активного `turnContext` ответа. Кроме того, перед отправкой сообщения может потребоваться создать беседу. Например, новый чат "один к одному" или новый поток беседы в канале. Невозможно создать новый групповой чат или новый канал в команде с упреждающего обмена сообщениями.

На высоком уровне действия, необходимые для отправки упреждающего сообщения:

1. [Получите ИД пользователя или ид команды или канала](#get-the-user-id-or-teamchannel-id) (при необходимости).
1. [Создайте беседу или цепочку](#create-the-conversation) бесед (при необходимости).
1. [Получите ИД беседы.](#get-the-conversation-id)
1. [Отправьте сообщение.](#send-the-message)

Фрагменты кода в разделе [примеров](#examples) для создания беседы "один к одному". Ссылки на полные рабочие примеры для бесед "один к одному", а также для групп или каналов см. в [примерах кода.](#code-samples)

## <a name="get-the-user-id-or-teamchannel-id"></a>Get the user ID or team/channel ID

Чтобы создать беседу или цепочку бесед в канале, необходим правильный ИД. Этот ИД можно получить несколькими способами:

1. Когда приложение устанавливается в любом конкретном контексте, вы получите [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. При добавлении нового пользователя в контекст, в котором установлено приложение, вы получите [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в команде, в которая установлено ваше приложение.
1. Вы можете получить [список участников команды,](~/bots/how-to/get-teams-context.md) в которая установлено ваше приложение.
1. Все действия, получаемые ботом, должны содержать необходимые сведения.

Независимо от того, как вы получаете информацию, вам потребуется сохранить беседу или создать `tenantId` `userId` новую `channelId` беседу. Вы также можете создать цепочку беседы в общем или канале команды по `teamId` умолчанию.

Уникальный для вашего ИД бота и конкретного пользователя, вы не можете повторно использовать их `userId` между ботами. Однако перед отправкой упреждающего сообщения в канал бот должен быть установлен в `channelId` команде.

## <a name="create-the-conversation"></a>Создание беседы

После получения сведений о пользователе или канале необходимо создать беседу, если она еще не существует или вы не `conversationId` знаете. Необходимо создать беседу только один раз и убедиться, что вы сохраняете значение или объект для `conversationId` `conversationReference` использования в будущем.

## <a name="get-the-conversation-id"></a>Получить ИД беседы

После создания беседы используйте объект `conversationReference` или `conversationId` отправьте `tenantId` сообщение. Этот ИД можно получить, создав беседу или с помощью любого действия, отправленного вам из этого контекста. Убедитесь, что вы сохраняете этот ИД.

## <a name="send-the-message"></a>Отправка сообщения

Теперь, когда у вас есть правильные сведения об адресе, вы можете отправить сообщение. Если вы используете SDK, вы сделаете это с помощью метода, а также для прямого `continueConversation` `conversationId` вызова `tenantId` API. Чтобы успешно отправить сообщение, необходимо `conversationParameters` правильно настроить его. См. [раздел примеров](#examples) или используйте один из примеров, перечисленных в разделе [примеров](#code-samples) кода.

## <a name="best-practices-for-proactive-messaging"></a>Практические методики упреждающего обмена сообщениями

Отправка упреждающих сообщений пользователям — очень эффективный способ общения с пользователями. Однако с их точки зрения это сообщение может отображаться полностью незащищенным, и в случае приветствия это сообщение впервые взаимодействует с вашим приложением. Поэтому очень важно использовать эту функцию не слишком часто, не рассылая пользователям нежелаую почту, и предоставлять достаточно информации, чтобы пользователи могли понять, почему они рассылаются.

### <a name="welcome-messages"></a>Приветствия

При использовании упреждающих сообщений для отправки приветствия пользователю необходимо помнить, что для большинства людей, получающих сообщение, нет контекста для его получения. Это также первый раз, когда они взаимодействуют с вашим приложением. Это ваша возможность создать хорошее первое впечатление. Лучшие приветствия должны включать следующие сообщения:

* **Почему пользователь получает сообщение.** Пользователю должно быть понятно, почему он получает сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен, и, возможно, кто его установил.
* **Что вы предлагаете.** Что они могут делать с вашим приложением? Какое значение вы можете им дать?
* **Что они должны делать дальше.** Предложите им опробовать команду или каким-либо образом взаимодействовать с приложением.

Помните, что неудовлетворительные приветствия могут привести к блокированию бота пользователями. Потратите много времени на то, чтобы создать приветствия, и итерации на них, если они не имеют желаемого эффекта.

### <a name="notification-messages"></a>Уведомления

При использовании упреждающих сообщений для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь для распространенных действий на основе уведомления и четкого понимания причины отправки уведомления. К хорошим уведомлениям обычно относятся:

* **Что случилось.** Четкое указание того, что стало причиной уведомления.
* **Результат.** Чтобы вызвать уведомление, необходимо четко знать, какой элемент или что было обновлено.
* **Кто и что инициировало его.** Кто или какие действия привели к отправлению уведомления.
* **Что пользователи могут делать в ответе.** Сделайте так, чтобы пользователи легко делайте действия на основе ваших уведомлений.
* **Как пользователи могут отказаться от этого.** Необходимо предоставить пользователям путь для отказа от дополнительных уведомлений.

## <a name="proactively-install-your-app-using-graph"></a>Упреждающие установки приложения с помощью Graph

> [!Note]
> Упреждающие установки приложений с помощью Microsoft Graph в настоящее время находятся в бета-версии.

Иногда может потребоваться заблаговременно отправлять сообщения пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением. Например, вы хотите использовать company [communicator](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. В этом сценарии можно использовать API Graph для упреждающего установки приложения для пользователей, а затем кэшировать необходимые значения из события, получаемого вашим приложением `conversationUpdate` после установки.

Вы можете устанавливать только приложения, которые находятся в каталоге приложений организации или в магазине приложений Teams.

См. ["Установка приложений для пользователей"](/graph/api/userteamwork-post-installedapps) в документации по Graph, а также в документации по профилактической установке ботов и обмену сообщениями [в Teams с помощью Microsoft Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) На платформе [GitHub также](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) есть пример платформы Microsoft .NET Framework.

## <a name="examples"></a>Примеры

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

Необходимо предоставить ид пользователя, и ид клиента. В случае успешного вызова API возвращается со следующим объектом ответа.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>Примеры кода

Официальные примеры упреждающих сообщений:

| Имя примера           | Описание                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Основные принципы бесед Teams  | В этой теме показано, как начать беседы в Teams, включая отправку сообщений "один к одному".|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|Запуск нового потока в канале     | Демонстрирует создание нового потока в канале. |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>Просмотр дополнительных примеров кода
>
> [!div class="nextstepaction"]
> [**Примеры кода упреждающих сообщений Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
