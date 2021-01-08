---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API роли участника собраний в приложениях Teams
ms.openlocfilehash: e768c2dc6722d006c89927adfe60e03243a076d0
ms.sourcegitcommit: f0dfae429385ef02f61896ad49172c4803ef6622
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/31/2020
ms.locfileid: "49740873"
---
# <a name="create-apps-for-teams-meetings"></a>Создание приложений для собраний Teams

## <a name="prerequisites-and-considerations"></a>Предварительные условия и вопросы

1. Приложения на собраниях требуют базовых знаний о [разработке приложений Teams.](../overview.md) Приложение на собрании может состоять [](../bots/what-are-bots.md)из вкладок, [](../tabs/what-are-tabs.md)ботов и функций расширений обмена сообщениями и требует обновления манифеста приложения [Teams,](#update-your-app-manifest) чтобы указать, что приложение доступно для собраний [](../messaging-extensions/what-are-messaging-extensions.md)

1. Чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области [groupchat.](../resources/schema/manifest-schema.md#configurabletabs) *См.* [расширение приложения Teams с помощью настраиваемой вкладки.](../tabs/how-to/add-tab.md) Поддержка области позволяет вашему приложению в чатах до `groupchat` [и](teams-apps-in-meetings.md#pre-meeting-app-experience) [после](teams-apps-in-meetings.md#post-meeting-app-experience) собрания.

1. Для параметров URL-адреса API собраний может потребоваться и tenantId. Они доступны в составе `meetingId` `userId` клиентского SDK Teams и бота. [](/onedrive/find-your-office-365-tenant-id) Кроме того, с помощью проверки подлинности tab SSO можно получить надежные сведения об ИД пользователя и [клиенте.](../tabs/how-to/authentication/auth-aad-sso.md)

1. Некоторые API собраний, например, требуют регистрации бота и ИД `GetParticipant` [приложения-бота](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) для создания маркеров auth.

1. Как разработчик, вы должны соблюдать общие рекомендации по проектированию вкладок [Teams](../tabs/design/tabs.md) для [](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) сценариев до и после собрания, а также рекомендации по диалоговом оклу в собрании, срабатываем во время собрания Teams.

1. Обратите внимание, что чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть в курсе событий собрания. Эти события могут быть в диалоговом окну собрания (см. параметр завершения в) и других поверхностях в течение `bot Id` `Notification Signal API` жизненного цикла собрания.

## <a name="meeting-apps-api-reference"></a>Справочник по API приложений для собраний

|API|Описание|Запрос|Source|
|---|---|----|---|
|**GetUserContext**| Получите контекстную информацию, чтобы отобразить релевантный контент на вкладке Teams. |_**microsoftTeams.getContext( ( ) => { /*...* / } )**_|SDK клиента Microsoft Teams|
|**GetParticipant**|Этот API позволяет боту получать сведения об участниках по их ид.|**GET** _**/v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |Сигналы собрания будут доставляться с помощью следующего существующего API уведомлений о беседе (для чата пользователя-бота). Этот API позволяет разработчикам сигнализировать на основе действия пользователя, чтобы показать диалоговое окно собрания.|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Обратитесь к нашему контексту ["Получить" в документации](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) по вкладке Teams, чтобы получить инструкции по идентификации получения контекстных сведений для содержимого вкладки. В рамках функции "Расстановка собраний" добавлено новое значение для полезной нагрузки ответа:

✔ **meetingId**: используется вкладками при запуске в контексте собрания.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * Не кэшделайте роли участников кэшом, так как организатор собрания может изменить роль в любой момент времени.
>
> * В настоящее время Teams не поддерживает большие списки рассылки или размеры списков для API более чем 350 `GetParticipant` участников.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| string | Да | Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.|
|**participantId**| string | Да | ParticipantId — это ИД пользователя. Он доступен в SSO tab, Bot Invoke и клиентском SDK Teams. Настоятельно рекомендуется получить participantId из SSO tab. |
|**tenantId**| string | Да | Для пользователей клиента требуется tenantId. Он доступен в SSO tab, Bot Invoke и клиентском SDK Teams. Настоятельно рекомендуется получить tenantId из SSO tab. |

#### <a name="example"></a>Пример

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
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
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

Тело ответа:

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

* * *

#### <a name="response-codes"></a>Коды ответа

* **403:** приложению запрещено получать сведения об участниках.  Это наиболее распространенный ответ об ошибке, который вызывается, если приложение не установлено на собрании. Например, если приложение отключено администратором клиента или заблокировано во время прямой миграции сайта.
* **200**: сведения об участниках успешно извлечены.
* **401**: недопустимый маркер.
* **404**: не удается найти участника.
* **500:** срок действия собрания истек (более 60 дней с момента окончания собрания) или у участника нет разрешений на основе их роли.


**Ожидается в ближайшее время**

* **404:** истек срок действия собрания или не удается найти участника.


### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> Когда вызывается диалоговое окно собрания, то же содержимое также будет представлено в качестве сообщения чата.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| string | Да | Идентификатор беседы доступен при вызове бота |

#### <a name="example"></a>Пример

> [!NOTE]
>
Параметр `completionBotId` параметра является `externalResourceUrl` необязательным в запрашиваемом примере полезной нагрузки. `Bot ID` объявляется в манифесте, и бот получает объект результата.
> * Параметры ширины и высоты externalResourceUrl должны быть в пикселях. Чтобы [убедиться,](design/designing-apps-in-meetings.md) что размеры находятся в пределах допустимого, обратитесь к рекомендациям по проектированию.
> * URL-адрес — это страница, загруженная в диалоговом оке `<iframe>` собрания. Домен должен быть в массиве приложения `validDomains` в манифесте приложения.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

* * *

#### <a name="response-codes"></a>Коды ответа

* **201**: успешно отправлена активность с сигналом  
* **401**: недопустимый маркер  
* **201**: успешно отправлено действие с сигналом. 
* **401**: недопустимый маркер.
* **403:** приложению не удается отправить сигнал. Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время миграции на веб-сайт и так далее. В этом случае полезное сообщение содержит подробное сообщение об ошибке. 
* **404:** чат собрания не существует.
 

## <a name="enable-your-app-for-teams-meetings"></a>Включить приложение для собраний Teams

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Возможности приложения для собраний объявляются в манифесте приложения с помощью настраиваемых областейtabs  ->   и **массивов контекста.** *Область* определяет, кому и *где будет* доступно ваше приложение, а также контекст.

> [!NOTE]
> Используйте [схему Developer Preview для](../resources/schema/manifest-schema-dev-preview.md) использования в манифесте приложения.

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a>Свойство Context

Вкладка и свойства работают согласованно, чтобы вы могли определить, где будет отображаться `context` `scopes` ваше приложение. Вкладки в `team` области или области могут иметь несколько `groupchat` контекстов. Возможные значения для свойства контекста:

* **channelTab**: вкладка в заголке канала команды.
* **privateChatTab**: вкладка в заголке группового чата между набором пользователей, не в контексте команды или собрания.
* **meetingChatTab**: вкладка в заголке группового чата между набором пользователей в контексте запланированного собрания.
* **meetingDetailsTab**: вкладка в заголовке представления сведений о собрании календаря.
* **meetingSidePanel**: панель на собрании, открытая через единую панель (u-bar).

> [!NOTE]
> Свойство "Context" в настоящее время не поддерживается и, следовательно, игнорируется на мобильных клиентах

## <a name="configure-your-app-for-meeting-scenarios"></a>Настройка приложения для сценариев собраний

> [!NOTE]
> * Чтобы приложение было видимым в коллекции вкладок, оно должно поддерживать настраиваемые вкладки и область **группового чата.** 
>
> * Мобильные клиенты поддерживают вкладки только на поверхностях до и после собрания. The in-meeting experiences (in-meeting dialog and tab) on mobile will be available soon. Следуйте [указаниям для вкладок на мобильных](../tabs/design/tabs-mobile.md) устройствах при создании вкладок для мобильных устройств.

### <a name="before-a-meeting"></a>Перед собранием

Пользователи с ролями организатора и/или presenter добавляют вкладки к собранию с помощью кнопки плюс ➕ на страницах сведений о **собрании** и чате.  Расширения сообщений добавляются в меню эллипса или переполнения &#x25CF;&#x25CF;&#x25CF; под областью составить сообщение в чате. Боты добавляются в чат собрания с помощью клавиши **@** "" и выбора **get bots.**

✔ удостоверение пользователя *должно* быть подтверждено с помощью [SSO вкладок.](../tabs/how-to/authentication/auth-aad-sso.md) После этой проверки подлинности приложение может получить роль пользователя с помощью API GetParticipant.

 ✔ зависимости от роли пользователя, теперь приложение сможет представлять специальные возможности. Например, приложение для опроса может разрешить создание опроса только организаторам и организаторам.

> **ПРИМЕЧАНИЕ.** Назначения ролей можно изменить во время собрания.  *См.* [роли в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019) 

### <a name="during-a-meeting"></a>Во время собрания

#### <a name="sidepanel"></a>**sidePanel**

✔ в манифесте приложения добавьте **sidePanel** в массив **контекста,** как описано выше.

✔ собрания, как и во всех сценариях, приложение будет отрисовыно на вкладке собрания шириной 320px. Для этого необходимо оптимизировать вкладку. *См.* интерфейс [FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔Соотделите в [SDK Teams,](../tabs/how-to/access-teams-context.md#user-context) чтобы использовать API **userContext** для маршрутов запросов соответствующим образом.

✔ для вкладок обратитесь к [потоку проверки подлинности Teams.](../tabs/how-to/authentication/auth-flow-tab.md) Поток проверки подлинности для вкладок очень похож на поток проверки подлинности для веб-сайтов. Таким образом, вкладки могут использовать OAuth 2.0 напрямую. *См. также,* платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

✔ сообщение должно работать ожидаемым, когда пользователь находится в представлении собрания и должен иметь возможность опубликовать карточки расширения сообщения.

✔ AppName in-meeting — в выдавке tooltip должно быть занося имя приложения в панели U-bar собрания.

#### <a name="in-meeting-dialog"></a>**Диалоговое окно собрания**

✔ Вы должны соблюдать рекомендации по проектированию [диалогового окна собрания.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

✔ для вкладок обратитесь к [потоку проверки подлинности Teams.](../tabs/how-to/authentication/auth-flow-tab.md)

✔ использовать API [](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) уведомлений, чтобы сигнализировать о том, что необходимо инициализировать уведомление о пузырьке.

✔ Как часть полезной нагрузки запроса на уведомление, включайте URL-адрес, где находится демонстрация содержимого.

✔ собрания не должен использовать модуль задачи.

> [!NOTE]
>
> * Эти уведомления имеют постоянный характер. Необходимо вызвать функцию [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического скрытие после того, как пользователь делает действие в веб-представлении. Это требование для отправки приложения. *См. также*, [Teams SDK: модуль задачи](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
>
> * Если вы хотите, чтобы ваше приложение поддерживает анонимных пользователей, то для исходного запроса на вызов необходимо использовать метаданные запроса (ИД пользователя) в объекте, а не метаданные `from.id` `from` `from.aadObjectId` запроса (Azure Active Directory ID пользователя). *См.* ["Использование модулей задач на вкладке"](../task-modules-and-cards/task-modules/task-modules-tabs.md) и ["Создание и отправка модуля задачи".](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

### <a name="after-a-meeting"></a>После собрания

Конфигурации после собрания и до собрания эквивалентны.

## <a name="meeting-app-sample"></a>Пример приложения для собраний

 > [!div class="nextstepaction"]
> [Приложение генератора маркеров собраний](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
