---
title: Упреждающие сообщения
description: Описание ботов, которые могут начать беседу в Microsoft Teams
keywords: teams scenarios proactive messaging conversation bot
ms.openlocfilehash: 8c93696f79b5d99c32162a7374c7d9adccacb984
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231626"
---
# <a name="proactive-messaging-for-bots"></a>Упреждающий обмен сообщениями для ботов

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Заблаговременное сообщение — это сообщение, от отправленное ботом для начала беседы. Бот может начать беседу по ряду причин, в том числе:

* Приветствия для личных бесед ботов
* Ответы на опрос
* Уведомления о внешних событиях

Отправка сообщения для запуска нового цепочки беседы отличается от отправки сообщения в ответ на существующую беседу: когда бот начинает новую беседу, нет существующей беседы для публикации сообщения. Чтобы отправить упреждающие сообщения, необходимо:

1. [Решите, что вы собираетесь сказать](#best-practices-for-proactive-messaging)
1. [Получение уникального ИД пользователя и ид клиента](#obtain-necessary-user-information)
1. [Отправка сообщения](#examples)

При создании упреждающих **сообщений** необходимо вызвать и передать URL-адрес службы, прежде чем создавать сообщения, которые будут `MicrosoftAppCredentials.TrustServiceUrl` использовать для `ConnectorClient` отправки. Если этого не сделать, ваше приложение получит `401: Unauthorized` ответ. См. [примеры ниже.](#net-example-from-this-sample)

## <a name="best-practices-for-proactive-messaging"></a>Best practices for proactive messaging

Отправка упреждающих сообщений пользователям может быть очень эффективным способом общения с пользователями. Однако с их точки зрения это сообщение может казаться им полностью необсмещенным, и в случае приветствия сообщения будут отображаться при первом взаимодействии с вашим приложением. Поэтому очень важно использовать эту функцию экономно (не спамить пользователей) и предоставлять им достаточно информации, чтобы дать им понять, почему они рассылаются сообщения.

Упреждающие сообщения обычно попадают в одну из двух категорий: приветствия или уведомления.

### <a name="welcome-messages"></a>Приветствия

При использовании упреждающих сообщений для отправки приветствия пользователю следует помнить, что для большинства людей, получающих сообщение, у них не будет контекста для причины его получения. Это также первый раз, когда они будут взаимодействовать с вашим приложением; это ваша возможность создать хорошее первое впечатление. К наиболее оптимальным приветствиям относятся:

* **Почему они получают это сообщение.** Пользователю должно быть понятно, почему он получает сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто, возможно, установил его.
* **Что вы предлагаете.** Что они могут делать с вашим приложением? Какое значение вы можете им дать?
* **Что они должны делать дальше.** Предложите им опробовать команду или каким-либо образом взаимодействовать с вашим приложением.

### <a name="notification-messages"></a>Уведомления

При использовании упреждающих сообщений для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь к общим действиям на основе уведомления и четкое понимание причины отправки уведомления. Хорошие уведомления обычно включают в себя следующие сообщения:

* **Что случилось.** Четкое указание того, что стало причиной уведомления.
* **С чем это произошло.** Должно быть понятно, какой элемент или элемент был обновлен для уведомления.
* **Кто это сделал.** Кто принял действие, которое привело к отправлению уведомления.
* **Что они могут делать с этим.** Сделайте так, чтобы пользователи легко сделайте действия на основе ваших уведомлений.
* **Как они могут отказаться.** Необходимо предоставить пользователям путь для отказа от дополнительных уведомлений.

## <a name="obtain-necessary-user-information"></a>Получение необходимых сведений о пользователе

Боты могут создавать новые беседы с отдельным пользователем Microsoft  Teams, получив уникальный ИД пользователя и *ИД клиента.* Эти значения можно получить с помощью одного из следующих методов:

* Путем [получения группы из](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) канала, в который устанавливается ваше приложение.
* Кэшing их, когда пользователь [взаимодействует с ботом в канале.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Когда пользователь @mentioned [в беседе канала,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) в его состав входит бот.
* Кэшing их, когда [ `conversationUpdate` вы](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) получаете событие, когда приложение установлено в личной области, или новые участники добавляются в канал или групповой чат,

### <a name="proactively-install-your-app-using-graph"></a>Упреждающие установки приложения с помощью Graph

> [!Note]
> Упреждающие установки приложений с помощью graph в настоящее время находятся в бета-версии.

Иногда может потребоваться заблаговременное сообщение пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением. Например, вы хотите использовать company [communicator](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. В этом сценарии можно использовать API Graph для упреждающего установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое ваше приложение получит после `conversationUpdate` установки.

Вы можете устанавливать только приложения, которые находятся в каталоге приложения организации или в магазине приложений Teams.

Подробные [сведения см. в](/graph/teams-proactive-messaging) документации По установке приложений для пользователей в документации Graph. Кроме того, в [.NET есть пример.](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)

## <a name="examples"></a>Примеры

Перед созданием новой беседы с помощью REST API убедитесь, что вы пройдете проверку подлинности и имеете маркер носители.

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

Этот ИД является уникальным ид беседы личного чата. Оохраняйте это значение и повторно его использовать для будущих взаимодействий с пользователем.

### <a name="using-net"></a>Использование .NET

В этом примере используется [пакет NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

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

*См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

## <a name="creating-a-channel-conversation"></a>Создание беседы в канале

Добавленный в команду бот может опубликовать в канале, чтобы создать новую цепочку ответов. Если вы используете Node.js Teams SDK, используйте его, чтобы у вас был полностью заполнен адрес с правильным идом действия и ид `startReplyChain()` беседы. Если вы используете C#, см. пример ниже.

Кроме того, вы можете использовать REST API и опубликовать запрос POST к [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурсу.

### <a name="net-example-from-this-sample"></a>Пример .NET [(из этого примера)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)

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
