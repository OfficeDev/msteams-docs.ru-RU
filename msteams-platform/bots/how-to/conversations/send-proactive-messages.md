---
title: отправка упреждающих сообщений
description: описывает, как отправлять упреждающие сообщения с помощью бота Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: отправка сообщения получить ID-ID-ID канала для беседы
ms.openlocfilehash: 7da470eaba6ae9ecb82c9a7ba04d69b2f196a9d7
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654295"
---
# <a name="send-proactive-messages"></a>Отправлять активные сообщения

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Проактивное сообщение — это любое сообщение, отправленное ботом, которое не является прямым ответом на запрос пользователя. Это может включать такие сообщения, как:

* Приветствия
* Уведомления
* Запланированные сообщения

Для отправки упреждающего сообщения бот должен иметь доступ к пользователю, групповому чату или команде, в которую необходимо отправить сообщение. Для группового чата или группы это означает, что приложение, содержа которое содержит бот, сначала должно быть установлено в этом расположении. Вы можете [упреждающий](#proactively-install-your-app-using-graph) установку приложения с помощью Graph [](/microsoftteams/teams-custom-app-policies-and-settings) в команде, если это необходимо, или использовать политику приложения для вытеснки приложений для групп и пользователей в клиенте. Для пользователей ваше приложение либо должно быть установлено для пользователя, либо пользователь должен быть частью команды, в которой установлено ваше приложение.

Отправка упреждающего сообщения отличается от обычного сообщения. В этом нет активного использования `turnContext` для ответа. Перед отправкой сообщения может потребоваться также создать беседу. Например, новый чат один к одному или новый поток беседы в канале. Невозможно создать новый групповой чат или новый канал в команде с активной передачей сообщений.

На высоком уровне необходимо выполнить действия, необходимые для отправки проактивного сообщения:

1. [Получите пользовательский ID или team/channel ID](#get-the-user-id-or-teamchannel-id) (при необходимости).
1. [Создание потока беседы](#create-the-conversation) или беседы (при необходимости).
1. [Получите ID беседы](#get-the-conversation-id).
1. [Отправка сообщения](#send-the-message).

Фрагменты кода в разделе [примеры](#examples) для создания беседы один к одному. Ссылки на полные рабочие примеры для бесед и групп или каналов см. в [примере кода.](#code-samples)

## <a name="get-the-user-id-or-teamchannel-id"></a>Получить пользовательский ИД или team/channel ID

Для создания нового потока беседы или беседы в канале необходим правильный ID. Этот ID можно получить или получить несколькими способами:

1. Когда ваше приложение установлено в определенном контексте, вы получите [ `onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. При добавлении нового пользователя в контекст, в котором установлено приложение, вы получите [ `onMembersAdded` действие.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. Список [каналов в](~/bots/how-to/get-teams-context.md) команде, установленной в приложении, можно получить.
1. Вы можете получить [список членов команды,](~/bots/how-to/get-teams-context.md) установленной вашим приложением.
1. Каждое действие, получаемые ботом, должно содержать необходимые сведения.

Независимо от того, как вы получаете информацию, вам потребуется сохранить и либо создать `tenantId` `userId` новый `channelId` разговор. Вы также можете использовать этот поток для создания нового потока беседы в общем или по умолчанию `teamId` канале группы.

Уникальный для вашего бота и определенного пользователя, вы не можете `userId` повторно использовать их между ботами. Однако, прежде чем отправить проактивное сообщение на канал, бот должен быть установлен в `channelId` команде.

## <a name="create-the-conversation"></a>Создание беседы

После получения сведений о пользователе или канале необходимо создать беседу, если она еще не существует или вы не знаете `conversationId` . Вы должны создать беседу только один раз и убедиться, что вы сохраняете значение или объект, который `conversationId` будет использовать в `conversationReference` будущем.

## <a name="get-the-conversation-id"></a>Получить ID беседы

После создания беседы используйте объект `conversationReference` или `conversationId` отправить `tenantId` сообщение. Этот ID можно получить, создав беседу или храня ее из любого действия, отправленного вам из этого контекста. Убедитесь, что вы сохраняете этот ID.

## <a name="send-the-message"></a>Отправка сообщения

Теперь, когда у вас есть правильные сведения о адресе, вы можете отправить свое сообщение. Если вы используете SDK, вы сделаете это с помощью метода, а также для прямого `continueConversation` `conversationId` вызова `tenantId` API. Чтобы успешно отправить сообщение, необходимо правильно `conversationParameters` установить. См. [раздел примеры](#examples) или используйте один из примеров, перечисленных в разделе примеры [кода.](#code-samples)

## <a name="best-practices-for-proactive-messaging"></a>Лучшие практики для активного обмена сообщениями

Отправка активных сообщений пользователям — это очень эффективный способ общения с пользователями. Однако с их точки зрения это сообщение может отображаться совершенно незащищенным, и в случае приветствия сообщений это первый раз, когда они взаимодействуют с вашим приложением. Поэтому очень важно использовать эти функции экономно, не спамить пользователей и предоставлять достаточно информации, чтобы пользователи могли понять, почему они рассылаются.

### <a name="welcome-messages"></a>Приветствия

При использовании активного обмена сообщениями для отправки приветствия пользователю необходимо иметь в виду, что для большинства людей, получающих сообщение, нет контекста для его получения. Кроме того, они впервые взаимодействуют с вашим приложением. Это ваша возможность создать хорошее первое впечатление. Лучшие приветствия должны включать в себя:

* **Почему пользователь получает сообщение.** Пользователю должно быть ясно, почему он получает сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.
* **Что вы предлагаете.** Что они могут сделать с вашим приложением? Какое значение вы можете принести им?
* **Что они должны делать дальше.** Предложите им опробовать команду или каким-то образом взаимодействовать с приложением.

Помните, что неудовлетворительные приветствия могут привести к блокировке бота пользователями. Утратите много времени на то, чтобы создать приветствия и итерировать их, если они не будут иметь желаемого эффекта.

### <a name="notification-messages"></a>Уведомления

При использовании упреждающих сообщений для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь к общим действиям, основанным на уведомлении и четком понимании причин, по которым произошло уведомление. Хорошие сообщения уведомлений обычно включают в себя:

* **Что случилось.** Четкое указание на то, что стало причиной уведомления.
* **Какой был результат.** Должно быть ясно, какой элемент или вещь была обновлена, чтобы вызвать уведомление.
* **Кто и что вызвало его.** Кто или какие действия привели к отправлению уведомления.
* **Что пользователи могут сделать в ответ.** Сделайте так, чтобы пользователям было проще принимать меры на основе ваших уведомлений.
* **Как пользователи могут отказаться.** Необходимо предоставить пользователям путь к отказу от дополнительных уведомлений.

### <a name="scheduled-messages"></a>Запланированные сообщения

При использовании активных сообщений для отправки запланированных сообщений пользователям убедитесь, что часовой пояс обновляется до часового пояса. Это обеспечивает доставку сообщений пользователям в соответствующее время. Расписание сообщений обычно включает в себя:

* **Почему пользователь получает** сообщение. Чтобы пользователям было легко понять причину, по которой они получают сообщение.
* **Что может сделать пользователь далее.** Пользователи могут принять необходимые действия на основе контента сообщения.

## <a name="proactively-install-your-app-using-graph"></a>Активная установка приложения с помощью Graph

> [!Note]
> Активная установка приложений с помощью Microsoft Graph в настоящее время находится в бета-версии.

Иногда может потребоваться заблаговременное сообщение пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением. Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. Для этого сценария можно использовать API Graph для активной установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое ваше приложение получает при `conversationUpdate` установке.

Можно установить только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.

См. [в документе](/graph/api/userteamwork-post-installedapps) Install apps for users in the Graph documentation and [Proactive bot installation and messaging in Teams with Microsoft Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) На платформе GitHub также имеется пример фреймворка [Microsoft.NET.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)

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

Необходимо предоставить пользовательский ИД и ИД клиента. Если вызов удался, API возвращается со следующим объектом ответа.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-samples"></a>Примеры кода

Официальные примеры проактивных сообщений:

| Имя образца           | Описание                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Основы беседы teams  | Демонстрирует основы бесед в Teams, в том числе отправку одно к одному упреждающих сообщений.|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|Запуск нового потока в канале     | Демонстрирует создание нового потока в канале. |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>Просмотр дополнительных примеров кода
>
> [!div class="nextstepaction"]
> [**Teams proactive messaging code samples**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
