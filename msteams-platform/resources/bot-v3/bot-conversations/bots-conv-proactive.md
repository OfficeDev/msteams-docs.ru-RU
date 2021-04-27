---
title: Проактивные сообщения
description: Описывает, как боты могут начать беседу в Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: teams scenarios proactive messaging conversation bot
ms.openlocfilehash: a13c565c8abe8c78fe6402d76796381b6a837393
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019792"
---
# <a name="proactive-messaging-for-bots"></a>Активный обмен сообщениями для ботов

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Проактивное сообщение — это сообщение, отправленное ботом для начала беседы. Существует множество различных причин для инициирования беседы ботом, в том числе:

* приветствия в личных беседах с ботами;
* ответы на опросы;
* уведомления о внешних событиях.

Отправка сообщения для запуска нового потока беседы отличается от отправки сообщения в ответ на существующий разговор: когда ваш бот начинает новый разговор, для отправки сообщения не существует предварительно существующего разговора. Чтобы отправить проактивное сообщение, необходимо:

1. [Решите, что вы собираетесь сказать](#best-practices-for-proactive-messaging)
1. [Получение уникального ИД пользователя и его клиента](#obtain-necessary-user-information)
1. [Отправка сообщения](#examples)

При создании упреждающих **сообщений** необходимо вызвать и передать URL-адрес службы перед созданием используемого для `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` отправки сообщения. Если этого не сделать, приложение получит `401: Unauthorized` ответ. Примеры [см. ниже.](#net-example-from-this-sample)

## <a name="best-practices-for-proactive-messaging"></a>Лучшие практики для активного обмена сообщениями

Отправка активных сообщений пользователям может быть очень эффективным способом общения с пользователями. Однако с их точки зрения это сообщение может казаться совершенно незащищенным, и в случае приветствия сообщения будут впервые взаимодействовать с вашим приложением. Поэтому очень важно использовать эту функцию щадя (не спамить пользователей) и предоставлять им достаточно информации, чтобы они могли понять, почему они рассылаются.

Как правило, упреждающие сообщения относятся к одной из двух категорий: приветствиям или уведомлениям.

### <a name="welcome-messages"></a>Приветствия

При использовании активного обмена сообщениями для отправки приветствия пользователю необходимо иметь в виду, что для большинства людей, получающих сообщение, у них не будет контекста для его получения. Это также первый раз, когда они будут взаимодействовать с вашим приложением; это ваша возможность создать хорошее первое впечатление. Лучшие приветствия будут включать в себя:

* **Почему они получают это сообщение.** Пользователю должно быть ясно, почему он получает сообщение. Если бот был установлен в канале и вы отправили приветствие всем пользователям, дайте им знать, в каком канале он был установлен и кто его установил.
* **Что вы предлагаете.** Что они могут сделать с вашим приложением? Какое значение вы можете принести им?
* **Что они должны делать дальше.** Предложите им опробовать команду или каким-то образом взаимодействовать с приложением.

### <a name="notification-messages"></a>Уведомления

При использовании активного обмена сообщениями для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь к общим действиям на основе уведомления и четкого понимания причин, по которым произошло уведомление. Хорошие сообщения уведомлений обычно включают в себя:

* **Что случилось.** Четкое указание на то, что стало причиной уведомления.
* **С чем это случилось.** Должно быть понятно, какой элемент/вещь был обновлен, чтобы вызвать уведомление.
* **Кто это сделал.** Кто принял действие, из-за которого было отправлено уведомление.
* **Что они могут с этим сделать.** Сделайте так, чтобы пользователям было проще принимать меры на основе ваших уведомлений.
* **Как они могут отказаться.** Необходимо предоставить пользователям путь к отказу от дополнительных уведомлений.

## <a name="obtain-necessary-user-information"></a>Получение необходимых сведений о пользователях

Боты могут создавать новые беседы с отдельным пользователем Microsoft Teams, получив уникальный *ID* пользователя и *ID клиента.* Эти значения можно получить с помощью одного из следующих методов:

* [Извлечение реестра команды из](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) канала, в который установлено ваше приложение.
* Кэшинг их при взаимодействии пользователя с [ботом в канале.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Когда пользователи @mentioned [в разговоре канала,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) бот является частью.
* Кэшинг их при [ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) приеме события при установке приложения в личной области или добавлении новых участников в канал или групповой чат,

### <a name="proactively-install-your-app-using-graph"></a>Активная установка приложения с помощью Graph

> [!Note]
> Активная установка приложений с помощью графа в настоящее время находится в бета-версии.

Иногда может потребоваться заблаговременное сообщение пользователям, которые ранее не устанавливали или не взаимодействовали с вашим приложением. Например, вы хотите использовать коммуникатор [компании](~/samples/app-templates.md#company-communicator) для отправки сообщений всей организации. Для этого сценария можно использовать API Graph для активной установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое ваше приложение получит после `conversationUpdate` установки.

Можно установить только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.

Дополнительные [сведения см. в документации](/graph/teams-proactive-messaging) По установке приложений для пользователей в документации Graph. Существует также пример [в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

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

Этот ID является уникальным ид беседы личного чата. Пожалуйста, сохраняйте это значение и повторно его использовать для будущих взаимодействий с пользователем.

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

*См. также* [примеры Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)

## <a name="creating-a-channel-conversation"></a>Создание беседы на канале

Бот, добавленный в команду, может публиковать сообщения на канале, создавая новые цепочки ответов. Если вы используете Node.js Teams SDK, используйте его, который дает вам полностью заполненный адрес с правильным ид-ид `startReplyChain()` действий. Если вы используете C#, см. пример ниже.

Кроме того, можно использовать API REST и опубликовать запрос POST на [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурс.

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
