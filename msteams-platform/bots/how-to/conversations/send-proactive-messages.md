---
title: Отправка упреждающих сообщений
description: Узнайте, как отправлять упреждающие сообщения с помощью бота Teams, устанавливать приложение с помощью Microsoft Graph и проверять примеры кода на основе пакета SDK Bot Framework версии 4.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 7e50719e9befd807127a1eae4022b4af67a9fc00
ms.sourcegitcommit: d58f670fed6ff217c52d2e00c0bee441fcb96920
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819685"
---
# <a name="proactive-messages"></a>Упреждающие сообщения

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Упреждающее сообщение — это любое сообщение, отправленное ботом, которое не является ответом на запрос пользователя. Это сообщение может содержать содержимое, например:

* Приветствия
* Уведомления
* Запланированные сообщения

> [!IMPORTANT]
>
> * Чтобы отправить упреждающее сообщение, рекомендуется начать с [создания бота уведомлений с помощью JavaScript](../../../sbs-gs-notificationbot.yml) или [примера уведомления о входящих веб-перехватчиках](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification). Чтобы приступить к работе, скачайте [обзор набора средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) . Дополнительные сведения см. в [документах Teams Toolkit](../../../toolkit/teams-toolkit-fundamentals.md).
>
> * В настоящее время боты доступны в облаке сообщества для государственных организаций (GCC) и GCC High, но недоступны в средах Министерства обороны США (DoD). Для упреждающих сообщений боты используют следующие конечные точки для облачных сред для государственных организаций: <br> -GCC: `https://smba.infra.gcc.teams.microsoft.com/gcc`<br> — GCCH: `https://smba.infra.gov.teams.microsoft.us/gcch`

Чтобы отправить упреждающее сообщение пользователю, групповому чату или команде, бот должен иметь необходимый доступ для отправки сообщения. В случае группового чата или команды приложение, содержащее бота, должно быть сначала установлено в этом расположении.

При необходимости можно [заранее установить приложение с помощью Microsoft Graph](#proactively-install-your-app-using-graph) в команде или использовать [настраиваемую политику приложений](/microsoftteams/teams-custom-app-policies-and-settings) для установки приложения в командах и для пользователей организации. В некоторых сценариях необходима [упреждающая установка приложения с помощью Graph](#proactively-install-your-app-using-graph). Чтобы пользователь получал упреждающие сообщения, установите приложение для пользователя или сделайте его частью команды, в которой установлено приложение.

Отправка упреждающего сообщения отличается от отправки обычного сообщения. Нет активного `turnContext` для использования в ответе. Перед отправкой сообщения необходимо создать беседу. Например, новый личный чат или новая цепочка беседы в канале. Вы не можете создать новый групповой чат или новый канал в команде с упреждающими сообщениями.

Чтобы отправить упреждающее сообщение, выполните следующие действия.

1. [Получение ИД пользователя, ИД команды или ИД канала](#get-the-user-id-team-id-or-channel-id) при необходимости.
1. [Создание беседы](#create-the-conversation) при необходимости.
1. [Получение ИД беседы](#get-the-conversation-id).
1. [Отправка сообщения](#send-the-message).

Фрагменты кода в разделе [примеров](#samples) предназначены для создания беседы "один к одному". Ссылки на примеры для бесед "один к одному", а также сообщения групп или каналов см. в [разделе Пример кода](#code-sample). Чтобы эффективно использовать упреждающие сообщения, ознакомьтесь [с рекомендациями по упреждающем обмену сообщениями](#best-practices-for-proactive-messaging).

## <a name="get-the-user-id-team-id-or-channel-id"></a>Получение ИД пользователя, ИД команды или ИД канала

Вы можете создать новую беседу с пользователем или поток беседы в канале, и у вас должен быть правильный идентификатор. Получить или получить этот идентификатор можно с помощью одного из следующих способов:

* При установке приложения в определенном контексте вы получаете [`onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* При добавлении нового пользователя в контекст, в котором установлено приложение, вы получаете [`onMembersAdded` действие](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Каждое событие, получаемое ботом, содержит необходимые сведения, которые можно получить из контекста бота (объект TurnContext).
* Вы можете получить [список каналов](~/bots/how-to/get-teams-context.md) в команде, где установлено приложение.
* Вы можете получить [список участников](~/bots/how-to/get-teams-context.md) команды, где установлено приложение.

Независимо от того, как вы получаете информацию, сохраните `tenantId` и `userId` или `channelId` , чтобы создать новую беседу. Вы также можете использовать `teamId`, чтобы создать новую беседу в общем или стандартном канале команды.

`userId` является уникальным для идентификатора бота и определенного пользователя. Вы не можете повторно использовать `userId` между ботами. `channelId` — глобальный параметр. Однако установите бот в команде, прежде чем отправлять упреждающее сообщение на канал.

Создайте беседу после получения сведений о пользователе или канале.

## <a name="create-the-conversation"></a>Создание беседы

Вы можете создать беседу, если она не существует или вы не знаете `conversationId`. Создайте беседу только один раз и сохраните `conversationId` значение или `conversationReference` объект .

Чтобы создать беседу, вам потребуются `userId`, `tenantId`и `serviceUrl`.

Для `serviceUrl`используйте значение из входящего действия, активирующего поток, или один из URL-адресов глобальной службы. `serviceUrl` Если объект недоступен для входящего действия, запускающего упреждающий сценарий, используйте следующие глобальные конечные точки URL-адреса:

* Общественного: `https://smba.trafficmanager.net/teams/`
* GCC: `https://smba.infra.gcc.teams.microsoft.com/gcc`
* GCCH: `https://smba.infra.gov.teams.microsoft.us/gcch`

Пример кода [**см. в**](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/57.teams-conversation-bot/Bots/TeamsConversationBot.cs) примере вызова`CreateConversationAsync`.

Вы можете получить беседу при первой установке приложения. После создания беседы [получите идентификатор беседы](#get-the-conversation-id). `conversationId` доступен в событиях обновления беседы.

Если у `conversationId`вас нет , вы можете [заранее установить приложение с помощью Graph](#proactively-install-your-app-using-graph) для получения `conversationId`.

## <a name="get-the-conversation-id"></a>Получение ИД беседы

Используйте объект `conversationReference` или `conversationId` и `tenantId` для отправки сообщения. Вы можете получить этот ИД, создав беседу или сохранив ее, из любого действия, отправленного вам из этого контекста. Сохраните этот ИД для справки.

Получив соответствующие сведения об адресе, вы можете отправить сообщение.

## <a name="send-the-message"></a>Отправка сообщения

Теперь, когда у вас есть правильные сведения об адресе, вы можете отправить сообщение. Если вы используете пакет SDK, необходимо использовать метод `continueConversation`, а также `conversationId` и `tenantId` для прямого вызова API. Чтобы отправить сообщение, задайте .`conversationParameters` См. раздел с [образцами](#samples) или воспользуйтесь одним из примеров, перечисленных в разделе с [примерами кода](#code-sample).

> [!NOTE]
> Teams не поддерживает отправку упреждающих сообщений с использованием электронной почты или имени участника-пользователя (UPN).

Теперь, когда вы отправили упреждающее сообщение, необходимо следовать этим рекомендациям при отправке упреждающих сообщений для улучшения обмена информацией между пользователями и ботом.

Чтобы узнать, как отправлять упреждающие сообщения от ботов, посмотрите следующее видео:

<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4NHyk]
<br>

### <a name="understand-who-blocked-muted-or-uninstalled-a-bot"></a>Сведения о том, кто заблокировал, отключил или удалил бота

Как разработчик, вы можете создать отчет, чтобы понять, какие пользователи в вашей организации заблокировали, отключили или удалили бот. Эта информация может помочь администраторам вашей организации транслировать сообщения на уровне организации или управлять использованием приложений.

С помощью Teams можно отправить боту упреждающее сообщение, чтобы убедиться, что пользователь заблокировал или удалил бот. Если бот заблокирован или удален, Teams возвращает `403` код ответа с `subCode: MessageWritesBlocked`. Этот ответ указывает, что сообщение, отправленное ботом, не доставляется пользователю.

Код ответа отправляется для каждого пользователя и включает удостоверение пользователя. Вы можете скомпилировать коды ответов для каждого пользователя вместе с его удостоверением, чтобы создать отчет обо всех пользователях, заблокировавших бот.

Ниже приведен пример кода ответа 403.

```http

HTTP/1.1 403 Forbidden

Cache-Control: no-store, must-revalidate, no-cache

 Pragma: no-cache

 Content-Length: 196

 Content-Type: application/json; charset=utf-8

 Server: Microsoft-HTTPAPI/2.0

 Strict-Transport-Security: max-age=31536000; includeSubDomains

 MS-CV: NXZpLk030UGsuHjPdwyhLw.5.0

 ContextId: tcid=0,server=msgapi-canary-eus2-0,cv=NXZpLk030UGsuHjPdwyhLw.5.0

 Date: Tue, 29 Mar 2022 17:34:33 GMT

{"errorCode":209,"message":"{\r\n  \"subCode\": \"MessageWritesBlocked\",\r\n  \"details\": \"Thread is blocked from message writes.\",\r\n  \"errorCode\": null,\r\n  \"errorSubCode\": null\r\n}"}
```

## <a name="best-practices-for-proactive-messaging"></a>Рекомендации по упреждающим сообщениям

Отправка упреждающих сообщений пользователям может быть эффективным способом общения с ними. Однако с точки зрения пользователя сообщение отображается без причины. Если есть приветственное сообщение, это будет первый раз, когда пользователь взаимодействует с вашим приложением. Важно использовать эту функциональность и предоставить пользователю полную информацию, чтобы он понял назначение этого сообщения.

### <a name="welcome-messages"></a>Приветствия

Если для отправки приветственного сообщения пользователю используется упреждающий обмен сообщениями, нет контекста для того, почему пользователь получает это сообщение. Кроме того, это первое взаимодействие пользователя с приложением. Это возможность создать хорошее первое впечатление. Хороший пользовательский интерфейс обеспечивает лучшее внедрение приложения. Плохие приветственные сообщения могут привести к тому, что пользователи заблокируют ваше приложение. Напишите четкое приветственное сообщение и итерируйте его, если оно не оказывает нужного эффекта.

Хорошее приветственное сообщение может включать следующее:

* Причина сообщения. Пользователю должно быть ясно, почему он получает сообщение. Если ваш бот был установлен в канале и вы отправили приветствие всем пользователям, сообщите, в каком канале он был установлен и кто его установил.

* Ваше предложение. Пользователи должны уметь определять, что они могут делать с вашим приложением и какую ценность вы можете им принести.

* Дальнейшие действия. Пользователи должны понимать дальнейшие действия. Например, предложите пользователям опробовать команду или взаимодействовать с приложением.

### <a name="notification-messages"></a>Уведомления

Чтобы отправлять уведомления с помощью упреждающих сообщений, убедитесь, что у пользователей есть четкий путь для выполнения общих действий на основе вашего уведомления. Убедитесь, что пользователи четко понимают, почему они получили уведомление. Сообщения о хороших уведомлениях обычно включают следующие элементы:

* Что произошло? Четкое указание того, что стало причиной получения уведомления.

* Каков результат? Должно быть понятно, какой элемент обновлен для получения уведомления.

* Кто или что его активирует? Кто или что принял меры, которые вызвали отправку уведомления.

* Что пользователи могут сделать в ответ? Сделайте так, чтобы на основе ваших уведомлений было удобно совершать действия.

* Как пользователи могут отказаться от получения уведомлений? Необходимо указать путь для пользователей, чтобы отказаться от дополнительных уведомлений.

Для отправки сообщений большой группе пользователей, например в организацию, заранее установите приложение с помощью Graph.

### <a name="scheduled-messages"></a>Запланированные сообщения

При использовании упреждающих сообщений для отправки запланированных сообщений пользователям убедитесь, что часовой пояс соответствует их часовому поясу. Это гарантирует доставку сообщений пользователям в подходящее время. Как правило, запланированные сообщения включают следующее.

* Почему пользователь получает сообщение? Сделайте так, чтобы пользователи могли легко понять причину, по которой они получают сообщение.

* Что пользователь может сделать дальше? Пользователи могут выполнить требуемое действие на основе содержимого сообщения.

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
        foreach (var conversationReference in _conversationReferences.Values) // Loop of all conversation references must be updated to get it from backend system.
        {
            var newReference = new ConversationReference()
        {
            Bot = new ChannelAccount()
            {
                Id = conversationReference.Bot.Id
            },
            Conversation = new ConversationAccount()
            {
                Id = conversationReference.Conversation.Id
            },
            ServiceUrl = conversationReference.ServiceUrl,
        };
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, newReference, BotCallback, default(CancellationToken));
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

В следующей таблице приводится простой пример кода, который внедряет базовый поток бесед в приложение Teams и описывает, как создать цепочку бесед в канале в Teams:

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Основы бесед в Teams  | Демонстрирует основы бесед в Teams, в том числе отправку личных упреждающих сообщений.| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Запуск новой цепочки в канале | Демонстрирует создание новой цепочки в канале. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| Упреждающая установка приложений и отправка упреждающих уведомлений | В этом примере показано, как использовать упреждающую установку приложений для пользователей и отправлять упреждающие уведомления, вызывая API Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | Н/Д |
| Упреждающий обмен сообщениями | В этом примере показано, как сохранить справочные сведения о беседах пользователя для отправки упреждающего напоминания с помощью ботов. | Н/Д | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging-teamsfx) | Н/Д |

> [!div class="nextstepaction"]
> [Дополнительный пример кода для упреждающего обмена сообщениями](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Формат сообщений бота](~/bots/how-to/format-your-bot-messages.md)

## <a name="see-also"></a>См. также

* [**Примеры кода упреждающих сообщений в Teams**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
* [Беседы с ботом в канале и групповом чате](~/bots/how-to/conversations/channel-and-group-conversations.md)
* [Ответ на действие отправки модуля задач](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [Отправка упреждающих уведомлений пользователям](/azure/bot-service/bot-builder-howto-proactive-message)
* [Создание первого приложения бота с помощью JavaScript](../../../sbs-gs-bot.yml)
* [Создание бота уведомлений с помощью JavaScript для отправки упреждающего сообщения](../../../sbs-gs-notificationbot.yml)
* [TurnContext](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest"&preserve-view=true")
