---
title: Упреждающий обмен сообщениями для ботов
description: В этом модуле вы узнаете, как использовать упреждающий обмен сообщениями для ботов и рекомендации по упреждающим обмена сообщениями в Microsoft Teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: ee193cd7dfcfec20f501483eabc3a485cff0caab
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143132"
---
# <a name="proactive-messaging-for-bots"></a>Упреждающий обмен сообщениями для ботов

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Упреждающее сообщение — это сообщение, отправляемое ботом для начала беседы. Существует множество различных причин для инициирования беседы ботом, в том числе:

* Приветственные сообщения для личных бесед ботов.
* Ответы на опрос.
* Уведомления о внешних событиях.
Отправка сообщения для запуска нового потока беседы отличается от отправки сообщения в ответ на существующую беседу: когда бот начинает новую беседу, отсутствует существующая беседа для публикации сообщения. Чтобы отправить упреждающее сообщение, выполните следующие шаги:

1. [Решите, что вы собираетесь сказать](#best-practices-for-proactive-messaging)
1. [Получите уникальный идентификатор пользователя и идентификатор клиента](#obtain-necessary-user-information)
1. [Отправка сообщения](#examples)

При создании упреждающих сообщений **обязательно** вызовите `MicrosoftAppCredentials.TrustServiceUrl` и передайте туда URL-адрес службы, прежде чем создавать объект `ConnectorClient`, используемый для отправки сообщения. В противном случае приложение получит ответ `401: Unauthorized`. Подробнее см. в [приведенных далее образцах](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Рекомендации по упреждающим сообщениям

Отправка упреждающих сообщений пользователям может быть эффективным способом общения с ними. Однако с точки зрения пользователя сообщение отображается без причины. Если есть приветственное сообщение, это будет первый раз, когда пользователь взаимодействует с вашим приложением. Важно использовать эту функциональность и предоставить пользователю полную информацию, чтобы он понял назначение этого сообщения.

Как правило, упреждающие сообщения относятся к одной из двух категорий: приветствиям или уведомлениям.

### <a name="welcome-messages"></a>Приветствия

При использовании упреждающего обмена сообщениями для отправки приветственного сообщения пользователю убедитесь, что с точки зрения пользователя сообщение отображается без запроса с его стороны. Если есть приветственное сообщение, это будет первый раз, когда пользователь взаимодействует с вашим приложением. Лучшие приветствия должны предоставлять следующую информацию

* **Почему получено это сообщение**: пользователю должно быть понятно, почему он получает это сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, сообщите, в каком канале он установлен и кто его установил.
* **Что вы можете предложить**: что могут пользователи делать с вашим приложением? Какая от него может быть польза?
* **Что делать дальше**: пригласите пользователей попробовать выполнить команду или каким-то иным образом взаимодействовать с вашим приложением.

### <a name="notification-messages"></a>Уведомления

Используя упреждающие сообщения для отправки уведомлений, сначала убедитесь, что пользователям понятно, как предпринять распространенные действия для реагирования на ваше сообщение и почему оно было отправлено. Хорошо написанное уведомление обычно содержит перечисленную ниже информацию.

* **Что произошло**: четкое указание на то, что именно стало причиной получения уведомления.
* **С кем/чем это произошло**: должно быть ясно, обновление какого элемента (или какое иное событие) вызвало необходимость отправки уведомления.
* **Кто это сделал**: кто предпринял действия, которые привели к отправке оповещения.
* **Что пользователи могут сделать по этому поводу**: обеспечьте пользователям удобные средства реагирования на ваше уведомление.
* **Как они могут отказаться**: укажите пользователям способ отказаться от дополнительных уведомлений.

## <a name="obtain-necessary-user-information"></a>Получение необходимых сведений о пользователе

Боты могут создавать новые беседы с отдельным пользователем Microsoft Teams, используя *уникальный идентификатор* пользователя и *идентификатор клиента*.  Эти значения можно получить одним из следующих методов:

* [Получение списка команд](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) из канала, где установлено приложение.
* Кэширование их при [взаимодействии пользователя с ботом в канале](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Когда пользователь [@упомянут в беседе канала](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions), в которой участвует бот.
* Кэширование их при [получении события `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) установки приложения в личной области или добавлении новых участников в канал или групповой чат.

### <a name="proactively-install-your-app-using-graph"></a>Заранее установите приложение с помощью Graph

> [!Note]
> Упреждающая установка приложений с помощью Graph в настоящее время находится в бета-версии.

Иногда бывает нужно заблаговременно отправить сообщения пользователям, которые ранее не устанавливали ваше приложение или не взаимодействовали с ним. Например, вы хотите использовать [корпоративный коммуникатор](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. В этом сценарии можно использовать API Graph для упреждающей установки приложения для пользователей, а затем кэшировать необходимые значения из события `conversationUpdate`, получаемого приложением после установки.

Вы можете устанавливать только приложения, которые находятся в каталоге приложений организации или магазине приложений Teams.

[Подробные сведения см](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true). в документации Graph по установке приложений для пользователей. Пример также приведен [в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Примеры

Перед созданием беседы с помощью REST API обязательно убедитесь, что вы выполняете проверку подлинности и имеете получаете маркер носителя.

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

Этот идентификатор является уникальным идентификатором беседы личного чата. Сохраните это значение и повторно используйте его для будущих взаимодействий с пользователем.

### <a name="using-net"></a>Использование .NET

В этом примере используется пакет NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).

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

### <a name="using-nodejs"></a>Использование Node.js

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

## <a name="creating-a-channel-conversation"></a>Создание беседы на канале

Бот, добавленный в команду, может публиковать сообщения на канале, создавая новые цепочки ответов. Если вы используете пакет SDK Node.js Teams, используйте `startReplyChain()`, чтобы получить полный адрес с правильным идентификатором действия и идентификатором беседы. Если вы пищете на C#, см. пример ниже.

В качестве альтернативы можно использовать REST API и отправить запрос POST к ресурсу [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation).

### <a name="net-example-from-this-sample"></a>Пример .NET (из [этого примера](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))

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

## <a name="see-also"></a>Дополнительные ресурсы

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
