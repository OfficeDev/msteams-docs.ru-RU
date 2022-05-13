---
title: Отправка и получение сообщений с помощью бота
description: В этой статье описывается, как отправлять и получать сообщения с помощью ботов в Microsoft Teams
ms.topic: overview
ms.localizationpriority: medium
keywords: Сообщения ботов teams
ms.date: 05/20/2019
ms.openlocfilehash: 0d4665d098e0e14fa3de5f2667c7e970b545b284
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2022
ms.locfileid: "65296975"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Беседа с ботом Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Беседа — это серия сообщений, отправляемых ботом одним или несколькими пользователями. Существует три типа бесед (также называемых областью) в Teams:

* `teams`: также называются беседами канала, которые видимы для всех участников канала.
* `personal`: беседы между ботами и одним пользователем
* `groupChat`: беседа между ботом и двумя или более пользователями

Поведение бота немного отличается в зависимости от типа беседы, в которых он участвует:

* [Боты в беседах канала и группового чата](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) требуют, чтобы пользователь @упомянул бота, чтобы вызвать его в канале.
* [Боты в беседах с одним пользователем](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) не требуют @упоминания — пользователь может просто вводить текст.

Чтобы бот работал в определенной области, он должен быть указан как поддерживающий эту область в манифесте. Области определены и описаны далее в [Справочнике по манифесту](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Упреждающие сообщения

Боты могут участвовать в беседе или инициировать ее. Большинство сообщений отправляется в ответ на другое сообщение. Если бот инициирует беседу, это называется *упреждающим сообщением*. Вот некоторые примеры.

* Приветствия
* Уведомления о событиях
* Сообщения опроса

## <a name="conversation-basics"></a>Основы разговора

Каждое сообщение является объектом `Activity` типа `messageType: message`. Когда пользователь отправляет сообщение, Teams отправляет его боту; в частности, он отправляет объект JSON в конечную точку обмена сообщениями бота. Бот проверяет сообщение, чтобы определить его тип и ответить соответствующим образом.

Боты также поддерживают сообщения в стиле событий. Дополнительные сведения см. в статье [Обработка событий бота в Microsoft Teams](~/resources/bot-v3/bots-notifications.md). В настоящее время речь не поддерживается.

Сообщения обычно одинаковы во всех областях, но существуют различия в способах доступа к боту в пользовательском интерфейсе и различия в фоновом режиме, о которых необходимо знать.

Базовая беседа обрабатывается через соединитель Bot Framework, единый REST API, позволяющий боту взаимодействовать с Teams и другими каналами. Пакет SDK Bot Builder предоставляет простой доступ к этому API, дополнительные функции для управления потоком и состоянием беседы, а также простые способы внедрения когнитивных служб, таких как обработка на естественном языке (NLP).

## <a name="message-content"></a>Содержимое сообщения

Бот может отправлять форматированный текст, изображения и карточки. Пользователи могут отправлять боту форматированный текст и изображения. Вы можете указать тип содержимого, которое бот может обрабатывать, на странице параметров Microsoft Teams для вашего бота.

| Формат | От пользователя к боту  | От бота к пользователю |  Примечания |
| --- | :---: | :---: | --- |
| Форматированный текст  | ✔ | ✔ |  |
| Изображения | ✔ | ✔ | Размер не должен превышать 1024×1024 МБ и 1 МБ в формате PNG, JPEG или GIF. GIF с анимацией не поддерживается. |
| Карточки | ✖ | ✔ | Сведения о поддерживаемых карточках см. в [Справочнике по карточкам Teams](~/task-modules-and-cards/cards/cards-reference.md). |
| Эмодзи | ✖ | ✔ | В настоящее время Teams поддерживает эмодзи через UTF-16, например U+1F600 для ухмыляющейся рожицы. |
|

Дополнительные сведения о типах взаимодействия с ботами, поддерживаемых Bot Framework, на которых основаны боты в Teams, см. в документации по Bot Framework о [потоке беседы](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true), и связанных понятиям в документации по [пакету SDK для Bot Builder для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) и [пакету SDK для Bot Builder для Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Форматирование сообщения

Можно задать необязательное свойство [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) для `message`, чтобы управлять отображением текстового содержимого сообщения. Подробное описание поддерживаемого форматирования в сообщениях ботов см. в разделе [Форматирование сообщений](~/resources/bot-v3/bots-message-format.md).
Можно задать необязательное свойство [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true), чтобы управлять отображением текстового содержимого сообщения.

Подробные сведения о том, Teams поддерживает форматирование текста в командах, см. в разделе [Форматирование текста в сообщениях бота](~/resources/bot-v3/bots-text-formats.md).

Дополнительные сведения о форматировании карточек в сообщениях см. в разделе [Форматирование карточек](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Сообщения с картинкой

Картинки отправляются путем добавления вложений к сообщению. Дополнительные сведения о вложениях см. в [документации по Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).

Размер рисунков не должен превышать 1024×1024 МБ и 1 МБ в формате PNG, JPEG или GIF. GIF с анимацией не поддерживается.

Рекомендуется указать высоту и ширину каждого изображения с помощью XML. При использовании Markdown размер изображения по умолчанию — 256×256. Например:

* Используйте `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Получение сообщений

В зависимости от объявленных областей бот может получать сообщения в следующих контекстах:

* **личный чат**. Пользователи могут взаимодействовать с ботом в приватной беседе, просто выбрав добавленного бота в истории чата или введя его имя или идентификатор приложения в поле "Кому:" в новом чате.
* **Каналы**. Бот может быть упомянут в канале (@*botname*), если он был добавлен в команду. Обратите внимание, что дополнительные ответы боту в канале требуют упоминания бота. Бот не будет отвечать на ответы, в которых он не упоминается.

Для входящих сообщений бот получает объект [Действие](../../../bots/how-to/conversations/conversation-messages.md) типа `messageType: message`. Хотя объект `Activity` может содержать другие типы информации, например [обновления каналов](~/resources/bot-v3/bots-notifications.md#channel-updates), отправляемые боту, тип `message` представляет собой связь между ботом и пользователем.

Бот получает полезные данные, содержащие сообщение пользователя `Text`, а также другие сведения о пользователе, источнике сообщения и сведения о Teams. Следует отметить:

* `timestamp` Дата и время сообщения в формате UTC.
* `localTimestamp` Дата и время сообщения в часовом поясе отправителя.
* `channelId`Всегда "msteams". Это относится к каналу bot framework, а не к каналу Teams.
* `from.id` Уникальный и зашифрованный идентификатор этого пользователя для бота; подходит в качестве ключа, если вашему приложению необходимо хранить пользовательские данные. Он уникален для вашего бота и не может использоваться напрямую вне вашего экземпляра бота любым значимым способом для идентификации этого пользователя.
* `channelData.tenant.id` Идентификатор клиента для пользователя.

> [!NOTE]
> `from.id` уникален для вашего бота и не может использоваться напрямую вне вашего экземпляра бота любым значимым способом для идентификации этого пользователя.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Объединение каналов и личных взаимодействий с ботом

При взаимодействии в канале бот должен уметь переводить определенные беседы с пользователем в автономный режим. Например, предположим, что пользователь пытается координировать сложную задачу, такую как планирование, с группой участников группы. Вместо того, чтобы отображать всю последовательность взаимодействий на канале, рассмотрите возможность отправки пользователю личного сообщения в чате. Бот должен иметь возможность легко переключать пользователя между личными беседами и беседами в канале беспроблемно.

> [!NOTE]
>Не забудьте обновить канал после завершения взаимодействия, чтобы уведомить других участников группы.

## <a name="full-inbound-schema-example"></a>Пример полной входящей схемы

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
> Текстовое поле для входящих сообщений иногда содержит упоминания. Обязательно проверьте и удалите их. Дополнительные сведения см. в разделе [Упоминания](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Данные канала Teams

Объект `channelData` содержит сведения, относящиеся к Teams, и является окончательным источником идентификаторов команд и каналов. Эти идентификаторы следует кэшировать и использовать в качестве ключей для локального хранилища.

Типичный объект channelData в действии, отправленном боту, содержит следующие сведения:

* `eventType` Тип события Teams, который передается только в случае [событий изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `tenant.id` Идентификатор клиента Microsoft Azure Active Directory (Azure AD), который передается во всех контекстах.
* `team` Передается только в контекстах канала, а не в личном чате.
  * `id` Глобальный уникальный ИД канала.
  * `name`Название команды, которое передается только в случаях [командного переименования событий](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` Передается только в контексте канала при упоминании бота или для событий в каналах в командах, где бот был добавлен.
  * `id` Глобальный уникальный ИД канала.
  * `name` Название канала, которое передается только в случае [событий изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `channelData.teamsTeamId` Устарело. Это свойство включено только для обратной совместимости.
* `channelData.teamsChannelId` Устарело. Это свойство включено только для обратной совместимости.

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

Пакет [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) предоставляет специализированный объект `TeamsChannelData`, который предоставляет свойства для доступа к сведениям, относящимся к Teams.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Отправка ответов на сообщения

Чтобы ответить на существующее сообщение, вызовите [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) .NET или [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) Node.js. Пакет SDK Bot Builder обрабатывает все сведения.

Если вы решите использовать REST API, также можно вызвать конечную точку [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true).

Само содержимое сообщения может содержать простой текст или некоторые [карточки и действия с карточками](~/task-modules-and-cards/cards/cards-actions.md), предоставленные Bot Framework.

Обратите внимание, что в исходящей схеме вы всегда должны использовать ту же схему `serviceUrl`, что и полученную. Имейте в виду, что значение `serviceUrl` имеет тенденцию быть стабильным, но может измениться. Когда приходит новое сообщение, ваш бот должен проверить сохраненное значение `serviceUrl`.

## <a name="updating-messages"></a>Обновление сообщений

Вместо того, чтобы ваши сообщения были статическими снимками данных, бот может динамически обновлять сообщения после их отправки. Динамические обновления сообщений можно использовать для таких сценариев, как обновление опроса, изменение доступных действий после нажатия кнопки или любое другое асинхронное изменение состояния.

Новое сообщение не обязательно должно совпадать с исходным по типу. Например, если исходное сообщение содержало вложение, новое сообщение может быть простым текстовым сообщением.

> [!NOTE]
> Вы можете обновлять только содержимое, отправленное в сообщениях с одним вложением и макетах карусели. Публикация обновлений сообщений с несколькими вложениями в макете списка не поддерживается.

### <a name="rest-api"></a>REST API

Чтобы выпустить обновление сообщения, просто выполните запрос PUT к конечной точке `/v3/conversations/<conversationId>/activities/<activityId>/` с использованием заданного ИД действия. Для выполнения этого сценария необходимо кэшировать идентификатор действия, возвращенный исходным вызовом POST.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Пример .NET

Метод `UpdateActivityAsync` можно использовать в пакете SDK Bot Builder для обновления существующего сообщения.

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

### <a name="nodejs-example"></a>Пример Node.js

Метод `session.connector.update` можно использовать в пакете SDK Bot Builder для обновления существующего сообщения.

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

Вы можете создать личную беседу с пользователем или начать новую цепочку ответов в канале для бота группы. Это позволяет отправлять сообщения пользователю или пользователям, при этом им не требуется сначала инициировать контакт с ботом. Дополнительные сведения см. в следующих статьях:

Дополнительные сведения о беседах, запущенных ботами, см. в разделе [Упреждающий обмен сообщениями для ботов](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).

## <a name="deleting-messages"></a>Удаление сообщений

Сообщения можно удалить с помощью метода соединителей [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html) в [пакете SDK BotBuilder](/bot-framework/bot-builder-overview-getstarted).

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
