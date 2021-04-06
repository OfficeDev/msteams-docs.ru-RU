---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний групп
ms.topic: conceptual
ms.author: lajanuar
keywords: teams apps meetings user participant role api
ms.openlocfilehash: ba00a2dc78cefb167f1bef8507f32dad5e38452c
ms.sourcegitcommit: e78c9f51c4538212c53bb6c6a45a09d994896f09
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/05/2021
ms.locfileid: "51585850"
---
# <a name="create-apps-for-teams-meetings"></a>Создание приложений для собраний Teams

## <a name="prerequisites-and-considerations"></a>Предпосылки и соображения

Прежде чем создавать приложения для собраний Teams, необходимо иметь представление о следующих ниже.

* Вы должны иметь знания о разработке приложений Teams. Дополнительные сведения см. в [приложении Teams.](../overview.md)

* Необходимо обновить манифест приложения Teams, чтобы указать, что приложение доступно для собраний. Дополнительные сведения см. в [манифесте приложения.](#update-your-app-manifest)

* Чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области groupchat. Дополнительные сведения см. в [поле groupchat и](../resources/schema/manifest-schema.md#configurabletabs) [создайте вкладку группы.](../build-your-first-app/build-channel-tab.md)

* Необходимо придерживаться общих правил разработки вкладок Teams для сценариев до и после собрания. Для работы во время собраний обратитесь к вкладке на собрании и рекомендациям по проектированию диалогов на собрании. Дополнительные сведения см. в рекомендациях по разработке вкладок [Teams,](../tabs/design/tabs.md)рекомендациях по разработке вкладок на собрании и рекомендациях по проектированию диалогов на [собрании.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) [](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)

* Необходимо поддерживать область, чтобы включить приложение в чаты перед собранием и `groupchat` после собрания. С помощью предварительного собрания приложения можно найти и добавить приложения для собраний и выполнить задачи перед собранием. С помощью приложения после собрания можно просмотреть результаты собрания, такие как результаты опроса или отзывы.

* Параметры URL-адресов API должны иметь `meetingId` и `userId` `tenantId` . Они доступны в рамках клиентской SDK и бот-активности Teams. Кроме того, с помощью проверки подлинности [Tab SSO](../tabs/how-to/authentication/auth-aad-sso.md)можно получить достоверную информацию для идентификации пользователя и идентификации клиента.

* API `GetParticipant` должен иметь регистрацию бота и ID для создания маркеров auth. Дополнительные сведения см. в [сведениях о регистрации ботов и ID.](../build-your-first-app/build-bot.md)

* Чтобы ваше приложение обновлялось в режиме реального времени, оно должно быть обновлено в зависимости от событий на собрании. Эти события могут быть в диалоговом окне собрания и на других этапах жизненного цикла собрания. Параметр завершения в диалоговом окне на собрании см. `bot Id` в `Notification Signal API` .

## <a name="meeting-apps-api-reference"></a>Ссылка на API приложений для собраний

|API|Описание|Запрос|Source|
|---|---|----|---|
|**GetUserContext**| Этот API позволяет получать контекстную информацию для отображения соответствующего контента на вкладке Teams. |_**microsoftTeams.getContext() => { /*...* / } )**_|Клиент Microsoft Teams SDK|
|**GetParticipant**| Этот API позволяет боту получать сведения о участниках, встречая ID и ID участника. |**GET** _**/v1/meetings/{meetingId}/participants/{participantsId}?tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомлений о беседе для чата пользователя-бота. Он позволяет сигнализировать на основе действий пользователя, отображает диалоговое окно на собрании. |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

Чтобы определить и получить контекстную информацию для содержимого вкладки, см. в тексте получить контекст [для вкладки Teams.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) `meetingId` используется вкладками при работе в контексте собрания и добавляется для полезной нагрузки ответа.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * Не кэшить роли участников, так как организатор собрания может изменить роль в любое время.
> * В настоящее время teams не поддерживают большие списки рассылки или размер реестра, вметив более 350 `GetParticipant` участников для API.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| string | Да | Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.|
|**participantId**| string | Да | ID участника — это пользовательский ИД. Он доступен в SSO tab, Bot Invoke и Teams Client SDK. Рекомендуется получить ID участника из SSO Tab. |
|**tenantId**| string | Да | Для пользователей-клиентов требуется ID клиента. Он доступен в SSO tab, Bot Invoke и Teams Client SDK. Рекомендуется получить ID клиента из SSO tab. |

#### <a name="example"></a>Пример

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

* * *

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

|Код ответа|Описание|
|---|---|
| **403** | Приложение не может получать сведения о участниках. Это наиболее распространенный ответ на ошибки, который запускается, если приложение не установлено на собрании. Например, если приложение отключено администратором клиента или заблокировано во время переноса веб-сайтов в прямом эфире.|
| **200** | Данные участника успешно извлекаются.|
| **401** | Приложение отвечает недействительным маркером.|
| **404** | Собрание истеко или участник не может быть найден.|
| **500** | Срок действия собрания истек более 60 дней с момента окончания собрания, либо у участника нет разрешений, основанных на их роли.|

### <a name="notificationsignal-api"></a>NotificationSignal API

Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.

> [!NOTE]
> * При вызове диалогового окна на собрании содержимое представляется в качестве сообщения чата.
> * В настоящее время отправка целевых уведомлений не поддерживается.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| string | Да | Идентификатор беседы доступен в рамках вызова бота |

#### <a name="example"></a>Пример

Объявляется `Bot ID` в манифесте, и бот получает объект результата.

> [!NOTE]
> * Параметр `completionBotId` необязательный `externalResourceUrl` в примере запрашиваемой полезной нагрузки. `Bot ID` объявляется в манифесте, и бот получает объект результата.
> * Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях. Чтобы размеры были в пределах допустимого, см. в [рекомендациях по проектированию.](design/designing-apps-in-meetings.md)
> * URL-адрес — это страница, загруженная в диалоговом окне на `<iframe>` собрании. Домен должен быть в массиве приложения в `validDomains` манифесте приложения.

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

* * *

#### <a name="response-codes"></a>Коды ответа

|Код ответа|Описание|
|---|---|
| **201** | Успешно отправляется действие с сигналом |
| **401** | Приложение отвечает недействительным маркером. |
| **403** | Приложение не может отправить сигнал. Это может произойти из-за различных причин, таких как отключение приложения администратором клиента, блокировка приложения во время переноса веб-сайта в прямом эфире и так далее. В этом случае полезное сообщение содержит подробное сообщение об ошибке. |
| **404** | Чат собрания не существует. |

## <a name="enable-your-app-for-teams-meetings"></a>Включить приложение для собраний Teams

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Возможности приложения собраний объявляются в манифесте приложения с помощью `configurableTabs` массивов и `scopes` `context` массивов. Область определяет, кому и в котором контекст определяет, где доступно ваше приложение.

> [!NOTE]
> Попробуйте обновить манифест приложения с помощью [схемы манифеста.](../resources/schema/manifest-schema-dev-preview.md)
> Приложениям на собраниях нужна *область группового чата.* Область *команды* работает только для вкладок в каналах.

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
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> `meetingStage` в настоящее время доступна только в предварительном просмотре разработчика.

### <a name="context-property"></a>Свойство Context

Вкладка `context` и свойства позволяют `scopes` определить, где должно отображаться ваше приложение. Вкладки в области или области `team` `groupchat` могут иметь несколько контекстов. Ниже ниже 10 значений для свойства, из которого можно использовать все или некоторые `context` из этих значений:

|Значение|Описание|
|---|---|
| **channelTab** | Вкладка в загонах канала команды. |
| **privateChatTab** | Вкладка в загонах группового чата между набором пользователей, не в контексте группы или собрания. |
| **meetingChatTab** | Вкладка в загонах группового чата между набором пользователей в контексте запланированного собрания. |
| **meetingDetailsTab** | Вкладка в загонах сведений о собрании для просмотра календаря. |
| **meetingSidePanel** | Панель на собрании, открытая с помощью единой панели (U-bar). |
| **meetingStage** | Приложение из боковогопанеля можно использовать на стадии собрания. |

> [!NOTE]
> `Context` свойство в настоящее время не поддерживается для мобильных клиентов.

## <a name="configure-your-app-for-meeting-scenarios"></a>Настройка приложения для сценариев собраний

> [!NOTE]
> * Чтобы приложение было видимым в галерее вкладок, оно должно поддерживать настраиваемые вкладки и область группового чата.
> * Мобильные клиенты поддерживают вкладки только на этапах предварительного и после собраний.
> * В настоящее время в мобильных клиентах не поддерживается диалоговое окно и вкладка на собрании. Дополнительные сведения см. [в руководстве по вкладки на мобильных](../tabs/design/tabs-mobile.md) устройствах при создании вкладок для мобильных устройств.

### <a name="before-a-meeting"></a>Перед собранием

Перед собранием пользователи могут добавлять вкладки, боты и расширения обмена сообщениями на собрание. Пользователи с ролями организатора и презентовщика могут добавлять вкладки в собрание.

**Добавление вкладки к собранию**

1. В календаре выберите собрание, на которое нужно добавить вкладку.
1. Выберите **вкладку Details** и выберите плюс <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. Отображается галерея вкладок.

    ![Опыт предварительного собрания](../assets/images/apps-in-meetings/PreMeeting.png)

1. В галерее вкладок выберите приложение, которое необходимо добавить, и выполните необходимые действия. Приложение устанавливается в качестве вкладки.
    > [!NOTE] 
    > В настоящее время на вкладке "Собрания" сведения о собраниях и сведения о участниках не поддерживаются.

**Добавление расширения обмена сообщениями на собрание**

1. Выберите меню эллипсов или &#x25CF;&#x25CF;&#x25CF; , расположенное в области композитных сообщений в чате.
1. Выберите приложение, которое необходимо добавить, и выполните необходимые действия. Приложение устанавливается в качестве расширения обмена сообщениями.

**Добавление бота на собрание**

В чате собраний **@** введите ключ и выберите **Get bots**.

> [!NOTE]
> * Удостоверение пользователя должно быть подтверждено с помощью [SSO Tabs.](../tabs/how-to/authentication/auth-aad-sso.md) После проверки подлинности приложение может получить роль пользователя с помощью `GetParticipant` API.
> * В зависимости от роли пользователя приложение может предоставлять определенные функции. Например, приложение для опроса позволяет создавать новый опрос только организаторам и презентаторам.
> * Назначения ролей могут быть изменены во время собрания. Дополнительные сведения см. [в сведениях о ролях в собрании Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

### <a name="during-a-meeting"></a>Во время собрания

#### <a name="sidepanel"></a>sidePanel

В sidePanel можно настроить опыт собрания, который позволяет организаторам и презентаторам иметь различные представления и действия. В манифесте приложения необходимо добавить sidePanel в массив контекста. В собрании и во всех сценариях приложение отрисовка в вкладке в собрании шириной 320 пикселей. Дополнительные сведения см. в [интерфейсе FrameContext.](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

Чтобы использовать `userContext` API для соответственного маршрута запросов, см. [в рубрике Teams SDK.](../tabs/how-to/access-teams-context.md#user-context) См. [поток проверки подлинности Teams для вкладок.](../tabs/how-to/authentication/auth-flow-tab.md) Поток проверки подлинности для вкладок очень похож на поток auth для веб-сайтов. Таким образом, вкладки могут напрямую использовать OAuth 2.0. См., платформа удостоверений Майкрософт и поток кода авторизации [OAuth 2.0.](/azure/active-directory/develop/v2-oauth2-auth-code-flow)

Расширение обмена сообщениями работает так, как и ожидалось, когда пользователь находится в представлении на собрании, и пользователь может отправлять составить карточки расширения сообщений. AppName in-meeting — это инструмент, который сообщает имя приложения на собрании U-bar.

#### <a name="in-meeting-dialog"></a>Диалоговое окно собрания

Диалоговое окно на собрании можно использовать для вовлечения участников во время собрания и сбора сведений или отзывов во время собрания. Используйте [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API для сигнала о том, что необходимо вызвать уведомление о пузыре. В качестве полезной нагрузки запроса уведомлений включайте URL-адрес, на котором будет хозяйствовать контент.

Диалоговое окно на собрании не должно использовать модуль задач. Модуль задач не вызывается в чате собрания. Url-адрес внешнего ресурса используется для отображения пузыря контента на собрании. Этот метод можно `submitTask` использовать для отправки данных в чате собраний.

> [!NOTE]
> * Необходимо вызвать функцию [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения после действия пользователя в веб-представлении. Это требование для отправки приложения. Дополнительные сведения см. в [модуле задач Teams SDK.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)
> * Если вы хотите, чтобы ваше приложение поддержало анонимных пользователей, то при первоначальном запросе необходимо использовать метаданные запроса в объекте, а не `from.id` `from` `from.aadObjectId` метаданные запроса. `from.id` является ИД пользователя и `from.aadObjectId` является ИД Azure Active Directory (AAD). Дополнительные сведения см. в [таблицах](../task-modules-and-cards/task-modules/task-modules-tabs.md) с использованием модулей задач и созданием и [отправкой модуля задач.](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

#### <a name="share-to-stage"></a>Share to stage 

> [!NOTE]
> Эта возможность является avaialable только в предварительном просмотре инсайдерской версии разработчика


Эта возможность дает разработчикам возможность делиться приложением на стадии собрания. Включив совместное использование на этапе собрания, участники собраний могут сотрудничать в режиме реального времени. 

Необходимый контекст — meetingStage в манифесте приложения. Предварительным условием для этого является контекст meetingSidePanel. Это позволит включить кнопку "Share" в боковомпанеэле, как было приведено ниже.



### <a name="after-a-meeting"></a>После собрания

Конфигурации после собрания и предварительного собрания эквивалентны.

## <a name="code-sample"></a>Пример кода

|Пример имени | Описание | C# |
|----------------|-----------------|--------------|
| Разнонасть собраний | Пример extensibility microsoft Teams для передачи маркеров. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) |
| Бот-бот для пузырьков контента для собраний | Пример extensibility microsoft Teams для взаимодействия с ботом пузырьков контента на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [Рекомендации по проектированию диалогов на собрании](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
> [!div class="nextstepaction"]
> [Поток проверки подлинности teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
