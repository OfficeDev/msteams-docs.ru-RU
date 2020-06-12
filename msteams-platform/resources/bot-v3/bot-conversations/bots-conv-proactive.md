---
title: Упреждающие сообщения
description: В этой статье описывается, как боты может начать беседу в Microsoft Teams.
keywords: сценарии Teams — Bot для активных сообщений
ms.openlocfilehash: adb677bf348065713911d576289c432f8aba3960
ms.sourcegitcommit: b822584b643e003d12d2e9b5b02a0534b2d57d71
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/11/2020
ms.locfileid: "44704455"
---
# <a name="proactive-messaging-for-bots"></a>Упреждающий обмен сообщениями для Боты

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Упреждающее сообщение — это сообщение, которое отправляется с помощью ленты, чтобы начать беседу. Вы можете попытаться начать беседу по ряду причин, в том числе:

* Приветственные сообщения для личных бесед
* Ответы опросов
* Уведомления о внешних событиях

Отправка сообщения для запуска нового цепочки беседы отличается от отправки сообщения в ответ на существующую беседу: при начале новой беседы не существует диалогового окна, в котором будет размещаться сообщение. Чтобы отправить упреждающее сообщение, необходимо выполнить следующие действия:

1. [Принятие решения о том, что вы собираетесь говорить](#best-practices-for-proactive-messaging)
1. [Получение уникального идентификатора пользователя и идентификатора клиента](#obtain-necessary-user-information)
1. [Отправка сообщения](#examples)

При создании упреждающего сообщения **необходимо** вызвать `MicrosoftAppCredentials.TrustServiceUrl` и передать URL-адрес службы перед созданием, который `ConnectorClient` будет использоваться для отправки сообщения. В противном случае ваше приложение получит `401: Unauthorized` ответ. Ознакомьтесь [с приведенными ниже примерами](#net-example-from-this-sample).

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

* [Получение списка команд](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) на канале, в котором установлено приложение.
* Путем их кэширования, когда пользователь [взаимодействует с программой Bot в канале](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Когда пользователи [@mentioned в канале беседы](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) , участником Bot является.
* Путем их кэширования при [получении `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) события при установке приложения в личную область или добавлении новых участников в канал или группу чата.

### <a name="proactively-install-your-app-using-graph"></a>Заактивная установка приложения с помощью Graph

> [!Note]
> Активная установка приложений с помощью Graph в настоящее время находится на стадии бета-тестирования.

Иногда это может потребоваться для упреждающего сообщения пользователей, которые ранее не устанавливали приложение или не работали с ним. Например, вы хотите использовать [Communicator компании](~/samples/app-templates.md#company-communicator) для отправки сообщений во всю организацию. В этом сценарии можно использовать API Graph для профилактической установки приложения для пользователей, а затем кэшировать необходимые значения из события, которое `conversationUpdate` получит ваше приложение после установки.

Вы можете устанавливать только приложения, которые находятся в каталоге организационных приложений или в магазине приложений Teams.

Подробные сведения приведены в [статье Установка приложений для пользователей](/graph/teams-proactive-messaging) в документации Graph. Кроме того, существует [пример в .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Примеры

Перед созданием новой беседы с помощью REST API обязательно проверьте подлинность и наличие маркера носителя.

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

### <a name="using-net"></a>Использование .NET

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

В этой статье *также приведены* [примеры кода Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).

## <a name="creating-a-channel-conversation"></a>Создание беседы канала

Добавленная командой Bot может отправляться в канал для создания новой цепочки ответа. Если вы используете пакет SDK для Node.js Teams, используйте его, чтобы `startReplyChain()` полностью заполнить адрес, соответствующий идентификатору действия и идентификатору беседы. Если вы используете C#, обратитесь к представленному ниже примеру.

Кроме того, вы можете использовать REST API и отправить запрос POST [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ресурсу.

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
