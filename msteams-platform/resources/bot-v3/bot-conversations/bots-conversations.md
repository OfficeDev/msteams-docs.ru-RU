---
title: Отправка и получение сообщений с помощью Bot
description: Сведения о том, как отправлять и получать сообщения с помощью боты в Microsoft Teams
keywords: Боты сообщения Teams
ms.date: 05/20/2019
ms.openlocfilehash: 864473c7f502d96987a48e5837840236c45f59c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675656"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Беседа с роботом Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Беседа — это серия сообщений, отправляемых между Bot и одним или несколькими пользователями. В Teams существует три вида бесед (также называемых областями):

* `teams`Также называется каналы каналов, видимых всем участникам канала.
* `personal`Беседы между Боты и одним пользователем.
* `groupChat`Чат между Bot и двумя или несколькими пользователями.

В зависимости от типа беседы, в которой она участвует, программа-робота немного ведет себя по-разному.

* Для [боты в беседах в канале и группе](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) необходимо, чтобы пользователь "@" привызывал его в канале.
* Для [боты в беседах с одним пользователем](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) не требуется @ упоминание, что пользователь может просто ввести.

Чтобы элемент Bot мог работать в определенной области, он должен быть указан в манифесте как поддерживающий эту область в манифесте. Области определены и обсуждаются в [справочнике по манифесту](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Упреждающие сообщения

Боты могут участвовать в беседе или инициировать ее. Большая часть обмена сообщениями заключается в ответ на другое сообщение. Если программа-робот инициирует беседу, она называется *упреждающим сообщением*. Примеры:

* Приветственные сообщения
* Уведомления о событиях
* Опрос сообщений

## <a name="conversation-basics"></a>Общие сведения о беседах

Каждое сообщение является `Activity` объектом типа `messageType: message`. Когда пользователь отправляет сообщение, Teams отправляет сообщение на сервер почтовых роботов; в частности, он отправляет объект JSON в конечную точку обмена сообщениями ленты. Ваш почтовый робот просматривает сообщение, чтобы определить его тип и ответить соответствующим образом.

Боты также поддерживает сообщения в стиле события. Более подробную информацию можно узнать [в статье обработка событий Bot в Microsoft Teams](~/resources/bot-v3/bots-notifications.md) . В настоящее время речь не поддерживается.

Сообщения для большинства областей имеют одинаковое значение, но существуют различия в доступе к интерфейсу Bot в пользовательском интерфейсе и различиях в сценах, о которых необходимо знать.

Основная беседа обрабатывается через соединитель Bot Framework, один REST API, позволяющий роботам общаться с Teams и другими каналами. Пакет SDK построителя позволяет легко получить доступ к этому API, дополнительные функции для управления движением и состоянием беседы, а также простые способы внедрения таких служб, как естественный язык (НЛП).

## <a name="message-content"></a>Содержимое сообщения

Ваш робот может отправлять форматированный текст, изображения и карточки. Пользователи могут отправлять форматированный текст и изображения в Bot. Вы можете указать тип контента, который может обработать пользователь Bot, на странице параметров Microsoft Teams для ленты.

| Format | От пользователя к Bot  | От Bot к пользователю |  Примечания |
| --- | :---: | :---: | --- |
| Форматированный текст  | ✔ | ✔ |  |
| Изображения | ✔ | ✔ | Не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается |
| Карточки | ✖ | ✔ | Поддерживаемые карточки представлены в [справочнике по карточке Teams](~/task-modules-and-cards/cards/cards-reference.md) |
| Эмодзи | ✖ | ✔ | В настоящее время Teams поддерживает эмодзи, используя кодировку UTF-16 (например, U + 1F600 для гриннинг Face) |
|

Для получения дополнительных сведений о типах взаимодействий с Bot, поддерживаемых с помощью Bot Framework (которые основаны на Боты в Teams), ознакомьтесь с документацией по среде Bot по [цепочке обсуждений](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) и связанными понятиями, изложенными в документации по [пакету SDK для программы Bot Builder для .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) и [пакету SDK построителя для Node. js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).

## <a name="message-formatting"></a>Форматирование сообщений

Можно задать необязательное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) свойство элемента, `message` чтобы управлять отображением текстового контента сообщения. В статье [Форматирование сообщений](~/resources/bot-v3/bots-message-format.md) представлено подробное описание поддерживаемого форматирования в сообщениях Bot.
Можно задать необязательное [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) свойство, чтобы управлять отображением текстового контента сообщения.

Подробные сведения о том, как teams поддерживает форматирование текста в Teams, см [в разделе Форматирование текста в сообщениях Bot](~/resources/bot-v3/bots-text-formats.md).

Сведения о форматировании карточек в сообщениях можно узнать в статье [Форматирование карточки](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Графические сообщения

Изображения отправляются путем добавления вложений к сообщению. Дополнительные сведения о вложениях можно найти в [документации по среде Bot](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).

Рисунки могут иметь не более 1024 × 1024 и 1 МБ в формате PNG, JPEG или GIF; анимированный GIF-файл не поддерживается.

Рекомендуем указать высоту и ширину каждого изображения с помощью XML. Если вы используете Markdown, размер изображения по умолчанию равен 256 × 256. Пример:

* Используйте`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Не используйте `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Получение сообщений

В зависимости от того, какие области объявляются, Bot может получать сообщения в следующих контекстах:

* **Личный чат** Пользователи могут общаться в частном разговоре с помощью ленты, просто выбрав добавленного элемента Bot в журнале чата или введя его имя или идентификатор приложения в поле Кому: в новом сеансе разговора.
* **Каналы** Вы можете упомянуть в канале ("@_ботнаме_"), если она была добавлена в команду. Обратите внимание, что для дополнительных ответов на канале Bot в канале требуется упоминание Bot. Он не реагирует на ответы, где он не упоминается.

Для входящих сообщений Bot получает [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) объект типа. `messageType: message` Несмотря на `Activity` то, что объект может содержать другие типы информации, например [обновления канала](~/resources/bot-v3/bots-notifications.md#channel-updates) , отправляемые в `message` Bot, тип представляет связь между Bot и пользователем.

Ваш Bot получает полезные данные, содержащие сообщение `Text` пользователя, а также другие сведения о пользователе, источник сообщения и сведения о Teams. Примечание:

* `timestamp`Дата и время сообщения в формате всемирного координированного времени (UTC).
* `localTimestamp`Дата и время сообщения в часовом поясе отправителя
* `channelId`Всегда "мстеамс". Это относится к каналу Bot Framework, а не к каналу Teams.
* `from.id`Уникальный и зашифрованный идентификатор пользователя для ленты. подходит в качестве ключа, если ваше приложение должно хранить пользовательские данные. Он уникален для почтового робота и не может использоваться непосредственно за престоронним экземпляром Bot с помощью какого-либо осмысленного способа идентификации этого пользователя
* `channelData.tenant.id`Идентификатор клиента для пользователя.

> [!NOTE]
> `from.id`является уникальным для почтового робота и не может использоваться непосредственно за престоронним экземпляром Bot с помощью какого-либо осмысленного способа идентификации этого пользователя.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Объединение каналов и частных взаимодействий с Bot

При взаимодействии с каналом Bot должен быть разумным, чтобы принимать определенные беседы в автономном режиме с пользователем. Например, предположим, что пользователь пытается координировать сложную задачу, например планирование с набором участников группы. Вместо того чтобы всю последовательность взаимодействий, видимых каналу, рассмотрите возможность отправки пользователю личного сообщения разговора. Ваш робот должен легко перевести пользователя между личными и каналами бесед без потери состояния.

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
> Текстовое поле для входящих сообщений иногда содержит упоминания. Обязательно проверьте и извлеките их. Дополнительные сведения [см.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)

## <a name="teams-channel-data"></a>Данные канала Teams

`channelData` Объект содержит сведения, зависящие от команды, и является основным источником для идентификаторов команд и каналов. Вы должны кэшировать и использовать эти идентификаторы в качестве ключей для локального хранилища.

Этот `channelData` объект не включается в сообщения в личных беседах, так как они выполняются вне какого-либо канала.

Типичный объект Чаннелдата в действии, отправляемом на почтовый робот, содержит следующие сведения:

* `eventType`Тип события Teams; передается только в случае [событий изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id`Идентификатор клиента Azure Active Directory; передается во всех контекстах
* `team`Передается только в контекстах канала, а не в личном сеансе чата.
  * `id`GUID для канала
  * `name`Имя команды; передается только в случае [событий переименования команды](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel`Передается только в контекстах канала при упоминании Bot или для событий в каналах в Microsoft Teams, где добавлен Bot
  * `id`GUID для канала
  * `name`Имя канала; передается только в случае [событий изменения канала](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `channelData.teamsTeamId`Устаревшие. Это свойство включено только для обеспечения обратной совместимости.
* `channelData.teamsChannelId`Устаревшие. Это свойство включено только для обеспечения обратной совместимости.

### <a name="example-channeldata-object-channelcreated-event"></a>Пример объекта Чаннелдата (событие Чаннелкреатед)

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

Пакет NuGet [Microsoft. Bot. Connector. Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) предоставляет специализированный `TeamsChannelData` объект, который предоставляет свойства для доступа к сведениям, относящимся к Teams.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Отправка ответов на сообщения

Чтобы ответить на существующее сообщение, вызовите [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) его в .NET [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) или Node. js. Пакет SDK построителя построителя обрабатывает все подробные сведения.

Если вы решили использовать REST API, вы также можете вызвать [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) конечную точку.

Само содержимое сообщения может содержать простой текст или некоторые [карточки и действия карточки с](~/task-modules-and-cards/cards/cards-actions.md)Bot Framework.

Обратите внимание, что в используемой схеме исходящей почты следует `serviceUrl` всегда использовать ту же информацию, что и в полученном виде. Имейте в виду, что значение `serviceUrl` является стабильным, но может измениться. Когда поступает новое сообщение, ваш робот должен проверить сохраненное значение `serviceUrl`.

## <a name="updating-messages"></a>Обновление сообщений

Вместо того чтобы сообщения были статическими моментальными снимками данных, ваш Bot может динамически обновлять сообщения после отправки. Динамическое обновление сообщений можно использовать для таких сценариев, как обновление опросов, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.

Новое сообщение не должно быть соответствующим исходному типу. Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.

> [!NOTE]
> Вы можете обновить только содержимое, отправленное в сообщениях с одним вложением и в виде схем обоймы. Публикация обновлений сообщений с несколькими вложениями в раскладке списков не поддерживается.

### <a name="rest-api"></a>REST API

Чтобы отправить сообщение об обновлении, просто выполните запрос PUT для `/v3/conversations/<conversationId>/activities/<activityId>/` конечной точки, используя заданный идентификатор действия. Для выполнения этого сценария необходимо кэшировать идентификатор действия, возвращенный исходным вызовом POST.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Пример .NET

С помощью `UpdateActivityAsync` метода в пакете SDK построителя построителя можно обновить существующее сообщение.

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

### <a name="nodejs-example"></a>Пример Node. js

С помощью `session.connector.update` метода в пакете SDK построителя построителя можно обновить существующее сообщение.

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

Вы можете создать личный разговор с пользователем или начать новую цепочку ответа в канале для командного канала. Это позволяет отправлять сообщения пользователям и пользователям, не прибегая к ним, прежде чем приступить к работе с роботом. Дополнительную информацию см. в следующих статьях:

В этой статье приведены сведения об [активных сообщениях для Боты](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) для получения общих сведений о беседах, запущенных Боты.

## <a name="deleting-messages"></a>Удаление сообщений

Сообщения можно удалять с помощью метода Connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) в [ботбуилдер SDK](/bot-framework/bot-builder-overview-getstarted).

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
