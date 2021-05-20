---
title: Отправка и получение сообщений с помощью бота
description: Описывает, как отправлять и получать сообщения с ботами в Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: команды ботов сообщения
ms.date: 05/20/2019
ms.openlocfilehash: e1926afe42bca45eda5f39be1be8342452b3aa24
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566497"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Поговорить с Microsoft Teams ботом

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Беседа — это серия сообщений, отправляемых ботом одним или несколькими пользователями. Существует три типа бесед (также называемых областью) в Teams:

* `teams` Также называются разговоры канала, видимые всем участникам канала.
* `personal` Разговоры между ботами и одним пользователем.
* `groupChat` Чат между ботом и двумя или более пользователями.

Бот ведет себя немного по-разному в зависимости от того, в каком разговоре он участвует:

* [Боты в разговоре в канале и групповом чате](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) требуют, чтобы @mention использовать бота, чтобы вызвать его в канале.
* [Боты в разговорах одного пользователя](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) не требуют @mention - пользователь может просто набрать.

Для того, чтобы бот работал в определенном объеме, он должен быть указан в качестве поддержки этой области в манифесте. Области определяются и обсуждаются далее в [Справке Манифеста.](~/resources/schema/manifest-schema.md)

## <a name="proactive-messages"></a>Проактивные сообщения

Боты могут участвовать в разговоре или инициировать его. Большинство сообщений в ответ на другое сообщение. Если бот инициирует разговор, это называется *упреждающим сообщением.* Вот некоторые примеры.

* Приветствия
* Уведомления о событии
* Сообщения для опроса

## <a name="conversation-basics"></a>Основы разговора

Каждое сообщение является объектом `Activity` типа `messageType: message`. Когда пользователь отправляет сообщение, Teams отправляет его боту; в частности, он отправляет объект JSON в конечную точку обмена сообщениями бота. Ваш бот рассматривает сообщение, чтобы определить его тип и реагирует соответствующим образом.

Боты также поддерживают сообщения в стиле событий. Для получения дополнительной информации [см. События бота Handle в Microsoft Teams.](~/resources/bot-v3/bots-notifications.md) В настоящее время речь не поддерживается.

Сообщения по большей части одинаковы во всех сферах, но есть различия в том, как бот доступен в пользовательском интерфейсе и различия за кулисами, которые вам нужно будет знать.

Основной разговор обрабатывается через Бот Рамочный разъем, единый API REST, чтобы ваш бот волен общаться с Teams другими каналами. Bot Builder SDK обеспечивает легкий доступ к этому API, дополнительную функциональность для управления потоком и состоянием разговоров, а также простые способы включения когнитивных услуг, таких как обработка естественного языка (NLP).

## <a name="message-content"></a>Содержимое сообщения

Ваш бот может отправлять богатые тексты, фотографии и карты. Пользователи могут отправлять богатый текст и фотографии вашему боту. Вы можете указать тип содержимого, с которого ваш бот может справиться в Microsoft Teams настройки для вашего бота.

| Формат | От пользователя к боту  | От бота к пользователю |  Примечания |
| --- | :---: | :---: | --- |
| Форматированный текст  | ✔ | ✔ |  |
| Изображения | ✔ | ✔ | Максимум 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированные GIF не поддерживаются. |
| Карточки | ✖ | ✔ | Смотрите [справку Teams карты для поддерживаемых](~/task-modules-and-cards/cards/cards-reference.md) карт. |
| Эмодзи | ✖ | ✔ | Teams в настоящее время поддерживает смайлики через UTF-16, такие как, U'1F600 для ухмыляясь лица. |
|

Для получения дополнительной информации о типах взаимодействия ботов, поддерживаемых Bot Framework, на которых основаны боты в командах, смотрите документацию Bot Framework о [потоке](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) разговоров и связанных с ней концепциях в [документации для Bot Builder SDK для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) [и Bot Builder SDK на Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Форматирование сообщения

Вы можете установить дополнительное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) свойство a, `message` чтобы контролировать, как отображается текстовое содержимое вашего сообщения. Можно [просмотреть форматирование](~/resources/bot-v3/bots-message-format.md) сообщений для подробного описания поддерживаемого форматирования в сообщениях бота.
Вы можете установить дополнительное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) свойство для управления тем, как отображается текстовое содержимое вашего сообщения.

Для получения подробной информации о том Teams поддерживает форматирование текста в командах, [смотрите форматирование текста в сообщениях бота.](~/resources/bot-v3/bots-text-formats.md)

Для получения дополнительной информации о форматировании карт в сообщениях, [см.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="picture-messages"></a>Сообщения изображения

Фотографии отправляются путем добавления вложений в сообщение. Более подробную информацию о вложениях можно найти в [документации Bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)

Изображения могут быть не более 1024×1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF не поддерживается.

Мы рекомендуем указать высоту и ширину каждого изображения с помощью XML. Если вы используете Markdown, размер изображения по умолчанию до 256×256. Пример:

* Воспользуйтесь `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Получение сообщений

В зависимости от того, какие области объявлены, ваш бот может получать сообщения в следующих контекстах:

* **личный чат** Пользователи могут взаимодействовать в приватном разговоре с ботом, просто выбрав добавленного бота в истории чата, или введя его имя или идентификатор приложения в поле To: box в новом чате.
* **Каналы** Бот может быть упомянут в _канале,_ если он был добавлен в команду. Обратите внимание, что дополнительные ответы на бота в канале требуют упоминания бота. Он не будет отвечать на ответы там, где он не упоминается.

Для входящих сообщений ваш бот [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) получает объект `messageType: message` типа. Хотя объект `Activity` может содержать другие типы информации, такие как [обновления каналов, отправленные](~/resources/bot-v3/bots-notifications.md#channel-updates) вашему боту, `message` тип представляет собой связь между ботом и пользователем.

Ваш бот получает полезную нагрузку, которая содержит сообщение `Text` пользователя, а также другую информацию о пользователе, источнике сообщения и Teams информации. Следует отметить:

* `timestamp` Дата и время сообщения в скоординированном универсальном времени (UTC).
* `localTimestamp` Дата и время сообщения в часовом поясе отправителя.
* `channelId` Всегда "мстемы". Это относится к каналу фреймворка бота, а не к каналу команд.
* `from.id` Уникальный и зашифрованный идентификатор для этого пользователя для вашего бота; подходит в качестве ключа, если вашему приложению необходимо хранить данные пользователей. Он уникален для вашего бота и не может быть непосредственно использован за пределами вашего экземпляра бота каким-либо значимым образом, чтобы определить этого пользователя.
* `channelData.tenant.id` Идентификатор арендатора для пользователя.

> [!NOTE]
> `from.id` уникален для вашего бота и не может быть непосредственно использован за пределами вашего экземпляра бота в какой-либо значимый способ идентификации этого пользователя.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Объединение каналов и частных взаимодействий с ботом

При взаимодействии в канале, ваш бот должен быть умным о принятии определенных разговоров в автономном режиме с пользователем. Например, предположим, что пользователь пытается координировать сложную задачу, например планирование с набором членов группы. Вместо того, чтобы вся последовательность взаимодействий видна каналу, рассмотрите возможность отправки личного сообщения чата пользователю. Ваш бот должен быть в состоянии легко переход пользователя между личными и канал разговоры, не теряя состояния.

> [!NOTE]
>Не забудьте обновить канал, когда взаимодействие будет завершено, чтобы уведомить других членов команды.

## <a name="full-inbound-schema-example"></a>Полный пример входящих схем

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
> Текстовое поле для входящих сообщений иногда содержит упоминания. Будьте уверены, чтобы должным образом проверить и лишить их. Для получения дополнительной информации [см.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)

## <a name="teams-channel-data"></a>Teams канал

Объект `channelData` содержит Teams информацию и является окончательным источником для командных и каналов. Вы должны кэшировать и использовать эти идентификаторы в качестве ключей для локального хранения.

Объект `channelData` не входит в сообщения в личных беседах, так как они происходят вне какого-либо канала.

Типичный объект channelData в действии, отправленной вашему боту, содержит следующую информацию:

* `eventType`Teams тип события; пройдено только в случаях [событий модификации канала.](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id`Azure Active Directory арендатора; прошли во всех контекстах.
* `team` Пройдено только в контексте канала, а не в личном чате.
  * `id` GUID для канала.
  * `name`Название команды; пройдено только в случаях [переименования команды событий.](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` Пройдено только в контексте канала, когда бот упоминается или для событий в каналах в командах, где бот был добавлен.
  * `id` GUID для канала.
  * `name`Название канала; пройдено только в случаях [событий модификации канала.](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `channelData.teamsTeamId` Устаревшие. Это свойство включено только для обратной совместимости.
* `channelData.teamsChannelId` Устаревшие. Это свойство включено только для обратной совместимости.

### <a name="example-channeldata-object-channelcreated-event"></a>Пример объекта channelData (каналСоздаемое событие)

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

Пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet предоставляет `TeamsChannelData` специализированный объект, который предоставляет свойства для доступа Teams конкретной информации.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Отправка ответов на сообщения

Чтобы ответить на существующее сообщение, [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) позвоните в .NET [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) или в Node.js. Bot Builder SDK обрабатывает все детали.

Если вы решите использовать API REST, вы также можете позвонить в [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) конечную точку.

Содержимое сообщения само по себе может содержать простой текст или некоторые из Bot Framework поставляется [карты и действия карты](~/task-modules-and-cards/cards/cards-actions.md).

Обратите внимание, что в своей выездной схеме вы всегда должны использовать то же `serviceUrl` самое, что и полученную схему. Имейте в виду, что `serviceUrl` значение, как правило, стабильны, но может измениться. Когда приходит новое сообщение, бот должен проверить его сохраненную `serviceUrl` стоимость.

## <a name="updating-messages"></a>Обновление сообщений

Вместо того, чтобы ваши сообщения были статическими снимками данных, ваш бот может динамически обновлять сообщения в линии после отправки. Динамические обновления сообщений можно использовать для таких сценариев, как обновление опроса, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.

Новое сообщение не должно соответствовать исходному типу. Например, если исходное сообщение содержало вложение, новое сообщение может быть простым текстовым сообщением.

> [!NOTE]
> Обновлять можно только содержимое, отправленное в односкладных сообщениях и макетах каруселей. Публикация обновлений сообщений с несколькими вложениями в макете списка не поддерживается.

### <a name="rest-api"></a>REST API

Чтобы выпустить обновление сообщения, просто выполните запрос PUT против конечной `/v3/conversations/<conversationId>/activities/<activityId>/` точки с помощью данного идентификатора действия. Для завершения этого сценария следует кэшировать идентификатор действия, возвращенный исходным вызовом POST.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Пример .NET

Вы можете использовать `UpdateActivityAsync` этот метод в Bot Builder SDK для обновления существующего сообщения.

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

Вы можете использовать `session.connector.update` этот метод в Bot Builder SDK для обновления существующего сообщения.

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

## <a name="starting-a-conversation-proactive-messaging"></a>Начало разговора (активный обмен сообщениями)

Вы можете создать личный разговор с пользователем или начать новую цепочку ответов в канале для вашей команды бота. Это позволяет отправлять сообщения пользователю или пользователям, не имея сначала их инициировать контакт с вашим ботом. Дополнительную информацию см. в следующих статьях:

Более [подробную информацию о беседах,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) начатых ботами, можно получить в службах обмена сообщениями Proactive для ботов.

## <a name="deleting-messages"></a>Удаление сообщений

Сообщения могут быть удалены с помощью метода [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) разъемов в [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).

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
