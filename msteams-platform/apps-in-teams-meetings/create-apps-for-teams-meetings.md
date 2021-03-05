---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний групп
ms.topic: conceptual
ms.author: lajanuar
keywords: teams apps meetings user participant role api
ms.openlocfilehash: bd0f53ae34a23bdbbdc2e6f3992c7dd0836e9f28
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449495"
---
# <a name="create-apps-for-teams-meetings"></a>Создание приложений для собраний Teams

## <a name="prerequisites-and-considerations"></a>Предпосылки и соображения

* Приложения на собраниях требуют некоторых базовых знаний о разработке [приложений Teams.](../overview.md) Приложение на собрании может состоять [](../bots/what-are-bots.md)из функций [](../messaging-extensions/what-are-messaging-extensions.md) вкладок, [](../tabs/what-are-tabs.md)ботов и расширений обмена сообщениями и потребует обновлений манифеста приложения [Teams,](#update-your-app-manifest) чтобы указать, что приложение доступно для собраний.

* Чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области [группового](../resources/schema/manifest-schema.md#configurabletabs) чата (см. в нем, как создать [вкладку группы).](../build-your-first-app/build-channel-tab.md) Поддержка области `groupchat` позволит вашему [](teams-apps-in-meetings.md#pre-meeting-app-experience) приложению использовать чаты перед собранием и [после](teams-apps-in-meetings.md#post-meeting-app-experience) собрания.

* Для параметров URL-адресов API собраний может потребоваться , и tenantId Они доступны в рамках `meetingId` `userId` SDK клиента Teams и бота. [](/onedrive/find-your-office-365-tenant-id) Кроме того, с помощью проверки подлинности [Tab SSO](../tabs/how-to/authentication/auth-aad-sso.md)можно получить достоверную информацию для идентификации пользователя и клиента.

* Некоторые API собраний, например, требуют регистрации бота и `GetParticipant` [ID](../build-your-first-app/build-bot.md) для создания маркеров auth.

* Необходимо придерживаться общих правил разработки вкладок [Teams](../tabs/design/tabs.md) для сценариев до и после собрания. Для работы во время собраний [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) обратитесь к [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) вкладке на собрании и рекомендациям по проектированию диалогов на собрании.

* Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании. Эти события могут быть в диалоговом окну (обратитесь к параметру завершения) и другим поверхностям на `bot Id` `Notification Signal API` жизненном цикле собрания.

## <a name="meeting-apps-api-reference"></a>Ссылка на API приложений для собраний

|API|Описание|Запрос|Источник|
|---|---|----|---|
|**GetUserContext**| Получите контекстную информацию для отображения соответствующего контента на вкладке Teams. |_**microsoftTeams.getContext() => { /*...* / } )**_|Клиент Microsoft Teams SDK|
|**GetParticipant**|Этот API позволяет боту получать сведения о участниках, встречая id и id участника.|**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |Сигналы собрания будут доставляться с помощью следующего существующего API уведомлений о беседе (для чата пользователя-бота). Этот API позволяет разработчикам сигнализировать на основе действий конечных пользователей, чтобы показать в случае встречи диалоговое пузырек.|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Обратитесь к нашему [контексту Get for your Teams tab](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) documentation for guidance on identifying and retrieving contextual information for your tab content. В рамках расстановки собраний добавлено новое значение для полезной нагрузки ответа:

✔ **meetingId**: используется вкладками при работе в контексте собрания.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * Не кэшить роли участников, так как организатор собрания может изменить роль в любой момент времени.
>
> * В настоящее время teams не поддерживают большие списки рассылки или размер реестра, вметив более 350 `GetParticipant` участников для API.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| string | Да | Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.|
|**participantId**| string | Да | УчастникId — это пользовательский ID. Он доступен в SSO tab, Bot Invoke и Teams Client SDK. Настоятельно рекомендуется получить участникаId из SSO tab. |
|**tenantId**| string | Да | TenantId является обязательной для пользователей-клиентов. Он доступен в SSO tab, Bot Invoke и Teams Client SDK. Настоятельно рекомендуется получить tenantId из SSO tab. |

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
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
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

* **403.** Приложение не может получать сведения о участниках. Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании. Например, если приложение отключено администратором клиента или заблокировано во время смягчения последствий для жизни.
* **200.** Успешно извлекаемая информация участника.
* **401.** Недействительный маркер.
* **404.** Участник не может быть найден.
* **500.** Срок действия собрания истек (более 60 дней с момента окончания собрания), либо у участника нет разрешений, основанных на их роли.


**Ожидается в ближайшее время**

* **404.** Собрание истеко или участник не может быть найден.


### <a name="notificationsignal-api"></a>NotificationSignal API

Все пользователи на собрании получают уведомления, отправленные через API NotificationSignal.

> [!NOTE]
> В настоящее время отправка целевых уведомлений не поддерживается.
> Когда вызывается диалоговое окно в собрании, то тот же контент также будет представлен в качестве сообщения чата.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| string | Да | Идентификатор беседы доступен в рамках вызова бота |

#### <a name="example"></a>Пример

Объявляется `Bot ID` в манифесте, и бот получает объект результата. В следующем примере параметр необязательный в `completionBotId` `externalResourceUrl` запрашиваемой полезной нагрузке:

> [!NOTE]
> * Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях. Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)
> * URL-адрес — это страница, загруженная в диалоговом окруже `<iframe>` на собрании. Домен должен быть в массиве приложения в `validDomains` манифесте приложения.

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

* **201.** Успешно отправляется действие с сигналом. 
* **401.** Недействительный маркер.
* **403.** Приложение не может отправить сигнал. Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее. В этом случае полезное сообщение содержит подробное сообщение об ошибке. 
* **404.** Чат собраний не существует.
 

## <a name="enable-your-app-for-teams-meetings"></a>Включить приложение для собраний Teams

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Возможности приложения собраний объявляются в манифесте приложения с помощью настраиваемых областей **и**  ->   массивов **контекста.** *Область* определяет, кому и *в котором контекст* определяет, где будет доступно ваше приложение.

> [!NOTE]
> Используйте [схему Developer Preview манифеста,](../resources/schema/manifest-schema-dev-preview.md) чтобы попробовать это в манифесте приложения.

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

Вкладка и свойства работают в гармонии, чтобы определить, где нужно `context` `scopes` отображаться ваше приложение. Вкладки в области или области `team` `groupchat` могут иметь несколько контекстов. Возможные значения для свойства контекста следующим образом:

* **channelTab**: вкладка в загонах канала команды.
* **privateChatTab**: вкладка в загона группового чата между набором пользователей, не в контексте группы или собрания.
* **meetingChatTab**: вкладка в заглавной части группового чата между набором пользователей в контексте запланированного собрания.
* **meetingDetailsTab**: вкладка в заглавной части представления сведений о собрании календаря.
* **meetingSidePanel**: панель на собрании, открытая с помощью единой панели (u-bar).

> [!NOTE]
> Свойство "Context" в настоящее время не поддерживается и, таким образом, будет игнорироваться для мобильных клиентов

## <a name="configure-your-app-for-meeting-scenarios"></a>Настройка приложения для сценариев собраний

> [!NOTE]
> * Чтобы приложение было видимым в галерее вкладок, оно должно поддерживать **настраиваемые** вкладки и область **группового чата.**
>
> * Мобильные клиенты поддерживают вкладки только в pre и post meeting Surfaces. В ближайшее время будут доступны опытом в собрании (диалоговое окно и вкладка на собрании) на мобильном телефоне. Следуйте [указаниям для вкладок на мобильных устройствах](../tabs/design/tabs-mobile.md) при создании вкладок для мобильных устройств.

### <a name="before-a-meeting"></a>Перед собранием

Пользователи с ролями организатора и/или презента добавляют вкладки на  собрание с помощью кнопки плюс ➕ на страницах чата собрания и сведений **о** собраниях. Расширения обмена сообщениями добавляются в меню эллипсов и переполнений &#x25CF;&#x25CF;&#x25CF; под областью составить сообщение в чате. Боты добавляются в чат собраний с помощью ключа **@** "" и выбора **ботов Get.**

✔ удостоверение пользователя *должно* быть подтверждено с помощью [SSO Tabs.](../tabs/how-to/authentication/auth-aad-sso.md) После проверки подлинности приложение может получить роль пользователя с помощью API GetParticipant.

 ✔ зависимости от роли пользователя приложение теперь будет иметь возможность представлять определенные функции. Например, приложение для опроса может разрешить создавать новый опрос только организаторам и презентаторам.

> **ПРИМЕЧАНИЕ.** Назначения ролей могут быть изменены во время собрания.  *См.* [роли в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019) 

### <a name="during-a-meeting"></a>Во время собрания

#### <a name="sidepanel"></a>**sidePanel**

✔ В манифесте приложения добавьте **sidePanel** в массив **контекста,** как описано выше.

✔ на собрании, как и во всех сценариях, приложение будет отрисовка на вкладке в собрании шириной 320px. Для этого необходимо оптимизировать вкладку. *См.* интерфейс [FrameContext](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔Refer для команд [SDK,](../tabs/how-to/access-teams-context.md#user-context) чтобы использовать **API userContext** для маршрутных запросов соответственно.

✔ Обратитесь к потоку [проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md). Поток проверки подлинности для вкладок очень похож на поток auth для веб-сайтов. Таким образом, вкладки могут напрямую использовать OAuth 2.0. *См. также,* платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

✔ расширение сообщения должно работать так, как ожидалось, когда пользователь находится в представлении на собрании и должен иметь возможность отправлять составить карточки расширения сообщений.

✔ AppName на собрании — Tooltip должен указать имя приложения на собрании U-bar.

#### <a name="in-meeting-dialog"></a>**Диалоговое окно собрания**

✔ Необходимо придерживаться рекомендаций по проектированию диалогов на [собрании.](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

✔ Обратитесь к потоку [проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).

✔ [API NotificationSignal](create-apps-for-teams-meetings.md#notificationsignal-api) для сигнала о том, что нужно запускать уведомление о пузыре.

✔ В качестве части полезной нагрузки запроса уведомлений включайте URL-адрес, на котором будет демонстрироваться содержимое.

✔ диалоговое окно на собрании не должно использовать модуль задач.

> [!NOTE]
>
> * Эти уведомления являются постоянными по своему характеру. После действия пользователя в веб-представлении необходимо вызвать функцию [**submitTask()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения. Это требование для отправки приложения. *См. также*, [Teams SDK: модуль задач](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
>
> * Если вы хотите, чтобы приложение поддержало анонимных пользователей, ваша начальная нагрузка запроса на вызов должна опираться на метаданные запроса (ID пользователя), а не метаданные `from.id` `from` `from.aadObjectId` запроса (Azure Active Directory пользователя). *См.* [в рубке](../task-modules-and-cards/task-modules/task-modules-tabs.md) Использование модулей задач и создание и [отправка модуля задач.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

### <a name="after-a-meeting"></a>После собрания

Конфигурации после собрания и предварительного собрания эквивалентны.

## <a name="meeting-app-sample"></a>Пример приложения для собраний

 > [!div class="nextstepaction"]
> [Приложение генератора маркеров собраний](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
