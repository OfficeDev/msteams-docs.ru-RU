---
title: Отправка упреждающих сообщений
author: clearab
description: Отправка активных сообщений с помощью робота Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e60fdbfb909abec2c6d64ed0d32fa1a4c4b463a6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675310"
---
# <a name="send-proactive-messages"></a>Отправка упреждающих сообщений

> [!Note]
> В примерах кода, приведенных в этой статье, используются расширения пакета SDK для v3 и 3 для Teams построителя. Концептуально сведения применяются при использовании версий пакета v4 SDK V4, но код слегка отличается.

Упреждающее сообщение — это сообщение, которое отправляется с помощью ленты, чтобы начать беседу. Вы можете попытаться начать беседу по ряду причин, в том числе:

* Приветственные сообщения для личных бесед
* Ответы опросов
* Уведомления о внешних событиях

Отправка сообщения для запуска нового цепочки беседы отличается от отправки сообщения в ответ на существующую беседу: при начале новой беседы не существует диалогового окна, в котором будет размещаться сообщение. Чтобы отправить упреждающее сообщение, необходимо выполнить следующие действия:

1. [Принятие решения о том, что вы собираетесь говорить](#best-practices-for-proactive-messaging)
1. [Получение уникального идентификатора пользователя и идентификатора клиента](#obtain-necessary-user-information)
1. [Отправка сообщения](#examples)

При создании упреждающего сообщения **необходимо** вызвать `MicrosoftAppCredentials.TrustServiceUrl`и передать URL-адрес службы перед созданием `ConnectorClient` , который будет использоваться для отправки сообщения. В противном случае ваше приложение получит `401: Unauthorized` ответ. 

## <a name="best-practices-for-proactive-messaging"></a>Рекомендации по использованию упреждающего обмена сообщениями

Отправка упреждающих сообщений пользователям может быть очень эффективным способом общения с пользователями. Однако с их точки зрения это сообщение может быть полностью нежелательным, а в случае приветственных сообщений будет использоваться при первом взаимодействии с приложением. Таким образом, очень важно использовать эту функцию экономно (не спама для пользователей) и предоставить им достаточно информации, чтобы убедиться в их подлинности.

Упреждающие сообщения обычно делятся на две категории: приветственные сообщения или уведомления.

### <a name="welcome-messages"></a>Приветственные сообщения

При использовании упреждающего обмена сообщениями для отправки пользователю приветственного сообщения необходимо помнить, что большинство людей, получивших сообщение, не будут иметь контекст для их получения. Это также происходит в первый раз, когда он будет взаимодействовать с вашим приложением; можно создать хорошее первое впечатление. Лучшие приветственные сообщения будут включать:

* **Почему они получают это сообщение.** Он должен быть очень очевидным, чтобы пользователь получал сообщение. Если ваш Bot был установлен в канале и вы отправили приветственное сообщение всем пользователям, сообщите им о том, в каком канале он был установлен и кто его установил.
* **Что вы предоставляете.** Что можно делать с приложением? Какое значение можно перенести?
* **Что делать дальше.** Пригласите их, чтобы испытать команду или взаимодействовать с приложением каким бы то ни было способом.

### <a name="notification-messages"></a>Сообщения уведомления

При использовании упреждающего обмена сообщениями для отправки уведомлений необходимо убедиться, что у пользователей есть четко настроенный путь для выполнения общих действий на основе уведомления, и четко понимать, почему возникло уведомление. К хорошим сообщениям уведомления обычно относятся:

* **Что случилось.** Четкое указание того, что произошло с причиной уведомления.
* **Что случилось.** Должно быть ясно, какие элементы/вещи были обновлены, чтобы получить уведомление.
* **Кто это сделал.** Кто потратил действие, вызвавшее отправку уведомления.
* **Что они могут сделать.** Облегчить пользователям выполнение действий в соответствии с вашими уведомлениями.
* **Как они могут отказаться.** Необходимо указать путь для пользователей, чтобы отказаться от дополнительных уведомлений.

## <a name="obtain-necessary-user-information"></a>Получение необходимых сведений о пользователе

Боты может создавать новые беседы с отдельным пользователем Microsoft Teams, получая *уникальный идентификатор* пользователя и *идентификатор клиента.* Эти значения можно получить с помощью одного из следующих методов:

* [Получение списка команд](../get-teams-context.md#fetching-the-roster-or-user-profile) на канале, в котором установлено приложение.
* Путем их кэширования, когда пользователь [взаимодействует с программой Bot в канале](./channel-and-group-conversations.md).
* Когда пользователи [@mentioned в канале беседы](./channel-and-group-conversations.md#retrieving-mentions) , участником Bot является.
* Путем их кэширования при [получении `conversationUpdate` ](./subscribe-to-conversation-events.md#team-members-added) события при установке приложения в личную область или добавлении новых участников в канал или группу чата.

### <a name="proactively-install-your-app-using-graph"></a>Заактивная установка приложения с помощью Graph

> [!Note]
> Активная установка приложений с помощью Graph в настоящее время находится на стадии бета-тестирования.

Иногда это может потребоваться для упреждающего сообщения пользователей, которые ранее не устанавливали приложение или не работали с ним. Например, вы хотите использовать [Communicator компании](~/samples/app-templates.md#company-communicator) для отправки сообщений во всю организацию. В этом сценарии можно использовать API Graph для профилактической установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое `conversationUpdate` получит ваше приложение после установки.

Вы можете устанавливать только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.

Подробные сведения приведены в [статье Установка приложений для пользователей](/graph/teams-proactive-messaging) в документации Graph. Кроме того, существует [пример в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Примеры

Перед созданием новой беседы с помощью REST API обязательно проверьте подлинность и наличие маркера носителя. `members.id` Поле в расположенном ниже объекте является уникальным в сочетании с пользователем. Вы не можете получить его с помощью любого другого метода, чем описано выше.

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

Этот идентификатор является уникальным ИДЕНТИФИКАТОРом беседы личного чата. Сохраните это значение и повторно используйте его для последующего взаимодействия с пользователем.

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

В этом примере используется пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

В этом примере используется пакет NPM [ботбуилдер – Teams](https://www.npmjs.com/package/botbuilder-teams) .

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```python
async def _send_proactive_message():
  for conversation_reference in CONVERSATION_REFERENCES.values():
    return await ADAPTER.continue_conversation(APP_ID, conversation_reference,
      lambda turn_context: turn_context.send_activity("proactive hello")
    )

```

---

## <a name="creating-a-channel-conversation"></a>Создание беседы канала

Добавленная командой Bot может отправляться в канал для создания новой цепочки ответа. Если вы используете пакет SDK для Teams. js, используйте `startReplyChain()` его, который предоставляет полностью заполненный адрес с правильным идентификатором действия и идентификатором диалога. Если вы используете C#, обратитесь к представленному ниже примеру.

Кроме того, вы можете использовать REST API и отправить запрос POST [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурсу.

# <a name="cnettabdotnet"></a>[ЯЗЫК C#/.НЕТ](#tab/dotnet)

В [этом примере](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)показан следующий фрагмент кода.


```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

В этом примере используется пакет NPM [ботбуилдер – Teams](https://www.npmjs.com/package/botbuilder-teams) . Приведенный ниже фрагмент кода относится к [теамсконверсатионбот. js](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js).

[!code-javascript[messageAllMembersAsync](~/../botbuilder-samples/samples/javascript_nodejs/57.teams-conversation-bot/bots/teamsConversationBot.js?range=115-134&highlight=13-15)]

# <a name="pythontabpython"></a>[Python](#tab/python)

[!code-python[message-all-members](~/../botbuilder-samples/samples/python/57.teams-conversation-bot/bots/teams_conversation_bot.py?range=101-135)]

---
