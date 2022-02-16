---
title: Справочные материалы по API приложений для собраний
author: surbhigupta
description: Определение ссылок API приложений собраний с примерами и примерами кода
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: команды приложений собраний участника роли пользователя API запрос уведомления контекста пользователя уведомления
ms.openlocfilehash: 3dd234e99068c2d7014a04f378a131b5d325a2c8
ms.sourcegitcommit: 58f1c3e6a4fab0778ff035e0bbddcee267a0e8e2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/16/2022
ms.locfileid: "62857239"
---
# <a name="meeting-apps-api-references"></a>Справочные материалы по API приложений для собраний

Расширенная доступность собрания обеспечивает API для улучшения работы с собраниями. Вы можете выполнить следующие работы с помощью перечисленных API:

* Создание приложений или интеграция существующих приложений в течение жизненного цикла собраний.
* Используйте API, чтобы ваше приложение знало о собрании.
* Выберите необходимые API для улучшения работы с собраниями.

В следующей таблице приводится список API, доступных в Microsoft Teams клиенте (MSTC) и Microsoft Bot Framework (MSBF) SDKs:

|Метод| Описание| Source|
|---|---|----|
|[**Получить пользовательский контекст**](#get-user-context-api)| Получите контекстную информацию для отображения соответствующего контента на вкладке Teams.| MSTC SDK|
|[**Получение участника**](#get-participant-api)| Извлечение сведений о участниках с помощью ИД собрания и ИД участника. |MSBF SDK|
|[**Отправка сигнала уведомления**](#send-notification-signal-api)| Предоставление сигналов собраний с помощью существующего API уведомлений о беседе для чата пользователя-бота и позволяет уведомлять пользователя о действии, которое показывает диалоговое окно в собрании. |MSBF SDK|
|[**Сведения о собрании**](#get-meeting-details-api)| Получите статичные метаданные собрания. |MSBF SDK |
|[**Отправка подписей в режиме реального времени**](#send-real-time-captions-api)| Отправка подписей в режиме реального времени на текущее собрание. |MSTC SDK|
|[**Share app content to stage**](#share-app-content-to-stage-api)| Делитесь определенными частями приложения с этапом собрания из боковой панели приложения на собрании. |MSTC SDK|
|[**Получить состояние общего доступа к контенту приложений**](#get-app-content-stage-sharing-state-api)| Извлечение сведений о состоянии общего доступа к приложению на стадии собрания. |MSTC SDK|
|[**Получите возможности совместного доступа к контенту на этапе приложения**](#get-app-content-stage-sharing-capabilities-api)| Извлечение возможностей приложения для общего доступа на стадию собрания. |MSTC SDK|
|[**Получить в режиме реального времени Teams собрания**](#get-real-time-teams-meeting-events-api)|Извлечение событий собраний в режиме реального времени, таких как фактическое время начала и окончания.| MSBF SDK|

## <a name="get-user-context-api"></a>Получить API контекста пользователя

Чтобы определить и получить контекстную информацию для контента вкладки, см. в тексте получить контекст для вкладки [Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` Используется вкладка, запущенная в контексте собрания, и добавляется для полезной нагрузки ответа.

## <a name="get-participant-api"></a>Получить API участника

> [!NOTE]
> * Не кэшить роли участников, так как организатор собрания может изменить роли в любое время.
> * В настоящее время `GetParticipant` API поддерживается только для списков рассылки или списков с менее чем 350 участниками.

### <a name="query-parameters"></a>Параметры запроса

> [!TIP]
> Получите ID участника и ID клиента из SSO Tab.

В следующей таблице содержатся параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK.|
|**participantId**| String | Да | ID участника — это пользовательский ИД. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID участника из SSO tab. |
|**tenantId**| Строка | Да | Для пользователей-клиентов требуется ID клиента. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID клиента из SSO tab. |

### <a name="example"></a>Пример

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

В следующей таблице приводится коды ответов:

|Код ответа|Описание|
|---|---|
| **403** | Сведения о участниках не делятся с приложением. Если приложение не установлено на собрании, оно вызывает ответ на ошибку 403. Если администратор клиента отключает или блокирует приложение во время переноса веб-сайта в прямом эфире, он запускает ответ на ошибку 403. |
| **200** | Данные участника успешно извлекаются.|
| **401** | Приложение отвечает недействительным маркером.|
| **404** | Срок действия собрания истек или участники недоступны.|

## <a name="send-notification-signal-api"></a>API сигнала отправки уведомлений

Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API. `NotificationSignal` API позволяет предоставлять сигналы собраний, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота. Вы можете отправлять сигнал в зависимости от действий пользователя, диалоговое окно на собрании. API включает параметр запроса, примеры и коды ответа.

> [!NOTE]
> * При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.
> * В настоящее время отправка целевых уведомлений не поддерживается.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержатся параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| Строка | Да | Идентификатор беседы доступен в рамках Bot Invoke. |

### <a name="examples"></a>Примеры

Объявляется `Bot ID` в манифесте, и бот получает объект результата.

> [!NOTE]
> * Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки.
> * Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях. Дополнительные сведения см. [в рекомендациях по проектированию](design/designing-apps-in-meetings.md).
> * URL-адрес — это страница, которая загружается `<iframe>` , как в диалоговом окне на собрании. Домен должен быть в массиве приложений `validDomains` в манифесте приложения.

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

В следующей таблице содержатся коды ответа:

|Код ответа|Описание|
|---|---|
| **201** | Успешно отправляется действие с сигналом. |
| **401** | Приложение отвечает недействительным маркером. |
| **403** | Приложение не может отправить сигнал. Код ответа 403 может возникать по различным причинам, например, администратор клиента отключает и блокирует приложение во время переноса веб-сайтов в прямом эфире. В этом случае полезное сообщение содержит подробное сообщение об ошибке. |
| **404** | Чат собраний не существует. |

## <a name="get-meeting-details-api"></a>Получить API сведений о собраниях

API сведений о собраниях позволяет приложению получать статические метаданные собрания. Метаданные предоставляют точки данных, которые не изменяются динамически. API доступен через службы ботов. В настоящее время как частные запланированные, так и повторяющиеся собрания, а также запланированные или повторяющиеся собрания каналов поддерживают API с различными разрешениями RSC соответственно.

### <a name="prerequisite"></a>Предварительное условие

Чтобы использовать API сведений о собраниях, необходимо получить различные разрешения RSC, основанные на области любого собрания, например закрытого собрания или собрания канала.

<br>

<details>

<summary><b>Для версии манифеста приложения 1.12</b></summary>

Используйте следующий пример для настройки `webApplicationInfo` `authorization` свойств манифеста приложения для любого закрытого собрания:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]
    }
}
 ```

Используйте следующий пример для настройки `webApplicationInfo` `authorization` свойств и свойств манифеста приложения для любого собрания канала:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChannelMeeting.ReadBasic.Group",
                "type": "Application"
            }
        ]
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>Для манифеста приложения версии 1.11 или более ранней версии</b></summary>

Используйте следующий пример, чтобы настроить свойство `webApplicationInfo` манифеста приложения для любого закрытого собрания:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

Используйте следующий пример, чтобы настроить `webApplicationInfo` свойство манифеста приложения для любого собрания канала:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "ChannelMeeting.ReadBasic.Group"
    ]
}
 ```

<br>

</details>

> [!NOTE]
> Бот может получать события начала или окончания собрания автоматически со всех собраний, созданных во всех каналах, `ChannelMeeting.ReadBasic.Group` добавляя манифест для разрешения RSC.
 
### <a name="query-parameter"></a>Параметр запроса

В следующей таблице перечислены параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK. |

### <a name="example"></a>Пример

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
            "conversationType": "groupchat", 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="send-real-time-captions-api"></a>API отправки субтитров в режиме реального времени

API отправки подписей в режиме реального времени предоставляет конечную точку POST для Microsoft Teams доступа к общению в режиме реального времени( CART) подписей, закрытых подписей на человеческом типе. Текстовое содержимое, отправленное в эту конечную точку, отображается конечным пользователям на собрании Microsoft Teams при включении подписей.

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

|Resource|Метод|Описание|
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

В следующей таблице печатались коды ошибок:

|Код ошибки|Описание|
|---|---|
| **400** | Плохой запрос. В органе ответа есть дополнительные сведения. Например, не все представленные параметры.|
| **401** | Несанкционированный. Плохой или просроченный маркер. Если вы получили эту ошибку, сгенерировать новый URL-адрес КОРЗИНЫ в Teams. |
| **404** | Собрание не найдено или не началось. Если вы получили эту ошибку, убедитесь, что вы начинаете собрание и выберите подписи к началу. После включения подписей на собрании можно приступить к poSTing подписям в собрании.|
| **500** |Внутренняя ошибка сервера. Дополнительные сведения можно получить [в службе поддержки контактов или предоставить обратную связь](../feedback.md).|

## <a name="share-app-content-to-stage-api"></a>Доля контента приложения для этапа API

API `shareAppContentToStage` позволяет обмениваться определенными частями приложения на стадии собрания. API доступен через Teams клиента SDK.

### <a name="prerequisite"></a>Предварительное условие

Чтобы использовать `shareAppContentToStage` API, необходимо получить разрешения RSC. В манифесте приложения настройте свойство `authorization` , а также поле `name` и `type` в поле `resourceSpecific` . Например:

```json
"authorization": {
    "permissions": { 
    "resourceSpecific": [
      { 
      "name": "MeetingStage.Write.Chat",
      "type": "Delegated"
      }
    ]
   }
}
 ```

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержатся параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Callback содержит два параметра: ошибка и результат. Ошибка *может* содержать ошибку типа *SdkError* или null при успешном совместном окне. Результат *может* содержать истинное значение в случае успешной доли или нулевую при сбойе.|
|**appContentURL**| String | Да | URL-адрес, который будет делиться на сцене.|

### <a name="example"></a>Пример

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приводится коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет надлежащих разрешений для допуска к этапу обмена данными.|

## <a name="get-app-content-stage-sharing-state-api"></a>Получить API состояния общего состояния контента приложений

API `getAppContentStageSharingState` позволяет получать сведения о совместном использовании приложений на стадии собрания.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержатся параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| Строка | Да | Callback содержит два параметра: ошибка и результат. Ошибка *может* содержать ошибку типа *SdkError* в случае ошибки или null при успешном совместном окне. В *результате* может содержаться `AppContentStageSharingState` объект, указывающий на успешное и повторное и повторное, или null, указывающий на неудачное и повторное.|

### <a name="example"></a>Пример

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

Тело ответа JSON для `getAppContentStageSharingState` API:

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приводится коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет надлежащих разрешений для допуска к этапу обмена данными.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>Получите API возможностей обмена контентом на этапе приложения

API `getAppContentStageSharingCapabilities` позволяет извлекть возможности приложения для совместного доступа к этапу собраний.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержатся параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| Строка | Да | Callback содержит два параметра: ошибка и результат. Ошибка *может* содержать ошибку типа *SdkError* или null при успешном совместном окне. В результате может содержаться `AppContentStageSharingState` объект, указывающий на успешное и повторное и повторное, или null, указывающий на неудачное и повторное.|

### <a name="example"></a>Пример

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

Тело ответа JSON для `getAppContentStageSharingCapabilities` API:

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приводится коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **1000** | У приложения нет разрешений на доступ к совместному доступу к этапу.|

## <a name="get-real-time-teams-meeting-events-api"></a>Получите API Teams собраний в режиме реального времени

Пользователь может получать события собраний в режиме реального времени. Как только любое приложение связано с собранием, фактическое время начала и окончания собрания передается боту. Фактическое время начала и окончания собрания отличается от запланированного времени начала и окончания. API сведений о собраниях предоставляет запланированное время начала и окончания. Событие предоставляет фактическое время начала и окончания.

### <a name="prerequisite"></a>Предварительное условие

Манифест приложения должен иметь свойство для `webApplicationInfo` получения событий начала и окончания собрания. Чтобы настроить манифест, используйте следующие примеры:

<br>

<details>

<summary><b>Для версии манифеста приложения 1.12</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]    
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>Для манифеста приложения версии 1.11 или более ранней версии</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

<br>

</details>

### <a name="example-of-getting-meetingstartendeventvalue"></a>Пример получения `MeetingStartEndEventvalue`

Бот получает событие через обработник `OnEventActivityAsync` . Чтобы deserialize полезной нагрузки JSON, для получения метаданных собрания вводится объект модели. Метаданные собрания в свойстве `value` в полезной нагрузке события. Создается `MeetingStartEndEventvalue` объект модели, переменные члена которого соответствуют клавишам, которые находятся под `value` свойством в полезной нагрузке события.

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

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Разнонасть собраний | Microsoft Teams для прохождения маркеров. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Бот-бот для пузырьков контента для собраний | Microsoft Teams для взаимодействия с ботом пузырьков контента на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Собрание MeetingSidePanel | Microsoft Teams для взаимодействия с боковой панелью на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Вкладка "Сведения в собрании" | Microsoft Teams для взаимодействия с вкладками Details in-meeting. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|Пример событий собраний|Пример приложения для демонстрации событий Teams собраний в режиме реального времени|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|Пример набора собраний|Пример приложения для демонстрации опыта собраний для сценария набора персонала.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|Установка приложения с помощью кода QR|Пример приложения, которое создает код QR и устанавливает приложение с помощью кода QR|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>Дополнительные ресурсы

* [Teams потока проверки подлинности для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Приложения для собраний Teams](teams-apps-in-meetings.md)

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Включить и настроить приложения для Teams собраний](enable-and-configure-your-app-for-teams-meetings.md)
