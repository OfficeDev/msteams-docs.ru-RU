---
title: Справочные материалы по API приложений для собраний
author: surbhigupta
description: Определение ссылок API приложений собраний с примерами и примерами кода
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams apps meetings user participant role api usercontext notification signal signal query
ms.openlocfilehash: dd46dc2622915055e46e07ae34d48c690d6d8d8e
ms.sourcegitcommit: 58a24422bb04a529b6629a56803ed2efabc17cb1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2022
ms.locfileid: "62323150"
---
# <a name="meeting-apps-api-references"></a>Справочные материалы по API приложений для собраний

Extensibilities собрания предоставляют API для преобразования опыта собраний:

* Создание приложений или интеграция существующих приложений в течение жизненного цикла собраний.
* Используйте API, чтобы сделать ваше приложение осведомленным о собрании.
* Выберите API, которые необходимо использовать для повышения качества работы собраний.

В следующей таблице приводится список API:

|API|Описание|Запрос|Источник|
|---|---|----|---|
|**GetUserContext**| Позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams. |_**microsoftTeams.getContext() => {/*...* / } )**_|Microsoft Teams клиента SDK|
|**GetParticipant**| Позволяет боту получать сведения о участниках путем собрания ИД и ИД участника. |**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота. Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|
|**Сведения о собрании** | Позволяет получать статические метаданные собраний. |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |
|**CART**|Позволяет размещать подписи на собрании, которое было начато.|**POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=ru-ru HTTP/1.1**|Microsoft Teams клиента SDK|

## <a name="getusercontext-api"></a>GetUserContext API

Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в тексте получить контекст для вкладки [Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` Используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.

## <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * Не кэшить роли участников, так как организатор собрания может изменить роли в любое время.
> * Teams в настоящее время не поддерживает большие списки рассылки или размеры реестра более 350 участников `GetParticipant` API.

API `GetParticipant` позволяет боту получать сведения о участниках, встречая ID и ID участника. API включает параметры запросов, примеры и коды ответа.

### <a name="query-parameters"></a>Параметры запроса

API `GetParticipant` включает следующие параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK.|
|**participantId**| String | Да | ID участника — это пользовательский ИД. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID участника из SSO tab. |
|**tenantId**| Строка | Да | Для пользователей-клиентов требуется ID клиента. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID клиента из SSO tab. |

### <a name="example"></a>Пример

API `GetParticipant` содержит следующие примеры:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = await TeamsInfo.GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourParticipantTenantId").ConfigureAwait(false);
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

### <a name="response-codes"></a>Коды ответа

API `GetParticipant` возвращает следующие коды ответа:

|Код ответа|Описание|
|---|---|
| **403** | Сведения о участниках не делятся с приложением. Если приложение не установлено на собрании, оно вызывает наиболее распространенный ответ на ошибку 403. Если администратор клиента отключает или блокирует приложение во время переноса веб-сайта в прямом эфире, запускается ответ на ошибку 403. |
| **200** | Данные участника успешно извлекаются.|
| **401** | Приложение отвечает недействительным маркером.|
| **404** | Собрание истеко или участник не может быть найден.|

## <a name="notificationsignal-api"></a>NotificationSignal API

Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.

> [!NOTE]
> * При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.
> * В настоящее время отправка целевых уведомлений не поддерживается.

`NotificationSignal` API позволяет предоставлять сигналы собраний, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота. Этот API позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно в собрании. API включает параметр запроса, примеры и коды ответа.

### <a name="query-parameter"></a>Параметр запроса

API `NotificationSignal` включает в себя следующий параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| Строка | Да | Идентификатор беседы доступен в рамках Bot Invoke. |

### <a name="examples"></a>Примеры

Объявляется `Bot ID` в манифесте, и бот получает объект результата.

> [!NOTE]
> * Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки. `Bot ID` объявляется в манифесте, и бот получает объект результата.
> * Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях. Чтобы гарантировать, что размеры находятся в пределах допустимого, см. [в рекомендациях по проектированию](design/designing-apps-in-meetings.md).
> * URL-адрес — это страница, загруженная в `<iframe>` диалоговом окне на собрании. Домен должен быть в массиве приложения `validDomains` в манифесте приложения.

API `NotificationSignal` содержит следующие примеры:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");
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

### <a name="response-codes"></a>Коды ответа

API `NotificationSignal` включает в себя следующие коды ответа:

|Код ответа|Описание|
|---|---|
| **201** | Успешно отправляется действие с сигналом. |
| **401** | Приложение отвечает недействительным маркером. |
| **403** | Приложение не может отправить сигнал. Код ответа 403 может возникать по различным причинам, например, администратор клиента отключает и блокирует приложение во время переноса веб-сайтов в прямом эфире. В этом случае полезное сообщение содержит подробное сообщение об ошибке. |
| **404** | Чат собраний не существует. |

## <a name="meeting-details-api"></a>API сведений о собраниях

> [!NOTE]
> В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.

API сведений о собраниях позволяет приложению получать статические метаданные собраний. Метаданные предоставляют точки данных, которые не изменяются динамически.
API доступен через службы ботов.

### <a name="prerequisite"></a>Предварительное условие

> [!NOTE] 
> Проверьте, соответствует ли ваше приложение всем необходимым требованиям, указанным в необходимых для приложений Teams [собраниях](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md).

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
### <a name="query-parameter"></a>Параметр запроса

API сведений о собраниях включает в себя следующий параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK. |

### <a name="example"></a>Пример

API сведений о собраниях содержит следующие примеры:

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
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

## <a name="cart-api"></a>API КОРЗИНЫ

API доступа к общению в режиме реального времени предоставляет конечную точку POST для подписей Microsoft Teams CART, закрытых подписей на человеческом типе. Текстовое содержимое, отправленное в эту конечную точку, отображается конечным пользователям на собрании Microsoft Teams при включении подписей.

### <a name="cart-url"></a>URL-адрес КОРЗИНЫ

URL-адрес КОРЗИНЫ конечной точки POST можно получить на странице  Параметры собрания в Microsoft Teams собрании. Дополнительные сведения см. в [подписях CART в Microsoft Teams собрании](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47). Вам не нужно изменять URL-адрес КОРЗИНЫ для использования подписей CART.

#### <a name="query-parameter"></a>Параметр запроса

URL-адрес CART содержит следующие параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|----|
|**meetingId**| String | Да |Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK. <br/>Например, meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-42411-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%22%22mId%22%22%3a%220%22%7d|
|**маркер**| String | Да |Маркер авторизации.<br/> Например, token=04751eac |

#### <a name="example"></a>Пример

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>Метод

|Ресурс|Метод|Описание|
|----|----|----|
|/cartcaption|POST|Обработка подписей для собрания, которое было начато|

> [!NOTE]
> Убедитесь, что тип контента для всех запросов является простым текстом с кодификатом UTF-8. В теле запроса содержатся только подписи.

#### <a name="example"></a>Пример

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> Каждый запрос POST создает новую строку подписей. Чтобы у конечных пользователей было достаточно времени для чтения контента, ограничив каждое тело запроса POST 80-120 символами.

### <a name="error-codes"></a>Коды ошибок

API CART включает следующие коды ошибок:

|Код ошибки|Описание|
|---|---|
| **400** | Плохой запрос. В органе ответа есть дополнительные сведения. Например, не все представленные параметры.|
| **401** | Несанкционированный. Плохой или просроченный маркер. Если вы получили эту ошибку, сгенерировать новый URL-адрес КОРЗИНЫ в Teams. |
| **404** | Собрание не найдено или не началось. Если вы получили эту ошибку, убедитесь, что вы начинаете собрание и выберите подписи к началу. После включения подписей на собрании можно приступить к poSTing подписям в собрании.|
| **500** |Внутренняя ошибка сервера. Дополнительные сведения можно получить [в службе поддержки контактов или предоставить обратную связь](../feedback.md).|

## <a name="real-time-teams-meeting-events"></a>События Teams в режиме реального времени

Пользователь может получать события собраний в режиме реального времени. Как только любое приложение связано с собранием, фактическое время начала и окончания собрания передается боту.

Фактическое время начала и окончания собрания отличается от запланированного времени начала и окончания. API сведений о собраниях предоставляет запланированное время начала и окончания. Событие предоставляет фактическое время начала и окончания.

### <a name="prerequisite"></a>Предварительное условие

> [!NOTE] 
> Проверьте, соответствует ли ваше приложение всем необходимым требованиям, указанным в необходимых для приложений Teams [собраниях](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md).

Манифест приложения должен иметь свойство для `webApplicationInfo` получения событий начала и окончания собрания. Чтобы настроить манифест, используйте следующий пример:

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
        "Id": "meeting id", 
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

Ваш бот получает событие через обработник `OnEventActivityAsync` .

Для десерализации полезной нагрузки json для получения метаданных собрания вводится объект модели. Метаданные собрания в свойстве `value` в полезной нагрузке события. Создается `MeetingStartEndEventvalue` объект модели, переменные члена которого соответствуют клавишам, которые находятся под `value` свойством в полезной нагрузке события.
     
> [!NOTE]      
> * Получите ID собрания из `turnContext.ChannelData`.    
> * Не используйте ИД беседы в качестве ИД собрания.     
> * Не используйте ID собрания из полезной нагрузки на события собраний `turncontext.activity.value`. 
      
В следующем коде показано, `MeetingType`как захватить метаданные собрания, которое является , `Title`, , `Id`, , `JoinUrl`и `EndTime` `StartTime`из события начала и конца собрания:

Событие "Начало собрания"
```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

Событие конца собрания
```csharp
protected override async Task OnTeamsMeetingEndAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js | 
|----------------|-----------------|--------------|--------------|
| Разнонасть собраний | Microsoft Teams для прохождения маркеров. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Бот-бот для пузырьков контента для собраний | Microsoft Teams для взаимодействия с ботом пузырьков контента на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Собрание MeetingSidePanel | Microsoft Teams для взаимодействия с боковой панелью на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Вкладка "Сведения в собрании" | Microsoft Teams для взаимодействия с вкладками Details in-meeting. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|Пример событий собраний|Пример приложения для демонстрации событий Teams собраний в режиме реального времени|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|Пример набора собраний|Пример приложения для демонстрации опыта собраний для сценария набора персонала.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|Установка приложения с помощью кода QR|Пример приложения, которое создает код QR и устанавливает приложение с помощью кода QR|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|


## <a name="see-also"></a>Дополнительные ресурсы

* [Teams потока проверки подлинности для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Приложения для собраний Teams](teams-apps-in-meetings.md)

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Включить и настроить приложения для Teams собраний](enable-and-configure-your-app-for-teams-meetings.md)
