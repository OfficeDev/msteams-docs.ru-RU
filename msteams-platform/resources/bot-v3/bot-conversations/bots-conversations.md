---
title: Отправка и получение сообщений с помощью бота
description: Описывает, как отправлять и получать сообщения с помощью ботов в Microsoft Teams
ms.topic: overview
ms.localizationpriority: medium
keywords: teams bots messages
ms.date: 05/20/2019
ms.openlocfilehash: ce3d3d1dd39707d08c720e75c67ec61b606f676a
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518501"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Беседа с Microsoft Teams ботом

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Беседа — это серия сообщений, отправляемых ботом одним или несколькими пользователями. Существует три типа бесед (также называемых областью) в Teams:

* `teams` Также называются телефонные беседы, видимые всем участникам канала.
* `personal` Беседы между ботами и одним пользователем.
* `groupChat` Чат между ботом и двумя или более пользователями.

Бот ведет себя немного по-другому в зависимости от того, в какой беседе он участвует:

* [Боты в беседах](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) с каналами и групповыми чатами требуют от пользователя @mention, чтобы вызвать его в канале.
* [Боты в беседах с одним](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) пользователем не требуют @mention — пользователь может просто ввести.

Чтобы бот работал в определенной области, он должен быть указан в качестве поддержки этой области в манифесте. Области определяются и обсуждаются далее в [справке манифеста](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Упреждающие сообщения

Боты могут участвовать в беседе или инициировать один. Большинство сообщений является ответом на другое сообщение. Если бот инициирует беседу, она называется *проактивным сообщением*. Вот некоторые примеры.

* Приветствия
* Уведомления о событиях
* Сообщения опросов

## <a name="conversation-basics"></a>Основы разговора

Каждое сообщение является объектом `Activity` типа `messageType: message`. Когда пользователь отправляет сообщение, Teams отправляет его боту; в частности, он отправляет объект JSON в конечную точку обмена сообщениями бота. Бот проверяет сообщение, чтобы определить его тип, и отвечает соответствующим образом.

Боты также поддерживают сообщения в стиле событий. Дополнительные сведения [см. в](~/resources/bot-v3/bots-notifications.md) Microsoft Teams. В настоящее время речь не поддерживается.

Сообщения по большей части одинаковы во всех сферах, но существуют различия в доступе к боту в пользовательском интерфейсе и различия за кулисами, о которых необходимо знать.

Основной разговор обрабатывается через соединители bot Framework, единый API REST, чтобы позволить боту общаться с Teams другими каналами. SDK Bot Builder предоставляет простой доступ к этому API, дополнительные функции для управления потоком и состоянием разговоров, а также простые способы включения когнитивных служб, таких как обработка естественного языка (NLP).

## <a name="message-content"></a>Содержимое сообщения

Бот может отправлять богатый текст, изображения и карточки. Пользователи могут отправлять богатый текст и изображения в бот. Вы можете указать тип контента, который бот может обрабатывать на странице Microsoft Teams параметров для вашего бота.

| Формат | От пользователя к боту  | От бота к пользователю |  Примечания |
| --- | :---: | :---: | --- |
| Форматированный текст  | ✔ | ✔ |  |
| Изображения | ✔ | ✔ | Максимальный размер 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF не поддерживается. |
| Карточки | ✖ | ✔ | См. [Teams ссылку на](~/task-modules-and-cards/cards/cards-reference.md) поддерживаемые карты. |
| Emojis | ✖ | ✔ | Teams поддерживает смайлики с помощью UTF-16, например U+1F600 для ухмыляясь. |
|

Дополнительные сведения о типах взаимодействия ботов, поддерживаемых bot Framework, на основе которых основаны боты в командах, см. в документации [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) Bot Framework о потоке бесед и связанных понятиях в документации для bot [Builder SDK для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) и bot [Builder SDK для Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Форматирование сообщения

Вы можете установить необязательное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) свойство a `message` для управления тем, как отрисовка текстового контента сообщения. [Подробное описание](~/resources/bot-v3/bots-message-format.md) поддерживаемого форматирования сообщений в сообщениях ботов см. в тексте форматирования сообщений.
Вы можете настроить необязательный [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) свойство для управления тем, как отрисовка текстового контента сообщения.

Подробные сведения о том, Teams поддерживает форматирование текста в командах, см. в текстовом [формате в сообщениях ботов](~/resources/bot-v3/bots-text-formats.md).

Дополнительные сведения о форматирования карт в сообщениях см. в [сообщении.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="picture-messages"></a>Сообщения изображений

Изображения отправляются путем добавления вложений в сообщение. Дополнительные сведения о вложениях можно найти в документации [Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).

Изображения могут быть не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF не поддерживается.

Рекомендуется указать высоту и ширину каждого изображения с помощью XML. При использовании Markdown размер изображения по умолчанию составляет 256×256. Например:

* Используйте `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Получение сообщений

В зависимости от объявленных областей бот может получать сообщения в следующих контекстах:

* **личный чат** Пользователи могут взаимодействовать в личной беседе с ботом, просто выбрав добавленный бот в истории чата или введя его имя или имя приложения в поле To: box в новом чате.
* **Каналы** Бот может быть упомянут ("@_botname_") в канале, если он был добавлен в команду. Обратите внимание, что дополнительные ответы на бота в канале требуют упоминания бота. Он не будет отвечать на ответы, в которых он не упоминается.

Для входящих сообщений бот получает объект [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) типа `messageType: message`. Несмотря на `Activity` то, что объект может содержать другие типы информации[](~/resources/bot-v3/bots-notifications.md#channel-updates), например обновления каналов, отправленные в бот, `message` этот тип представляет связь между ботом и пользователем.

Бот получает полезное сообщение `Text` пользователя, а также другие сведения о пользователе, источнике сообщения и Teams. Примечание:

* `timestamp` Дата и время сообщения в координируется универсальное время (UTC).
* `localTimestamp` Дата и время сообщения в часовом поясе отправитель.
* `channelId` Всегда "msteams". Это относится к каналу базы ботов, а не каналу команд.
* `from.id` Уникальный и зашифрованный ID для этого пользователя для вашего бота; подходит в качестве ключа, если вашему приложению необходимо хранить данные пользователей. Он уникален для вашего бота и не может непосредственно использоваться за пределами экземпляра бота любым значимым способом для идентификации этого пользователя.
* `channelData.tenant.id` ID клиента для пользователя.

> [!NOTE]
> `from.id` является уникальным для вашего бота и не может непосредственно использоваться за пределами экземпляра бота любым значимым способом для идентификации этого пользователя.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Объединение каналов и частных взаимодействий с ботом

При взаимодействии в канале бот должен быть умен в том, что касается принятия определенных бесед в автономном режиме с пользователем. Например, предположим, что пользователь пытается скоординировать сложную задачу, например планирование с набором участников группы. Вместо того, чтобы вся последовательность взаимодействий была видна каналу, рассмотрите возможность отправки пользователю личного сообщения чата. Ваш бот должен иметь возможность легкого перехода пользователя между личными и канальными беседами без потери состояния.

> [!NOTE]
>Не забудьте обновить канал после завершения взаимодействия, чтобы уведомить других участников группы.

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
> Текстовое поле для входящие сообщения иногда содержит упоминания. Убедитесь, что правильно проверить и лишить их. Дополнительные сведения см. в ["Упоминаниях"](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Teams каналов

Объект `channelData` содержит Teams и является окончательным источником для кодов группы и канала. Необходимо кэширования и использования этих ids в качестве ключей для локального хранения.

Типичный объект channelData в действии, отправленный боту, содержит следующие сведения:

* `eventType`Teams событий; передается только в случаях событий [изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `tenant.id`Microsoft Azure Active Directory клиента Azure AD; передается во всех контекстах.
* `team` Передается только в контекстах каналов, а не в личном чате.
  * `id` GUID для канала.
  * `name` Имя команды; передается только в случаях [переименования событий группы](~/resources/bot-v3/bots-notifications.md#team-name-updates).
* `channel` Передается только в контекстах каналов, когда бот упоминается или для событий в каналах в командах, где был добавлен бот.
  * `id` GUID для канала.
  * `name` Имя канала; передается только в случаях [событий изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `channelData.teamsTeamId` Обесценилось. Это свойство включено только для обратной совместимости.
* `channelData.teamsChannelId` Обесценилось. Это свойство включено только для обратной совместимости.

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

Пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet `TeamsChannelData` предоставляет специализированный объект, который предоставляет свойства для доступа Teams информации.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Отправка ответов на сообщения

Чтобы ответить на существующее сообщение, позвоните [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) в .NET [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) или Node.js. SDK Bot Builder обрабатывает все сведения.

Если вы решите использовать API REST, вы также можете вызвать конечную [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) точку.

Само содержимое сообщения может содержать простой текст или некоторые из предоставленных карт и действий карт Bot [Framework.](~/task-modules-and-cards/cards/cards-actions.md)

Обратите внимание, что в исходящие `serviceUrl` схемы всегда следует использовать ту же схему, что и полученную. Следует помнить, что значение значения `serviceUrl` имеет тенденцию быть стабильным, но может изменяться. Когда появится новое сообщение, бот должен проверить его сохраненное значение `serviceUrl`.

## <a name="updating-messages"></a>Обновление сообщений

Вместо того чтобы ваши сообщения были статическими снимками данных, ваш бот может динамически обновлять сообщения в линию после их отправки. Динамические обновления сообщений можно использовать для таких сценариев, как обновления опросов, изменение доступных действий после нажатия кнопки или любое другое асинхронное изменение состояния.

Новое сообщение не соответствует исходному типу. Например, если исходное сообщение содержало вложение, новое сообщение может быть простым текстовым сообщением.

> [!NOTE]
> Вы можете обновлять только содержимое, отправленное в сообщениях с одним вложением и макетах карусель. Размещение обновлений для сообщений с несколькими вложениями в макете списка не поддерживается.

### <a name="rest-api"></a>REST API

Чтобы отправить обновление сообщения, просто выполните запрос PUT `/v3/conversations/<conversationId>/activities/<activityId>/` на конечную точку с помощью данного ID действия. Чтобы завершить этот сценарий, необходимо кэшировали ID действия, возвращенный исходным вызовом POST.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Пример .NET

Этот метод можно использовать `UpdateActivityAsync` в SDK-конструкторе ботов для обновления существующего сообщения.

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

### <a name="nodejs-example"></a>Node.js пример

Этот метод можно использовать `session.connector.update` в SDK-конструкторе ботов для обновления существующего сообщения.

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

## <a name="starting-a-conversation-proactive-messaging"></a>Запуск беседы (активный обмен сообщениями)

Вы можете создать личный разговор с пользователем или запустить новую цепочку ответов в канале для бота вашей команды. Это позволяет отправлять сообщения пользователю или пользователям, не инициировать первый контакт с ботом. Дополнительную информацию см. в следующих статьях:

Дополнительные сведения о беседах, запущенных [ботами](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) , см. в сообщении Proactive для ботов.

## <a name="deleting-messages"></a>Удаление сообщений

Сообщения можно удалить с помощью метода соединители [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) в [SDK BotBuilder](/bot-framework/bot-builder-overview-getstarted).

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
