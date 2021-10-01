---
title: Необходимые условия для приложений в собраниях Teams
author: surbhigupta
description: Определение необходимых условий с приложениями для Teams собраний
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams apps meetings user participant role api
ms.openlocfilehash: 56219323f6106619a9dd4f1b26289ecf86d297f3
ms.sourcegitcommit: 329447310013a2672216793dab79145b24ef2cd2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2021
ms.locfileid: "60017319"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Необходимые условия для приложений в собраниях Teams

Приложения для Teams собраний могут расширить возможности своих приложений на протяжении всего жизненного цикла собраний. Прежде чем работать с приложениями для Teams собраний, необходимо выполнить следующие требования:

* Знать, как разрабатывать Teams приложения. Дополнительные сведения о разработке приложения Teams см. в Teams [разработки приложения.](../overview.md)

* Обновим манифест Teams, чтобы указать, что приложение доступно для собраний. Дополнительные сведения см. в [манифесте приложения.](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)

* Используйте приложение, которое поддерживает настраиваемые вкладки в области группового чата. Дополнительные сведения см. в [области группового чата](../resources/schema/manifest-schema.md#configurabletabs) и [создании вкладки группы.](../build-your-first-app/build-channel-tab.md)

* Придерживайтеся общих Teams правил разработки вкладок для сценариев до и после собрания. Для работы во время собраний обратитесь к вкладке на собрании и рекомендациям по проектированию диалогов на собрании. Дополнительные сведения см. [Teams](../tabs/design/tabs.md)руководства по разработке вкладок, [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)рекомендации по проектированию вкладок на собрании и рекомендации по проектированию диалогов на [собрании.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Поддержка области, чтобы включить приложение в чаты перед собранием и `groupchat` после собрания. С помощью предварительного собрания приложения можно найти и добавить приложения для собраний и выполнять задачи перед собранием. С помощью приложения после собрания можно просмотреть результаты собрания, такие как результаты опроса или плата
* Параметры URL-адресов API должны иметь `meetingId` и `userId` `tenantId` . Параметры доступны в рамках Teams клиентской SDK и бот-активности. Кроме того, вы можете получить достоверную информацию для идентификации пользователя и идентификации клиента с помощью вкладки [SSO проверки подлинности.](../tabs/how-to/authentication/auth-aad-sso.md)

* API `GetParticipant` должен иметь регистрацию бота и ID для создания маркеров auth. Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)

* Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании. Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания. Параметр завершения в диалоговом окне на собрании `bot Id` см. в `NotificationSignal` API.

* API `Meeting Details` должен иметь регистрацию бота и бот-ИД. Для этого требуется бот SDK для получения `TurnContext` .

* Для событий собраний в режиме реального времени необходимо ознакомиться с объектом, доступным `TurnContext` через SDK Bot. Объект `Activity` содержит `TurnContext` полезной нагрузки с фактическим временем начала и окончания. Для проведения собраний в режиме реального времени требуется зарегистрированный бот-ИД с Teams платформы.

После того как вы прошли необходимые условия, вы можете использовать ссылки API приложений собраний , и это позволит вам получить доступ к информации с помощью атрибутов и отображения `GetUserContext` `GetParticipant` `NotificationSignal` `Meeting Details` соответствующего контента.

## <a name="meeting-apps-api-references"></a>Справочные материалы по API приложений для собраний

Следующие дополнительные возможности собраний предоставляют API для преобразования опыта собраний:

* Создание приложений или интеграция существующих приложений в течение жизненного цикла собраний.
* Используйте API, чтобы сделать ваше приложение осведомленным о собрании.
* Выберите API, которые необходимо использовать для повышения качества работы собраний.

В следующей таблице приводится список этих API:

|API|Description|Запрос|Источник|
|---|---|----|---|
|**GetUserContext**| Этот API позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams. |_**microsoftTeams.getContext() => { /*...* / } )**_|Microsoft Teams Клиентская SDK|
|**GetParticipant**| Этот API позволяет боту получать сведения о участниках, встречая ID и ID участника. |**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота. Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|
|**Сведения о собрании** | Этот API позволяет получать статические метаданные собраний. |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |

В следующей таблице ниже приводится метод bot Framework SDK для API:

|API|Метод Bot Framework SDK|
|---|---|
|**GetParticipant**| `GetMeetingParticipantAsync (Microsoft.Bot.Builder.ITurnContext turnContext, string meetingId = default, string participantId = default, string tenantId = default, System.Threading.CancellationToken cancellationToken = default);` |
|**NotificationSignal** | `activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<title>&completionBotId=BOT_APP_ID");` |
|**Сведения о собрании** | `TeamsMeetingInfo (string id = default);` |

### <a name="getusercontext-api"></a>GetUserContext API

Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в этой Teams [контексте.](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library) `meetingId`используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * Не кэшить роли участников, так как организатор собрания может изменить роли в любое время.
> * Teams в настоящее время не поддерживает большие списки рассылки или размеры реестра более 350 участников `GetParticipant` для API.

API позволяет боту получать сведения о `GetParticipant` участниках, встречая ID и ID участника. API включает параметры запросов, примеры и коды ответа. API поддерживается как в закрытых запланированных, так и повторяющихся собраниях, а также в запланированных или повторяющихся собраниях канала. 

#### <a name="query-parameters"></a>Параметры запроса

API `GetParticipant` включает следующие параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK.|
|**participantId**| String | Да | ID участника — это пользовательский ИД. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID участника из SSO tab. |
|**tenantId**| Строка | Да | Для пользователей-клиентов требуется ID клиента. Он доступен в вкладке SSO, Bot Invoke и Teams клиентской SDK. Рекомендуется получить ID клиента из SSO tab. |

#### <a name="example"></a>Пример

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

#### <a name="response-codes"></a>Коды ответа

API `GetParticipant` возвращает следующие коды ответа:

|Код ответа|Description|
|---|---|
| **403** | Сведения о участниках не делятся с приложением. Если приложение не установлено на собрании, оно вызывает наиболее распространенный ответ на ошибку 403. Если администратор клиента отключает или блокирует приложение во время переноса веб-сайта в прямом эфире, запускается ответ на ошибку 403. |
| **200** | Данные участника успешно извлекаются.|
| **401** | Приложение отвечает недействительным маркером.|
| **404** | Срок собрания истек или участник не может быть найден.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.

> [!NOTE]
> * При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.
> * В настоящее время отправка целевых уведомлений не поддерживается.

API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе `NotificationSignal` для чата пользователя-бота. Этот API позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно в собрании. API включает параметр запроса, примеры и коды ответа.

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

#### <a name="response-codes"></a>Коды ответа

API `NotificationSignal` включает в себя следующие коды ответа:

|Код ответа|Description|
|---|---|
| **201** | Успешно отправляется действие с сигналом. |
| **401** | Приложение отвечает недействительным маркером. |
| **403** | Приложение не может отправить сигнал. Код ответа 403 может возникать по различным причинам, например, администратор клиента отключает и блокирует приложение во время переноса веб-сайтов в прямом эфире. В этом случае полезное сообщение содержит подробное сообщение об ошибке. |
| **404** | Чат собраний не существует. |

### <a name="meeting-details-api"></a>API сведений о собраниях

> [!NOTE]
> В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.

API позволяет приложению получать `Meeting Details` статические метаданные собраний. Метаданные предоставляют точки данных, которые не изменяются динамически.
API доступен через службы ботов.

#### <a name="prerequisite"></a>Предварительное условие

Чтобы использовать `Meeting Details` API, необходимо получить разрешения RSC. Чтобы настроить свойство манифеста приложения, используйте следующий `webApplicationInfo` пример:

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

API `Meeting Details` включает в себя следующий параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams клиентской SDK. |

#### <a name="example"></a>Пример

API `Meeting Details` содержит следующие примеры:

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

Ответный орган JSON для `Meeting Details` API:

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

Фактическое время начала и окончания собрания отличается от запланированного времени начала и окончания. API `Meeting Details` предоставляет запланированное время начала и окончания. Событие предоставляет фактическое время начала и окончания.

### <a name="prerequisite"></a>Предварительное условие

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

Ваш бот получает событие через `OnEventActivityAsync` обработник.

Чтобы deserialize полезной нагрузки JSON, для получения метаданных собрания вводится объект модели. Метаданные собрания в свойстве в `value` полезной нагрузке события. Создается объект модели, переменные члена которого соответствуют клавишам, которые находятся под свойством `MeetingStartEndEventvalue` `value` в полезной нагрузке события.
     
> [!NOTE]      
> * Получите ID собрания из `turnContext.ChannelData` .    
> * Не используйте ИД беседы в качестве ИД собрания.     
> * Не используйте ID собрания из полезной нагрузки на события `turncontext.activity.value` собраний. 
      
В следующем коде показано, как захватить метаданные собрания, которое является `MeetingType` , , , , , и из события начала и конца `Title` `Id` `JoinUrl` `StartTime` `EndTime` собрания:

Событие "Начало собрания"

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
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

* Есть `meetingId` `userId` параметры, и в `tenantId` собрании URL-адрес API. Параметры доступны в рамках Teams клиентской SDK и бот-активности. Кроме того, вы можете получить достоверную информацию для идентификации пользователя и идентификации клиента с помощью вкладки [SSO проверки подлинности.](../tabs/how-to/authentication/auth-aad-sso.md)

* Регистрация ботов и ID в API для `GetParticipant` создания маркеров auth. Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)

* Чтобы ваше приложение было в курсе событий на собрании. Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания. В диалоговом окне на собрании проверьте параметр завершения в `bot Id` `NotificationSignal` API.

* Регистрация бота и его ID в `MeetingDetails` API. Для этого требуется бот SDK для получения `TurnContext` .

* Ознакомьтесь с `TurnContext` объектом, доступным с помощью SDK-бота. Объект `Activity` содержит `TurnContext` полезной нагрузки с фактическим временем начала и окончания. Для проведения собраний в режиме реального времени требуется зарегистрированный бот-ИД с Teams платформы.

## <a name="see-also"></a>См. также

* [Рекомендации по проектированию диалогов на собрании](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams потока проверки подлинности для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Приложения для Teams собраний](teams-apps-in-meetings.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Справочные материалы по API приложений для собраний](API-references.md)
