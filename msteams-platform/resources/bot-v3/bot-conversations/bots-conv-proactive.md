---
title: Упреждающие сообщения
description: Описывает, что боты могут начать беседу в Microsoft Teams
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams scenarios proactive messaging conversation bot
ms.openlocfilehash: c84b504fc6dba84f33ecaf76a0ce0cdebea82255
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720066"
---
# <a name="proactive-messaging-for-bots"></a>Активный обмен сообщениями для ботов

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Проактивное сообщение — это сообщение, отправленное ботом для начала беседы. Существует множество различных причин для инициирования беседы ботом, в том числе:

* приветствия в личных беседах с ботами;
* ответы на опросы;
* уведомления о внешних событиях.

Отправка сообщения для запуска нового потока беседы отличается от отправки сообщения в ответ на существующий разговор: при запуске нового разговора у бота нет предварительного разговора для отправки сообщения. Чтобы отправить проактивное сообщение, необходимо:

1. [Решите, что вы собираетесь сказать](#best-practices-for-proactive-messaging)
1. [Получение уникального ИД пользователя и его клиента](#obtain-necessary-user-information)
1. [Отправка сообщения](#examples)

При создании упреждающих **сообщений** необходимо вызвать и передать URL-адрес службы перед созданием используемого `MicrosoftAppCredentials.TrustServiceUrl` для `ConnectorClient` отправки сообщения. Если этого не делать, ваше приложение `401: Unauthorized` получает ответ. Дополнительные сведения см. [в примерах ниже.](#net-example-from-this-sample)

## <a name="best-practices-for-proactive-messaging"></a>Лучшие практики для активного обмена сообщениями

Отправка активных сообщений — эффективный способ общения с пользователями. Однако с точки зрения пользователя сообщение отображается незащищенным. Если есть приветствие, это будет первый раз, когда они взаимодействуют с вашим приложением. Важно использовать эту функцию и предоставить полную информацию пользователю, чтобы понять цель этого сообщения.

Как правило, упреждающие сообщения относятся к одной из двух категорий: приветствиям или уведомлениям.

### <a name="welcome-messages"></a>Приветствия

При использовании активной системы обмена сообщениями для отправки приветствия пользователю убедитесь, что с точки зрения пользователя сообщение будет непроизводимо. Если есть приветствие, это будет первый раз, когда они взаимодействуют с вашим приложением. Лучшие приветствия будут включать в себя:

* **Почему они получают это сообщение.** Пользователю должно быть понятно, почему он получает это сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.
* **Что вы предлагаете.** Что они могут сделать с вашим приложением? Какое значение вы можете принести им?
* **Что они должны делать дальше:** предложить им опробовать команду или каким-то образом взаимодействовать с приложением.

### <a name="notification-messages"></a>Уведомления

При использовании активного обмена сообщениями для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь к общим действиям на основе уведомления и четкого понимания причин, по которым произошло уведомление. Хорошие сообщения уведомлений обычно включают в себя:

* **Что произошло:** четкое указание на то, что стало причиной уведомления.
* **Что случилось с**: Должно быть ясно, какой элемент/вещь была обновлена, чтобы вызвать уведомление.
* **Кто:** Кто принял действие, из-за чего было отправлено уведомление?
* **Что они могут с этим сделать:** у вас будет легко принимать меры на основе уведомлений.
* **Как они могут отказаться:** предоставить пользователям путь к отказу от дополнительных уведомлений.

## <a name="obtain-necessary-user-information"></a>Получение необходимых сведений о пользователях

Боты могут создавать новые беседы с Microsoft Teams пользователем, получив уникальный *ID* пользователя и *ID клиента.* Эти значения можно получить с помощью одного из следующих методов:

* [Извлечение реестра команды из](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) канала, на который установлено ваше приложение.
* Кэшинг их при взаимодействии пользователя с [ботом в канале.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Когда пользователь @mentioned [в разговоре по каналу,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) бот является частью.
* Кэшинг их при [ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) приеме события при установке приложения в личной области или добавлении новых участников в канал или групповой чат.

### <a name="proactively-install-your-app-using-graph"></a>Активная установка приложения с помощью Graph

> [!Note]
> Активная установка приложений с помощью графа в настоящее время находится в бета-версии.

Иногда может потребоваться заблаговременное сообщение пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением. Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. Для этого сценария можно использовать API Graph, чтобы упреждающий установку приложения для пользователей, а затем кэш данных, необходимых для события, которое ваше приложение получит после `conversationUpdate` установки.

Вы можете установить только приложения, которые находятся в каталоге организационных приложений или Teams магазине приложений.

Дополнительные [сведения см.](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true) в Graph документации по установке приложений для пользователей. Существует также пример [в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Примеры

Убедитесь, что перед созданием нового разговора с помощью API REST у вас есть маркер проверки подлинности и носите.

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

Этот ID является уникальным ид беседы личного чата. Храните это значение и повторно использовать его для будущих взаимодействий с пользователем.

### <a name="using-net"></a>Использование .NET

В этом примере используется [пакет Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.

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

Бот, добавленный в команду, может публиковать сообщения на канале, создавая новые цепочки ответов. Если вы используете Node.js Teams SDK, используйте , который дает вам полностью заполненный адрес с правильным ИД активности и ИД `startReplyChain()` беседы. Если вы используете C#, см. пример ниже.

Кроме того, можно использовать API REST и опубликовать запрос POST на [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурс.

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

## <a name="see-also"></a>См. также

[Примеры Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
