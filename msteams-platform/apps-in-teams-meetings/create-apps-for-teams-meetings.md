---
title: Необходимые условия и ссылки на API для приложений в собраниях Teams
author: surbhigupta
description: Работа с приложениями для Teams собраний
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams apps meetings user participant role api
ms.openlocfilehash: 38a7a5fdf9794fb95b4141f2c73e8282a9bf8601
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211592"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a>Необходимые условия и ссылки на API для приложений в собраниях Teams

Чтобы расширить возможности ваших приложений на протяжении жизненного цикла собраний, Teams позволяет работать с приложениями для Teams собраний. Необходимо пройти необходимые условия и использовать ссылки API приложений для собраний для улучшения работы с собраниями.

## <a name="prerequisites"></a>Необходимые компоненты

Прежде чем работать с приложениями для Teams собраний, необходимо иметь представление о следующем:

* Вы должны иметь знания о разработке Teams приложений. Дополнительные сведения см. [в Teams разработки приложения.](../overview.md)

* Необходимо обновить манифест Teams, чтобы указать, что приложение доступно для собраний. Дополнительные сведения см. в [манифесте приложения.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)

* Ваше приложение должно поддерживать настраиваемые вкладки в области группового чата, чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки. Дополнительные сведения см. в [поле groupchat и](../resources/schema/manifest-schema.md#configurabletabs) [создайте вкладку группы.](../build-your-first-app/build-channel-tab.md)

* Необходимо придерживаться общих Teams правил разработки вкладок для сценариев до и после собрания. Для работы во время собраний обратитесь к вкладке на собрании и рекомендациям по проектированию диалогов на собрании. Дополнительные сведения см. [Teams](../tabs/design/tabs.md)руководства по разработке вкладок, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)рекомендации по проектированию вкладок на собрании и рекомендации по проектированию диалогов на [собрании.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Необходимо поддерживать область, чтобы включить приложение в чаты перед собранием и `groupchat` после собрания. С помощью предварительного собрания приложения можно найти и добавить приложения для собраний и выполнить задачи перед собранием. С помощью приложения после собрания можно просмотреть результаты собрания, такие как результаты опроса или отзывы.

* Параметры URL-адресов API должны иметь `meetingId` и `userId` `tenantId` . Они доступны в рамках Teams клиентской SDK и бот-активности. Кроме того, вы можете получить достоверную информацию для идентификации пользователя и идентификации клиента с помощью вкладки [SSO authentication.](../tabs/how-to/authentication/auth-aad-sso.md)

* API `GetParticipant` должен иметь регистрацию бота и ID для создания маркеров auth. Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)

* Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании. Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания. Параметр завершения в диалоговом окне на собрании `bot Id` см. в `NotificationSignal` API.

* API сведений о собраниях должен иметь регистрацию бота и бот-ID. Для этого требуется бот SDK для получения `TurnContext` .

* Для событий собраний в режиме реального времени необходимо ознакомиться с объектом, доступным `TurnContext` через SDK Bot. Объект `Activity` содержит `TurnContext` полезной нагрузки с фактическим временем начала и окончания. Для проведения собраний в режиме реального времени требуется зарегистрированный бот-ИД с Teams платформы.

После того как вы прошли необходимые условия, вы можете использовать ссылки API приложений собраний , и API сведений о собраниях, которые позволяют получать доступ к информации с помощью атрибутов и отображать соответствующий `GetUserContext` `GetParticipant` `NotificationSignal` контент.

## <a name="meeting-apps-api-references"></a>Ссылки на API приложений для собраний

Новые функции собраний предоставляют API, которые преобразовывают возможности собраний. С помощью этой новой возможности можно создавать приложения или интегрировать существующие приложения в жизненный цикл собрания. Вы можете использовать API для того, чтобы ваше приложение знало о собрании. Вы можете выбрать API, которые необходимо использовать для повышения качества работы собраний.

В следующей таблице приводится список этих API:

|API|Описание|Запрос|Источник|
|---|---|----|---|
|**GetUserContext**| Этот API позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams. |_**microsoftTeams.getContext() => { /*...* / } )**_|Microsoft Teams Клиентская SDK|
|**GetParticipant**| Этот API позволяет боту получать сведения о участниках, встречая ID и ID участника. |**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота. Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|
|**Сведения о собрании** | Этот API позволяет получать статические метаданные собраний. |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |

### <a name="getusercontext-api"></a>GetUserContext API

Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в этой Teams [контексте.](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library) `meetingId`используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * Не кэшить роли участников, так как организатор собрания может изменить роли в любое время.
> * Teams в настоящее время не поддерживает большие списки рассылки или размеры реестра более 350 участников `GetParticipant` для API.

API позволяет боту получать сведения о `GetParticipant` участниках, встречая ID и ID участника. API включает параметры запросов, примеры и коды ответа.

#### <a name="query-parameters"></a>Параметры запроса

API `GetParticipant` включает следующие параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK.|
|**participantId**| String | Да | ID участника — это пользовательский ИД. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID участника из SSO Tab. |
|**tenantId**| Строка | Да | Для пользователей-клиентов требуется ID клиента. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID клиента из SSO tab. |

#### <a name="example"></a>Пример

API `GetParticipant` содержит следующие примеры:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}

```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

---

Тело ответа JSON для `GetParticipant` API:

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "isGroup":true
   }
}
```

#### <a name="response-codes"></a>Коды ответа

API `GetParticipant` включает в себя следующие коды ответа:

|Код ответа|Описание|
|---|---|
| **403** | Приложение не может получать сведения о участниках. Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании. Например, если приложение отключено администратором клиента или заблокировано во время переноса веб-сайтов в прямом эфире.|
| **200** | Данные участника успешно извлекаются.|
| **401** | Приложение отвечает недействительным маркером.|
| **404** | Собрание истеко или участник не может быть найден.|
| **500** | Срок действия собрания истек (более 60 дней) с момента окончания собрания, или у участников нет разрешений, основанных на их роли.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.

> [!NOTE]
> * При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.
> * В настоящее время отправка целевых уведомлений не поддерживается.

`NotificationSignal` API позволяет предоставлять сигналы собраний, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота. Этот API позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно в собрании. API включает параметр запроса, примеры и коды ответа.

#### <a name="query-parameter"></a>Параметр запроса

API `NotificationSignal` включает в себя следующий параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| Строка | Да | Идентификатор беседы доступен в рамках Bot Invoke. |

#### <a name="examples"></a>Примеры

Объявляется `Bot ID` в манифесте, и бот получает объект результата.

> [!NOTE]
> * Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки. `Bot ID` объявляется в манифесте, и бот получает объект результата.
> * Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях. Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)
> * URL-адрес — это страница, загруженная в диалоговом окне на `<iframe>` собрании. Домен должен быть в массиве приложения в `validDomains` манифесте приложения.

API `NotificationSignal` содержит следующие примеры:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

# <a name="json"></a>[JSON](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

---

#### <a name="response-codes"></a>Коды ответа

API `NotificationSignal` включает в себя следующие коды ответа:

|Код ответа|Описание|
|---|---|
| **201** | Успешно отправляется действие с сигналом. |
| **401** | Приложение отвечает недействительным маркером. |
| **403** | Приложение не может отправить сигнал. Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее. В этом случае полезное сообщение содержит подробное сообщение об ошибке. |
| **404** | Чат собрания не существует. |

### <a name="meeting-details-api"></a>API сведений о собраниях

> [!NOTE]
> В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.

API сведений о собраниях позволяет приложению получать статические метаданные собраний. Это точки данных, которые не изменяются динамически.
API доступен через службы ботов.

#### <a name="prerequisite"></a>Обязательное условие

Чтобы использовать API сведений о собраниях, необходимо получить разрешения RSC. Чтобы настроить свойство манифеста приложения, используйте следующий `webApplicationInfo` пример:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a>Параметр запроса

API сведений о собраниях включает в себя следующий параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK. |

#### <a name="example"></a>Пример

API сведений о собраниях содержит следующие примеры:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
var connectorClient = parameters.TurnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

Недоступно

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

---

The JSON response body for Meeting Details API is as follows:

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="real-time-teams-meeting-events"></a>События Teams в режиме реального времени

> [!NOTE]
> В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.

Пользователь может получать события собраний в режиме реального времени. Как только любое приложение связано с собранием, фактическое время начала и окончания собрания передается боту.

Фактическое время начала и окончания собрания отличается от запланированного времени начала и окончания. API сведений о собрании предоставляет запланированное время начала и окончания, а событие предоставляет фактическое время начала и окончания.

### <a name="prerequisite"></a>Обязательное условие

Манифест приложения должен иметь свойство для получения событий `webApplicationInfo` начала и окончания собрания. Чтобы настроить манифест, используйте следующий пример:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

### <a name="example-of-meeting-start-event-payload"></a>Пример полезной нагрузки на начало собрания

В следующем коде приводится пример полезной нагрузки на событие начала собрания:

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id":"meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a>Пример полезной нагрузки конечного события собрания

В следующем коде приводится пример полезной нагрузки на конечные события собрания:

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-getting-metadata-of-a-meeting"></a>Пример получения метаданных собрания

Ваш бот получает событие через `OnEventActivityAsync` обработник.

Для десерализации полезной нагрузки json для получения метаданных собрания вводится объект модели. Метаданные собрания находятся в свойстве `value` в полезной нагрузке события. Создается объект модели, переменные члена которого соответствуют клавишам, которые находятся под свойством `MeetingStartEndEventvalue` `value` в полезной нагрузке события.

В следующем коде показано, как захватить метаданные собрания , , , и от `MeetingType` начала и окончания собрания `Title` `Id` `JoinUrl` `StartTime` `EndTime` события:

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

MeetingStartEndEventvalue.cs содержит следующий код:

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a>Пример кода

|Пример имени | Описание | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| Разнонасть собраний | Microsoft Teams для прохождения маркеров. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Бот-бот для пузырьков контента для собраний | Microsoft Teams для взаимодействия с ботом пузырьков контента на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Собрание MeetingSidePanel | Microsoft Teams для взаимодействия с боковой панелью на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Вкладка "Сведения в собрании" | Microsoft Teams для итерактинга с помощью вкладки Подробные сведения на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a>См. также

* [Рекомендации по проектированию диалогов на собрании](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams потока проверки подлинности для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Приложения для Teams собраний](teams-apps-in-meetings.md)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Включить и настроить приложения для Teams собраний](enable-and-configure-your-app-for-teams-meetings.md)
