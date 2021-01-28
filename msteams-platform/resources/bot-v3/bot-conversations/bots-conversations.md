---
title: Отправка и получение сообщений с помощью бота
description: В этой статье описывается, как отправлять и получать сообщения с ботами в Microsoft Teams
ms.topic: overview
keywords: сообщения ботов teams
ms.date: 05/20/2019
ms.openlocfilehash: 20c285a0cd06ac929d628edbc059b2a00b937eec
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014119"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Общение с ботом Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Беседа — это серия сообщений, отправленных между ботом и одним или более пользователями. Существует три типа бесед (также называемых областью) в Teams:

* `teams` Также называется беседами канала, которые видны всем участникам канала.
* `personal` Беседы между ботами и одним пользователем.
* `groupChat` Чат между ботом и двумя или более пользователями.

Бот ведет себя немного по-разному в зависимости от типа беседы, в которых он участвует:

* [Боты в беседах](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) в канале и групповом чате требуют от пользователя @упоминания бота, чтобы вызвать его в канале.
* [Боты в беседах с одним пользователем](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) не требуют @упоминания — пользователь может просто ввести.

Чтобы бот работал в определенной области, он должен быть указан как поддерживающие эту область в манифесте. Области определяются и обсуждаются далее в справочнике [по манифестам.](~/resources/schema/manifest-schema.md)

## <a name="proactive-messages"></a>Упреждающие сообщения

Боты могут участвовать в беседе или инициировать ее. Большая часть сообщений является ответом на другое сообщение. Если бот инициирует беседу, это называется упреждающего *сообщения.* Примеры:

* Приветствия
* Уведомления о событиях
* Опрос сообщений

## <a name="conversation-basics"></a>Основы разговора

Каждое сообщение является `Activity` объектом типа `messageType: message` . Когда пользователь отправляет сообщение, Teams отправляет его вашему боту; В частности, он отправляет объект JSON в конечную точку обмена сообщениями бота. Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.

Боты также поддерживают сообщения в стиле событий. Дополнительные сведения см. в записи обработки событий ботов [в Microsoft Teams.](~/resources/bot-v3/bots-notifications.md) В настоящее время речь не поддерживается.

Сообщения по большей части одинаковы для всех областей, но существуют различия в доступе к боту в пользовательском интерфейсе и различия, о которых вам потребуется знать.

Базовая беседа обрабатывается через соединители Bot Framework, один API REST, позволяющий боту взаимодействовать с Teams и другими каналами. SDK построитель ботов предоставляет простой доступ к этому API, дополнительные функции для управления потоком беседы и состоянием, а также простые способы включения функций распознавания, таких как обработка на естественном языке (NLP).

## <a name="message-content"></a>Содержимое сообщения

Бот может отправлять текст, изображения и карточки. Пользователи могут отправлять вашему боту текст и изображения. Вы можете указать тип содержимого, которое бот может обрабатывать на странице параметров Microsoft Teams для вашего бота.

| Format | От пользователя к боту  | От бота к пользователю |  Примечания |
| --- | :---: | :---: | --- |
| Форматированный текст  | ✔ | ✔ |  |
| Изображения | ✔ | ✔ | Не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается |
| Карточки | ✖ | ✔ | См. справочник [по карточкам Teams для](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемых карточек |
| Эмодзи | ✖ | ✔ | В настоящее время Teams поддерживает эмодзи через UTF-16 (например, U+1F600 для ухмылки) |
|

Дополнительные сведения о типах взаимодействия ботов, поддерживаемых Bot Framework (на которых основаны [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) боты в командах), см. в документации Bot Framework о потоке бесед и связанных понятиях в документации для [Bot Builder SDK для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) и [Bot Builder SDK для Node.js. ](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)

## <a name="message-formatting"></a>Форматирование сообщения

Вы можете настроить необязательное свойство A для управления отрисовки текстового [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) `message` содержимого сообщения. Подробное [описание поддерживаемого форматирования](~/resources/bot-v3/bots-message-format.md) в сообщениях ботов см. в описании форматирования сообщений- ботов.
Вы можете настроить необязательное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) свойство, чтобы управлять отрисовка текстового содержимого сообщения.

Подробные сведения о том, как Teams поддерживает форматирование текста в командах, см. в сообщении [бота.](~/resources/bot-v3/bots-text-formats.md)

Сведения о форматирования карточек в сообщениях см. в [формате карточки.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="picture-messages"></a>Сообщения с рисунками

Изображения отправляются путем добавления вложений в сообщение. Дополнительные сведения о вложениях можно найти в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)

Изображения могут иметь не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированное GIF не поддерживается.

Рекомендуется указать высоту и ширину каждого изображения с помощью XML. Если вы используете Markdown, размер изображения по умолчанию составляет 256×256. Пример:

* Воспользуйтесь `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Получение сообщений

В зависимости от объявленных областей бот может получать сообщения в следующих контекстах:

* **личный чат** Пользователи могут взаимодействовать в частной беседе с ботом, просто выбрав добавленного бота в истории чата или введя его имя или ИД приложения в поле "To:" в новом чате.
* **Каналы** Бот можно упомянуть ("@_botname")_ в канале, если он был добавлен в команду. Обратите внимание, что для дополнительных ответов бота в канале необходимо упомянуть бота. Он не будет отвечать на ответы там, где он не упоминается.

Для входящих сообщений бот получает объект [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) типа `messageType: message` . Хотя объект может содержать другие типы информации, например обновления каналов, отправленные вашему боту, тип представляет связь между ботом `Activity` и [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` пользователем.

Бот получает полезное сообщение пользователя, а также другие сведения о пользователе, источнике сообщения и `Text` сведениях Teams. Обратите внимание:

* `timestamp` Дата и время сообщения в универсальном координировании времени (UTC)
* `localTimestamp` Дата и время сообщения в часовом поясе отправитель
* `channelId` Всегда "msteams". Это относится к каналу bot framework, а не к каналу teams.
* `from.id` Уникальный и зашифрованный код для этого пользователя для вашего бота; подходит в качестве ключа, если приложению необходимо хранить данные пользователя. Он уникален для вашего бота и не может непосредственно использоваться за пределами экземпляра бота, чтобы определить этого пользователя
* `channelData.tenant.id` ИД клиента для пользователя.

> [!NOTE]
> `from.id` уникален для вашего бота и не может непосредственно использоваться за пределами экземпляра бота для идентификации этого пользователя.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Сочетание каналов и частных взаимодействий с ботом

При взаимодействии в канале бот должен быть уверен в том, что некоторые беседы с пользователем будут отключены. Например, предположим, что пользователь пытается скоординировать сложную задачу, например планирование с набором участников группы. Вместо того, чтобы вся последовательность действий была видна каналу, рассмотрите возможность отправки пользователю личного сообщения чата. Бот должен иметь возможность легко перенаупорять пользователя между личными беседами и беседами в каналах, не теряя состояние.

> [!NOTE]
>Не забудьте обновить канал после завершения взаимодействия, чтобы уведомить других участников команды.

## <a name="full-inbound-schema-example"></a>Пример полной схемы входящие

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> Текстовое поле для входящие сообщения иногда содержит упоминания. Убедитесь, что они правильно проверяются и разостримы. Дополнительные сведения см. в [упоминаний.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)

## <a name="teams-channel-data"></a>Данные канала Teams

Объект `channelData` содержит сведения, специфичная для Teams, и является окончательным источником для кодов команды и канала. Необходимо кэширования и использовать эти ids в качестве ключей для локального хранилища.

Объект не включается в сообщения в личных беседах, так как они проходят `channelData` за пределами любого канала.

Типичный объект channelData в действии, отправленный вашему боту, содержит следующие сведения:

* `eventType` Тип события Teams; передается только в случае событий [изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id` ИД клиента Azure Active Directory; передается во всех контекстах
* `team` Передается только в контекстах канала, а не в личном чате.
  * `id` GUID для канала
  * `name` Имя команды; передается только в случаях [переименования команды](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` Передается только в контекстах канала, когда бот упоминается, или для событий в каналах в командах, в которые был добавлен бот
  * `id` GUID для канала
  * `name`Имя канала; передается только в случае событий [изменения канала.](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `channelData.teamsTeamId` Неподготовлено. Это свойство включено только для обеспечения обратной совместимости.
* `channelData.teamsChannelId` Неподготовлен. Это свойство включено только для обеспечения обратной совместимости.

### <a name="example-channeldata-object-channelcreated-event"></a>Пример объекта channelData (событие channelCreated)

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a>Пример .NET

Пакет [NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) предоставляет специализированный объект, который предоставляет свойства для доступа к сведениям `TeamsChannelData` о Teams.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Отправка ответов на сообщения

Чтобы ответить на существующее сообщение, вызовите [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) .NET [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) или Node.js. SDK построитель ботов обрабатывает все сведения.

Если вы решили использовать REST API, можно также вызвать [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) конечную точку.

Само содержимое сообщения может содержать простой текст или некоторые предоставленные bot Framework карточки [и действия карт.](~/task-modules-and-cards/cards/cards-actions.md)

Обратите внимание, что в схеме исходящие исходящие должны всегда использовать тот же, `serviceUrl` который вы получили. Следует помнить, что значение `serviceUrl` переменной обычно является стабильным, но может меняться. Когда приходит новое сообщение, бот должен проверить его сохраненное значение `serviceUrl` .

## <a name="updating-messages"></a>Обновление сообщений

Вместо того чтобы ваши сообщения были статическими моментальные снимки данных, бот может динамически обновлять сообщения в текстовом режиме после их отправки. Динамические обновления сообщений можно использовать для таких сценариев, как обновление опроса, изменение доступных действий после нажатия кнопки или любое другое асинхронное изменение состояния.

Новое сообщение не соответствует исходному типу. Например, если исходное сообщение содержало вложение, новое сообщение может быть простым текстовым сообщением.

> [!NOTE]
> Вы можете обновлять только содержимое, отправленное в сообщениях с одним вложением и макетах карусели. Публикация обновлений для сообщений с несколькими вложениями в макете списка не поддерживается.

### <a name="rest-api"></a>REST API

Чтобы отправить обновление сообщения, просто выполните запрос PUT к конечной точке с использованием `/v3/conversations/<conversationId>/activities/<activityId>/` заданного ИД действия. Чтобы завершить этот сценарий, необходимо кэшировали ИД действия, возвращенный исходным вызовом POST.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Пример .NET

Вы можете использовать метод `UpdateActivityAsync` в SDK bot Builder для обновления существующего сообщения.

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a>Node.js примере

Вы можете использовать метод `session.connector.update` в SDK построитель ботов для обновления существующего сообщения.

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a>Начало беседы (упреждающий обмен сообщениями)

Вы можете создать личную беседу с пользователем или запустить новую цепочку ответов в канале для бота группы. Это позволяет отправлять сообщения пользователям или пользователям, не инициировать контакты с ботом. Дополнительную информацию см. в следующих статьях:

Дополнительные [сведения о беседах,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) запущенных ботами, см. в этой теме.

## <a name="deleting-messages"></a>Удаление сообщений

Сообщения можно удалить с помощью метода [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) соединители в [botBuilder SDK.](/bot-framework/bot-builder-overview-getstarted)

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
