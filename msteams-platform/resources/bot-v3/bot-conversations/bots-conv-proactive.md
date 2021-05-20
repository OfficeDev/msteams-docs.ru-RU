---
title: Проактивные сообщения
description: Описывает боты могут начать разговор в Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: команды сценарии проактивного обмена сообщениями разговор бот
ms.openlocfilehash: baf148d0f4d0a669de582dfca70ed5d5bed0274c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566791"
---
# <a name="proactive-messaging-for-bots"></a>Проактивные сообщения для ботов

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Проактивное сообщение – это сообщение, которое отправляется ботом для начала разговора. Существует множество различных причин для инициирования беседы ботом, в том числе:

* Приветственные сообщения для личных разговоров бота.
* Ответы на опросы.
* Внешние уведомления о событиях.

Отправка сообщения для запуска нового потока бесед отличается от отправки сообщения в ответ на существующий разговор: когда ваш бот начинает новый разговор, нет уже существующего разговора, чтобы отправить сообщение. Для того, чтобы отправить упреждающее сообщение, вам нужно:

1. [Решите, что вы собираетесь сказать](#best-practices-for-proactive-messaging)
1. [Получение уникального идентификатора пользователя и идентификатора арендатора](#obtain-necessary-user-information)
1. [Отправка сообщения](#examples)

При создании упреждающих **сообщений вы** `MicrosoftAppCredentials.TrustServiceUrl` должны позвонить, и пройти в службу URL, прежде чем `ConnectorClient` создавать вы будете использовать для отправки сообщения. Если вы этого не сделаете, ваше приложение получит `401: Unauthorized` ответ. Для получения дополнительной [информации, смотрите образцы ниже](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Лучшие практики для упреждающих сообщений

Отправка упреждающих сообщений пользователям может быть очень эффективным способом общения с пользователями. Однако, с их точки зрения, это сообщение может показаться, чтобы прийти к ним совершенно unprompted, и в случае приветственных сообщений будет первый раз, когда они взаимодействовали с вашим приложением. Таким образом, очень важно использовать эту функциональность экономно (не спам ваших пользователей), и предоставить им достаточно информации, чтобы позволить им понять, почему они в настоящее время messaged.

Как правило, упреждающие сообщения относятся к одной из двух категорий: приветствиям или уведомлениям.

### <a name="welcome-messages"></a>Приветствия

При использовании упреждающих сообщений для отправки приветственного сообщения пользователю необходимо иметь в виду, что для большинства людей, получающих сообщение, они не будут иметь контекста, почему они получают его. Это также первый раз, когда они будут взаимодействовать с вашим приложением; это ваша возможность создать хорошее первое впечатление. Лучшие приветственные сообщения будут включать в себя:

* **Почему они получают это сообщение.** Пользователю должно быть очень ясно, почему он получает сообщение. Если ваш бот был установлен в канале, и вы послали приветственное сообщение для всех пользователей, дайте им знать, какой канал он был установлен и, возможно, кто установил его.
* **Что ты предлагаешь.** Что они могут сделать с вашим приложением? Какую ценность вы можете принести им?
* **Что им делать дальше.** Предложите им опробовать команду или каким-либо образом взаимодействовать с вашим приложением.

### <a name="notification-messages"></a>Уведомления

При использовании упреждающих сообщений для отправки уведомлений необходимо убедиться, что у пользователей есть четкий путь для ваших действий на основе вашего уведомления, а также четкое понимание причин, по которым произошло уведомление. Хорошие сообщения уведомлений, как правило, включают в себя:

* **Что произошло.** Четкое указание на то, что произошло, чтобы вызвать уведомление.
* **С чем это случилось.** Должно быть ясно, какой элемент/вещь была обновлена, чтобы вызвать уведомление.
* **Кто сделал это.** Кто принял меры, которые вызвали уведомление будет отправлено.
* **Что они могут с этим поделаешь.** Утехите пользователям действия на основе ваших уведомлений.
* **Как они могут отказаться.** Необходимо предоставить пользователям возможность отказаться от дополнительных уведомлений.

## <a name="obtain-necessary-user-information"></a>Получение необходимой информации о пользователе

Боты могут создавать новые беседы с отдельным Microsoft Teams пользователем, получая уникальный идентификатор *пользователя и идентификатор* *арендатора.* Вы можете получить эти значения с помощью одного из следующих методов:

* Путем [извлечения списка команд из](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) канала, в который устанавливается ваше приложение.
* Путем кэширования их, когда [пользователь взаимодействует с вашим ботом в канале.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Когда пользователи [@mentioned в разговоре канала](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) бот является частью.
* По кэширования их, когда [вы получаете `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) событие, когда ваше приложение установлено в личном прицеле, или новые члены добавляются в канал или групповой чат, что.

### <a name="proactively-install-your-app-using-graph"></a>Проактивная установка приложения с помощью Graph

> [!Note]
> Проактивная установка приложений с использованием графика в настоящее время находится в бета-версии.

Иногда может возникнуть необходимость в упреждающем сообщении пользователям, которые ранее не устанавливали и не взаимодействовали с вашим приложением. Например, вы хотите использовать [коммуникатор компании для отправки](~/samples/app-templates.md#company-communicator) сообщений всей организации. Для этого сценария можно использовать API Graph для упреждающей установки приложения для пользователей, а затем кэшировать необходимые значения `conversationUpdate` из события, которое приложение получит при установке.

Вы можете устанавливать только приложения, которые находятся в каталоге организационных приложений, или Teams магазине приложений.

Для [получения подробной информации можно](/graph/teams-proactive-messaging) Graph приложений для пользователей в документации. Существует также [образец в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Примеры

Убедитесь, что вы аутентичность и предъявить маркер предъявителя, прежде чем создавать новый разговор с помощью REST API.

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

Вы должны предоставить идентификатор пользователя и идентификатор арендатора. Если вызов удался, API возвращается со следующим объектом ответа.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Этот идентификатор является уникальным идентификатором разговора личного чата. Пожалуйста, храните это значение и повторно и использовать его для будущих взаимодействий с пользователем.

### <a name="using-net"></a>Использование .NET

В этом примере [используется пакет Microsoft.Bot.connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet microsoft.

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

Бот, добавленный в команду, может публиковать сообщения на канале, создавая новые цепочки ответов. Если вы используете Node.js Teams SDK, используйте его, который дает вам `startReplyChain()` полностью населенный адрес с правильным идентификатором активности и идентификатором разговора. Если вы используете C- , смотрите пример ниже.

Кроме того, можно использовать API REST и выдавать запрос POST [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурсу.

### <a name="net-example-from-this-sample"></a>Пример .NET (из [этого примера)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)

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

[Образцы Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)