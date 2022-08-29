---
title: Справочные материалы по API приложений для собраний
author: surbhigupta
description: В этой статье вы узнаете о справочниках по API приложений для собраний, доступных для клиентских приложений Teams и пакета SDK Bot Framework, с примерами кода и кодами ответов.
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 8277e0fb947ac109f3482c31613c01fd924fa139
ms.sourcegitcommit: d5628e0d50c3f471abd91c3a3c2f99783b087502
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2022
ms.locfileid: "67435015"
---
# <a name="meeting-apps-api-references"></a>Справочные материалы по API приложений для собраний

Расширяемость собраний предоставляет API-интерфейсы для улучшения взаимодействия с собранием. С помощью перечисленных API можно выполнить следующее:

* Создавать приложения или интегрировать существующие приложения в жизненные циклы собраний.
* Использовать API для информирования вашего приложения о собрании.
* Выбрать необходимые API для улучшения работы с собраниями.

> [!NOTE]
> Используйте [пакет SDK для JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) для Teams (*версия*: 1.10 и более поздние), для работы единого входа на боковой панели собрания.

В следующей таблице представлен список API-интерфейсов, доступных в пакетах SDK для клиента Microsoft Teams (MSTC) и Microsoft Bot Framework (MSBF).

|Метод| Описание| Источник|
|---|---|----|
|[**Получить пользовательский контекст**](#get-user-context-api)| Получение контекстных сведений для отображения соответствующего содержимого на вкладке Microsoft Teams.| [MSTC SDK](/microsoftteams/platform/tabs/how-to/access-teams-context#get-context-by-using-the-microsoft-teams-javascript-library) |
|[**Получение участника**](#get-participant-api)| Получить информацию об участнике по идентификатору собрания и идентификатору участника. | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetingparticipantasync?view=botbuilder-dotnet-stable&preserve-view=true)
|[**Отправить уведомление о собрании**](#send-an-in-meeting-notification)| Предоставление сигналов собрания с помощью существующего API уведомлений о беседе для чата пользователя с ботом позволяет уведомлять пользователя о действиях, отображая уведомление в собрании. | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityextensions.teamsnotifyuser?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Получить сведения о собрании**](#get-meeting-details-api)| Получите статические метаданные собрания. | [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsinfo.getmeetinginfoasync?view=botbuilder-dotnet-stable&preserve-view=true) |
|[**Отправляйте субтитры в реальном времени**](#send-real-time-captions-api)| Отправка субтитров к текущему собранию в режиме реального времени. | [MSTC SDK](/azure/cognitive-services/speech-service/speech-sdk?tabs=nodejs%2Cubuntu%2Cios-xcode%2Cmac-xcode%2Candroid-studio#get-the-speech-sdk&preserve-view=true) |
|[**Делитесь содержимым приложения на сцене**](#share-app-content-to-stage-api)| Поделитесь определенными частями приложения на сцене собрания с боковой панели приложения в собрании. | [MSTC SDK](/javascript/api/@microsoft/teams-js/meeting) |
|[**Получить состояние обмена сцены содержимого приложения**](#get-app-content-stage-sharing-state-api)| Получить информацию о состоянии общего доступа к приложению на сцене собрания. | [MSTC SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**Получить возможности обмена сцены содержимого приложения**](#get-app-content-stage-sharing-capabilities-api)| Получите возможности приложения для совместного использования на сцене собрания. | [MSTC SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |
|[**Получать события собраний Teams в режиме реального времени**](#get-real-time-teams-meeting-events-api)|Узнавать о событиях собраний в режиме реального времени, таких как фактическое время начала и окончания.| [MSBF SDK](/dotnet/api/microsoft.bot.builder.teams.teamsactivityhandler.onteamsmeetingstartasync?view=botbuilder-dotnet-stable&preserve-view=true) |
| [**Получение входящего звукового состояния**](#get-incoming-audio-state) | Позволяет приложению получить параметр состояния входящего звука для пользователя собрания.| [MSTC SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |
| [**Переключение входящего звука**](#toggle-incoming-audio) | Позволяет приложению переключать параметры состояния входящего звука для пользователя собрания от отключения звука до включения или наоборот.| [MSTC SDK](/javascript/api/@microsoft/teams-js/microsoftteams.meeting?view=msteams-client-js-latest&preserve-view=true) |

## <a name="get-user-context-api"></a>Получить API пользовательского контекста

Как определить и получить контекстную информацию для содержимого вкладки, можно узнать в разделе[Получение контекста вкладки Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library). `meetingId` используется вкладкой, работающей в контексте собрания, и добавляется для полезных данных ответа.

## <a name="get-participant-api"></a>Получить API участника

API `GetParticipant` должен иметь регистрацию бота и идентификатор для создания токенов авторизации Подробнее в разделе [Регистрация и идентификатор бота.](../build-your-first-app/build-bot.md).

> [!NOTE]
>
> * Не кэшируйте роли участников, так как организатор собрания может изменить роли в любое время.
> * Сейчас API `GetParticipant` поддерживается только для списков рассылки или реестров до 350 участников.

### <a name="query-parameters"></a>Параметры запроса

> [!TIP]
> Получите идентификаторы участников и арендаторов на [вкладке проверки подлинности единого входа](../tabs/how-to/authentication/tab-sso-overview.md).

API `Meeting` должен иметь `meetingId`, `participantId` и `tenantId` в качестве параметров URL-адреса. Параметры доступны как часть пакета SDK клиента Teams и действия бота.

В следующей таблице приведены параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.|
|**participantId**| String | Да | Идентификатор участника — это идентификатор пользователя. Он доступен в Tab SSO, Bot Invoke и Teams Client SDK. Рекомендуется получить идентификатор участника из Tab SSO. |
|**tenantId**| Строка | Да | Идентификатор клиента требуется для пользователей клиентов. Он доступен в Tab SSO, Bot Invoke и Teams Client SDK. Рекомендуется получить идентификатор клиента из Tab SSO. |

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
      "conversationType": "groupChat", 
      "isGroup":true
   }
}
```

---

| Имя свойства | Описание |
|---|---|
| **user.id** | Идентификатор пользователя. |
| **user.aadObjectId** | Идентификатор объекта Azure Active Directory пользователя. |
| **user.name** | Имя пользователя. |
| **user.givenName** | Имя пользователя.|
| **user.surname** | Фамилия пользователя. |
| **user.email** | Идентификатор почты пользователя. |
| **user.userPrincipalName** | Имя участника-пользователя. |
| **User.tenantId** | Идентификатор клиента Azure Active Directory. |
| **user.userRole** | Роль пользователя. Например, admin или user. |
| **meeting.role** | Роль участника в собрании. Например, "Организатор", "Выступающий" или "Участник". |
| **meeting.inMeeting** | Значение, указывающее, находится ли участник в собрании. |
| **conversation.id** | Идентификатор чата собрания. |
| **conversation.isGroup** | Логическое значение, указывающее, содержит ли беседа более двух участников. |

### <a name="response-codes"></a>Коды ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **403** | Полученные сведения об участниках не передаются приложению. Если приложение не установлено в собрании, оно вызывает ошибочный отклик 403. Если администратор клиента отключает или блокирует приложение во время динамической миграции сайта, это вызывает ошибочный отклик 403. |
| **200** | Сведения об участнике успешно извлечены.|
| **401** | Приложение отвечает недопустимым токеном|
| **404** | Истек срок действия собрания или участники недоступны.|

## <a name="send-an-in-meeting-notification"></a>Отправить уведомление о собрании

Все пользователи на собрании получают уведомления, отправленные с помощью полезных данных уведомлений на собрании. Полезные данные уведомлений на собрании запускают уведомление на собрании и позволяют вам предоставлять сигналы собрания, которые доставляются с использованием существующего API-интерфейса уведомления о разговоре для чата пользователя с ботом. Вы можете отправить уведомление на собрании на основе действий пользователя. Эти полезные данные доступны через службы ботов.

> [!NOTE]
>
> * Когда вызывается уведомление о собрании, содержимое представляется в виде сообщения чата.
> * Сейчас отправка целевых уведомлений и поддержка веб-приложений не поддерживаются.
> * Вы должны вызвать функцию [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) для автоматического закрытия после того, как пользователь выполнит действие в веб-представлении. Это требование для отправки приложения. Подробнее в статье [Модуль задач Teams SDK](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
> * Если вы хотите, чтобы ваше приложение поддерживало анонимных пользователей, полезная нагрузка начального запроса на вызов должна полагаться на `from.id` метаданные запроса`from` в объекте, а не на `from.aadObjectId` метаданные запроса. `from.id` — это идентификатор пользователя, а `from.aadObjectId` — идентификатор Microsoft Azure Active Directory (Azure AD) пользователя. Подробнее в разделе[использование модулей задач на вкладках и создание ](../task-modules-and-cards/task-modules/task-modules-tabs.md) и [ отправка модуля задач.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| Строка | Да | Идентификатор беседы доступен как часть вызова бота. |

### <a name="examples"></a>Примеры

`Bot ID` объявляется в манифесте, и бот получает объект результата.

> [!NOTE]
>
> * Параметр `completionBotId` `externalResourceUrl` является необязательным в запрашиваемом примере полезных данных
> * Параметры ширины и высоты `externalResourceUrl` должны быть в пикселях. Подробнее в [правилах разработки вкладок](design/designing-apps-in-meetings.md).
> * URL-адрес — это страница, которая загружается как `<iframe>` в уведомлении о собрании. Домен должен быть в массиве приложений `validDomains` в манифесте приложения.

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
```

```json

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&<completionBotId>=<BOT_APP_ID>"
        }
    },
    "replyToId": "1493070356924"
}
```

---

| Имя свойства | Описание |
|---|---|
| **type** | Тип действия. |
| **text** | Текстовое содержимое сообщения. |
| **summary** | Сводный текст сообщения. |
| **channelData.notification.alertInMeeting** | Логическое значение, указывающее, должно ли уведомление отображаться пользователю во время собрания. |
| **channelData.notification.externalResourceUrl** | Значение URL-адреса внешнего ресурса уведомления.|
| **replyToId** | Идентификатор родительского или корневого сообщения потока. |
| **APP_ID** | Идентификатор приложения, объявленный в манифесте. |
| **completionBotId** | Идентификатор приложения бота |

### <a name="response-codes"></a>Коды ответа

В следующей таблице содержатся коды ответов:

|Код ответа|Описание|
|---|---|
| **201** | Действие с сигналом успешно отправлено. |
| **401** | Приложение отвечает недопустимым токеном |
| **403** | Приложению не удалось отправить сигнал. Код отклика 403 может возникать по разным причинам, например, когда администратор клиента отключает и аварийно завершает работу приложения во время динамической миграции сайта. В этом случае полезные данные содержат подробное сообщение об ошибке. |
| **404** | Чат собрания не существует. |

## <a name="get-meeting-details-api"></a>Получить API сведений о собрании

API сведений о собрании позволяет вашему приложению получать статические метаданные собрания. Метаданные предоставляют точки данных, которые не изменяются динамически. API доступен через службы ботов. Сейчас как частные запланированные или повторяющиеся собрания, так и запланированные или повторяющиеся собрания канала поддерживают API с различными разрешениями RSC соответственно.

API `Meeting Details` должен иметь регистрацию бота и идентификатор бота. Для получения `TurnContext` требуется bot SDK. Чтобы использовать API сведений о собрании, вы должны получить различные разрешения RSC в зависимости от области собрания, например закрытого собрания или собрания канала.

### <a name="prerequisite"></a>Предварительное условие

Чтобы использовать API сведений о собрании, вы должны получить различные разрешения RSC в зависимости от области собрания, например закрытого собрания или собрания канала.

<br>

<details>

<summary><b>Для манифеста приложения версии 1.12 и более поздних</b></summary>

Используйте следующий пример, чтобы настроить манифест `webApplicationInfo` и `authorization` свойства вашего приложения для любого индивидуального собрания:

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

Используйте следующий пример, чтобы настроить манифест `webApplicationInfo` и `authorization` свойства вашего приложения для любого собрания канала:

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

<summary><b>Для манифеста приложения версии 1.11 и более ранних</b></summary>

Используйте следующий пример, чтобы настроить свойство `webApplicationInfo` манифеста приложения для любого индивидуального собрания:

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

Используйте следующий пример для настройки свойства `webApplicationInfo` манифеста приложения для любого собрания канала:

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
>
> * Бот может автоматически получать события начала или окончания собрания из всех собраний, созданных во всех каналах, путем добавления `ChannelMeeting.ReadBasic.Group` в манифест для разрешения RSC.
>
> * Для звонков "один к одному `organizer` `organizer` " инициатор чата, а для групповых звонков — инициатор звонков.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице перечислены параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| String | Да | Идентификатор собрания доступен через Bot Invoke и Teams Client SDK. |

### <a name="example"></a>Пример

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

Not available

```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

Текст отклика JSON для API сведений о собрании выглядит следующим образом:

* **Запланированные собрания:**

    ```json

    {
       "details":  { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "Scheduled" 
         },
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
             }, 
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    } 
    ```

* **Вызовы "один к одному":**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "OneToOneCall"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer  ": {
             "id": "<organizer user ID>",
             "aadObjectId": "<AAD object ID>",
             "objectId": "<organizer object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Групповые вызовы:**

    ```json
    {
        "details": {
             "id": "<meeting ID>",
             "type": "GroupCall",
             "joinUrl": "https://teams.microsoft.com/l/xx"
         },
        "conversation": {
             "isGroup": true,
             "conversationType": "groupChat",
             "id": "meeting chat ID"
         },
        "organizer": {
             "id": "<organizer user ID>",
             "objectId": "<organizer object ID>",
             "aadObjectId": "<AAD object ID>",
             "tenantId": "<Tenant ID>" 
         }
    }
    
    ```

* **Мгновенные собрания:**

    ```json
    { 
       "details": { 
             "id": "<meeting ID>", 
             "msGraphResourceId": "MSowYmQ0M2I4OS1lN2QxLTQxNzAtOGZhYi00OWJjYjkwOTk1YWYqMCoqMTk6bWVldGluZ19OVEkyT0RjM01qUXROV1UyW", 
             "scheduledStartTime": "2022-04-24T22:00:00Z", 
             "scheduledEndTime": "2022-04-24T23:00:00Z", 
             "joinUrl": "https://teams.microsoft.com/l/xx", 
             "title": "All Hands", 
             "type": "MeetNow" 
         }, 
        "conversation": { 
             "isGroup": true, 
             "conversationType": "groupChat", 
             "id": "meeting chat ID" 
         },
        "organizer": { 
             "id": "<organizer user ID>", 
             "aadObjectId": "<AAD object ID>", 
             "tenantId": "<Tenant ID>" ,
             "objectId": "<organizer object ID>"
         }
    }
    
    ```

---

| Имя свойства | Описание |
|---|---|
| **details.id** | Идентификатор собрания, закодированный в виде строки BASE64. |
| **details.msGraphResourceId** | MsGraphResourceId, используемый специально для вызовов MS API Graph. |
| **details.scheduledStartTime** | Запланированное время начала собрания в формате UTC. |
| **details.scheduledEndTime** | Запланированное время окончания собрания в формате UTC. |
| **details.joinUrl** | URL-адрес, используемый для присоединения к собранию. |
| **details.title** | Название собрания. |
| **details.type** | Тип собрания (GroupCall, OneToOneCall, Adhoc, Broadcast, MeetNow, Recurring, Scheduled или Unknown). |
| **conversation.isGroup** | Логическое значение, указывающее, содержит ли беседа более двух участников. |
| **conversation.conversationType** | Тип беседы. |
| **conversation.id** | Идентификатор чата собрания. |
| **organizer.id** | Идентификатор пользователя организатора. |
| **organizer.aadObjectId** | Идентификатор объекта Azure Active Directory организатора. |
| **organizer.tenantId** | Идентификатор клиента Azure Active Directory организатора. |

При типе повторяющегося собрания

**startDate**: указывает дату начала применения шаблона. Значение startDate должно соответствовать значению даты свойства start ресурса события. Обратите внимание, что первое событие собрания может не произойти в эту дату, если оно не соответствует шаблону.

**endDate**: указывает дату остановки применения шаблона. Обратите внимание, что последнее событие собрания может не произойти в эту дату, если оно не соответствует шаблону.

## <a name="send-real-time-captions-api"></a>API отправки субтитров в режиме реального времени

API отправки субтитров в режиме реального времени предоставляет конечную точку POST для доступа к обмену данными Teams в режиме реального времени (CART) с закрытыми субтитрами, типизированными человеком. Текстовое содержимое, отправляемое в эту конечную точку, отображается конечным пользователям на собрании Teams, если у них включены субтитры.

### <a name="cart-url"></a>URL-адрес CART

URL-адрес CART для конечной точки POST можно получить на странице  параметров собрания в собрании Teams. Подробнее в разделе [Субтитры CART на собрании Microsoft Teams](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47). Вам не нужно изменять URL-адрес CART, чтобы использовать субтитры CART.

#### <a name="query-parameter"></a>Параметр запроса

URL-адрес CART включает следующие параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|----|
|**meetingId**| String | Да |Идентификатор собрания доступен через Bot Invoke и Teams Client SDK. <br/>Например, meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**токен**| String | Да |Токен авторизации<br/> Например, token=04751eac |

#### <a name="example"></a>Пример

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>Метод

|Ресурс|Метод|Описание|
|----|----|----|
|/cartcaption|POST|Обработка субтитров для собрания, которое было начато|

> [!NOTE]
> Убедитесь, что тип содержимого для всех запросов — обычный текст в кодировке UTF-8. Текст запроса содержит только субтитры.

#### <a name="example"></a>Пример

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> Каждый запрос POST создает новую строку субтитров. Чтобы у конечного пользователя было достаточно времени для чтения содержимого, ограничьте текст каждого POST-запроса до 80–120 символов.

### <a name="error-codes"></a>Коды ошибок

В следующей таблице приведены коды ошибок:

|Код ошибки|Описание|
|---|---|
| **400** | Неправильный запрос. В тексте отклика есть дополнительные сведения. Например, представлены не все необходимые параметры.|
| **401** | Недостаточно полномочий. Неверный или просроченный токен. Если вы получаете эту ошибку, создайте новый URL-адрес CART в Teams. |
| **404** | Собрание не найдено или не началось. Если вы получили эту ошибку, убедитесь, что вы начали собрание и выберите начальные субтитры. После включения субтитров на собрании вы можете начать публиковать субтитры на собрании.|
| **500** |Внутренняя ошибка сервера. Для получения дополнительной информации [обратитесь в службу поддержки или оставьте отзыв](../feedback.md).|

## <a name="share-app-content-to-stage-api"></a>Поделитесь содержимым приложения на сцене API

API `shareAppContentToStage` позволяет вам делиться определенными частями вашего приложения на сцене собрания. API доступен через клиентский SDK Teams.

### <a name="prerequisite"></a>Предварительное условие

* Чтобы использовать API `shareAppContentToStage`, необходимо получить разрешения RSC. В манифесте приложения настройте свойство `authorization` и `name` и `type` в поле `resourceSpecific`. Например:

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

* `appContentUrl` должен быть разрешен массивом `validDomains` внутри manifest.json, иначе API возвратит 501.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице приведены параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра, ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, либо значение null при успешном совместном использовании. *Результат* может содержать либо истинное значение в случае успешного общего доступа, либо значение NULL в случае сбоя совместного использования.|
|**appContentURL**| String | Да | URL-адрес, который будет опубликован на сцене.|

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

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет необходимых разрешений, чтобы разрешить общий доступ к этапу.|

## <a name="get-app-content-stage-sharing-state-api"></a>Получить состояние обмена сцены содержимого приложения API

API `getAppContentStageSharingState`позволяет получать информацию о совместном использовании приложений на сцене собрания.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра, ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, в случае ошибки, либо значение null при успешном совместном использовании.  *Результат* может либо содержать `AppContentStageSharingState` объект, указывающий на успешный поиск, либо значение null, указывающее на неудачный поиск.|

### <a name="example"></a>Пример

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

Текст отклика JSON для `getAppContentStageSharingState` API:

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет необходимых разрешений, чтобы разрешить общий доступ к этапу.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>Получить возможности обмена сцены содержимого приложения API

API `getAppContentStageSharingCapabilities` позволяет получить возможности приложения для совместного использования на сцене собрания.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра, ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, либо значение null при успешном совместном использовании. Результат может либо содержать объект `AppContentStageSharingState`, указывающий на успешный поиск, значение null, указывающее на неудачный поиск.|

### <a name="example"></a>Пример

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

Текст отклика JSON для `getAppContentStageSharingCapabilities` API:

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **1000** | У приложения нет разрешений на предоставление общего доступа к этапу.|

## <a name="get-real-time-teams-meeting-events-api"></a>Получите API событий собраний Teams в реальном времени

> [!NOTE]
> События собраний Teams в режиме реального времени поддерживаются только для запланированных собраний.

Пользователь может получать информацию о собраниях в режиме реального времени. Как только приложение связывается с собранием, фактическое время начала и окончания собрания передается боту. Фактическое время начала и окончания собрания отличается от запланированного времени начала и окончания. API сведений о собрании предоставляет запланированное время начала и окончания. Событие предоставляет фактическое время начала и окончания.

Вы должны быть знакомы с объектом`TurnContext`, доступным через Bot SDK. Объект `Activity` в `TurnContext` содержит полезные данные с фактическим временем начала и окончания. Для проведения собраний в реальном времени требуется зарегистрированный идентификатор бота на платформе Teams. Бот может автоматически получать событие начала или окончания собрания, добавляя `ChannelMeeting.ReadBasic.Group` в манифест.

### <a name="prerequisite"></a>Предварительное условие

Манифест вашего приложения должен иметь свойство `webApplicationInfo` для получения событий начала и окончания собрания. Используйте следующие примеры для настройки манифеста:

<br>

<details>

<summary><b>Для манифеста приложения версии 1.12 и более поздних</b></summary>

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

<summary><b>Для манифеста приложения версии 1.11 и более ранних</b></summary>

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

Бот получает событие через обработчик `OnEventActivityAsync`. Чтобы десериализовать полезные данные JSON вводится объект модели для получения метаданных для собрания. Метаданные собрания в свойстве `value` в полезных данных события. Создается объект модели `MeetingStartEndEventvalue`, переменные элементы которого соответствуют ключам в свойстве `value` в полезных данных события.

> [!NOTE]
>
> * Получить идентификатор собрания от `turnContext.ChannelData`.
> * Не используйте идентификатор беседы в качестве идентификатора собрания.
> * Не используйте идентификатор собрания из полезных данных событий `turncontext.activity.value`.

В следующем коде показано, как захватить метаданные собрания `MeetingType`, `Title`, `Id`, `JoinUrl`, `StartTime` и `EndTime` из события начала и окончания собрания:

Событие начала собрания

```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingStartEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

Событие окончания собрания

```csharp
protected override async Task OnTeamsMeetingEndAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

### <a name="example-of-meeting-start-event-payload"></a>Пример полезных данных события начала собрания

В следующем коде приводится пример полезных данных события начала собрания:

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

### <a name="example-of-meeting-end-event-payload"></a>Пример полезных данных события окончания собрания

В следующем коде приводится пример полезных данных события окончания собрания:

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

| Имя свойства | Описание |
|---|---|
| **name** | Имя пользователя.|
| **type** | Тип действия. |
| **timestamp** | Локальная дата и время сообщения, выраженные в формате ISO-8601. |
| **id** | Идентификатор действия. |
| **channelId** | Канал, с помощью который связано это действие. |
| **serviceUrl** | URL-адрес службы, куда должны отправляться ответы на это действие. |
| **from.id** | Идентификатор пользователя, отправившего запрос. |
| **from.aadObjectId** | Идентификатор объекта Azure Active Directory пользователя, отправившего запрос. |
| **conversation.isGroup** | Логическое значение, указывающее, содержит ли беседа более двух участников. |
| **conversation.tenantId** | Идентификатор клиента Azure Active Directory для беседы или собрания. |
| **conversation.id** | Идентификатор чата собрания. |
| **recipient.id** | Идентификатор пользователя, который получает запрос. |
| **recipient.name** | Имя пользователя, который получает запрос. |
| **entities.locale** | сущность, содержащая метаданные о языковом стандарте. |
| **entities.country** | Объект , содержащий метаданные о стране. |
| **entities.type** | сущность, содержащая метаданные о клиенте. |
| **channelData.tenant.id** | Идентификатор клиента Azure Active Directory. |
| **channelData.source** | Имя источника, из которого инициируется или вызывается событие. |
| **channelData.meeting.id** | Идентификатор по умолчанию, связанный с собранием. |
| **Значение. MeetingType** | Тип собрания. |
| **Значение. Название** | Тема собрания. |
| **Значение. Id** | Идентификатор по умолчанию, связанный с собранием. |
| **Значение. JoinUrl** | URL-адрес присоединения к собранию. |
| **Значение. Starttime** | Время начала собрания в формате UTC. |
| **Значение. Время окончания** | Время окончания собрания в формате UTC. |
| **locale**| Языковой стандарт сообщения, задаемого клиентом. |

## <a name="get-incoming-audio-state"></a>Получение входящего звукового состояния

API `getIncomingClientAudioState` позволяет приложению получить параметр состояния входящего звука для пользователя собрания. API доступен через клиентский SDK Teams.

> [!NOTE]
>
> * API `getIncomingClientAudioState` для мобильных устройств в настоящее время доступен в [общедоступной предварительной версии для разработчиков](../resources/dev-preview/developer-preview-intro.md).
> * Согласие для конкретного ресурса доступно для манифеста версии 1.12 и более поздних версий, поэтому этот API не работает для манифеста версии 1.11 и более ранних версий.

### <a name="manifest"></a>Манифест

```JSON
"authorization": {
    "permissions": {
      "resourceSpecific": [
        {
          "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
          "type": "Delegated"
        }
      ]
    }
  }
```
  
### <a name="example"></a>Пример

```javascript
callback = (errcode, result) => {
        if (errcode) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }

microsoftTeams.meeting.getIncomingClientAudioState(this.callback)
```
### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра `error` и `result`. Ошибка *может* содержать тип ошибки или `SdkError` `null` при успешной выборке звука. Результат *может* содержать значение true или false, если выборка звука выполнена успешно, или значение NULL при сбое выборки звука. Входящий звук отключен, если результат имеет значение true, и не включен, если результат имеет значение false. |
  
### <a name="response-codes"></a>Коды ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет необходимых разрешений, чтобы разрешить общий доступ к этапу.|

## <a name="toggle-incoming-audio"></a>Переключение входящего звука

API `toggleIncomingClientAudio` позволяет приложению переключать параметры состояния входящего звука для пользователя собрания от отключения звука до включения или наоборот. API доступен через клиентский SDK Teams.

> [!NOTE]
>
> * API `toggleIncomingClientAudio` для мобильных устройств в настоящее время доступен в [общедоступной предварительной версии для разработчиков](../resources/dev-preview/developer-preview-intro.md).
> * Согласие для конкретного ресурса доступно для манифеста версии 1.12 и более поздних версий, поэтому этот API не работает для манифеста версии 1.11 и более ранних версий.

### <a name="manifest"></a>Манифест

```JSON
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeetingParticipant.ToggleIncomingAudio.Chat",
                "type": "Delegated"
            }
        ]
    }
}
```
 
### <a name="example"></a>Пример

```javascript
callback = (error, result) => {
        if (error) {
            // Handle error code
        }
        else {
            // Handle success code
        }
    }

microsoftTeams.meeting.toggleIncomingClientAudio(this.callback)
```
  
### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра `error` и `result`. Ошибка *может* содержать тип ошибки или `SdkError` `null` при успешном выполнении переключателя. Результат *может* содержать значение true или false, если переключатель выполнен успешно, или значение NULL при сбое переключателя. Входящий звук отключен, если результат имеет значение true, и не включен, если результат имеет значение false.
  
### <a name="response-code"></a>Код ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет необходимых разрешений, чтобы разрешить общий доступ к этапу.|

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| Расширяемость собраний | Пример расширяемости собраний Teams для передачи маркеров. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Бот пузырькового содержимого собрания | Пример расширяемости собраний Teams для взаимодействия с ботом пузырьков содержимого на собрании. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Собрание meetingSidePanel | Пример расширяемости собраний Teams для взаимодействия с боковой панелью в собрании. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| Вкладка "Сведения" в собрании | Пример расширяемости собраний Teams для взаимодействия с вкладкой "Сведения" в собрании. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|Пример событий собрания|Пример приложения для отображения событий собраний Teams в реальном времени|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|Образец собрания для набора сотрудников|Пример приложения для демонстрации опыта собраний для сценария набора сотрудников.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|Установка приложения с помощью QR-кода|Пример приложения, которое создает QR-код и устанавливает приложение с помощью QR-кода|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>Дополнительные ресурсы

* [Проверка подлинности Microsoft Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Приложения для собраний Teams](teams-apps-in-meetings.md)
* [Пакет SDK Live Share](teams-live-share-overview.md)

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Включите и настройте свои приложения для собраний Teams](enable-and-configure-your-app-for-teams-meetings.md)
