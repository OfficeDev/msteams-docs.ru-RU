---
title: Создание приложений для собраний групп
author: laujan
description: создание приложений для собраний групп
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: команды приложений встречи пользователь участник роль api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565916"
---
# <a name="create-apps-for-teams-meetings"></a>Создание приложений для собраний Teams

## <a name="prerequisites-and-considerations"></a>Предпосылки и соображения

Прежде чем создавать приложения Teams собраний, необходимо иметь представление о следующем:

* Вы должны иметь знания о том, как Teams приложений. Для получения дополнительной информации [с Teams м.](../overview.md)

* Необходимо обновить манифест Teams, чтобы указать, что приложение доступно для встреч. Для получения дополнительной информации [см.](#update-your-app-manifest)

* Для того чтобы ваше приложение функционировало в жизненном цикле собрания в качестве вкладки, оно должно поддерживать настраиваемые вкладки в области группового чата. Для получения дополнительной информации [можно просмотреть область группового](../resources/schema/manifest-schema.md#configurabletabs) [чата и создать вкладку группы.](../build-your-first-app/build-channel-tab.md)

* Необходимо придерживаться общих Teams разработке вкладок для сценариев предварительного и после собрания. Для получения опыта во время встреч обратитесь к вкладке в заседании и рекомендациям по проектированию диалогов на совещании. Для получения дополнительной информации [см. Teams руководства по проектированию вкладок,](../tabs/design/tabs.md) [рекомендации по проектированию вкладок](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) на совещании [и рекомендации по проектированию диалоговых диалогов.](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)

* Необходимо поддерживать область `groupchat` действия приложения в чатах перед встречей и после собрания. С помощью приложения перед встречей можно найти и добавить приложения для встреч и выполнить задачи перед встречей. С помощью приложения после собрания можно просматривать результаты собрания, такие как результаты опроса или отзывы.

* Совещание параметров URL API должно `meetingId` `userId` иметь, и `tenantId` . Они доступны в рамках программы Teams SDK и бота. Кроме того, надежную информацию для идентификатора пользователя и идентификатора клиента можно получить с помощью [проверки подлинности Tab SSO.](../tabs/how-to/authentication/auth-aad-sso.md)

* API `GetParticipant` должен иметь регистрацию бота и ID для создания токенов auth. Для получения дополнительной информации, [см.](../build-your-first-app/build-bot.md)

* Для обновления приложения в режиме реального времени оно должно быть обновлено на основе событий на собрании. Эти события могут быть в поле диалога на встрече и на других этапах жизненного цикла собрания. Для окна диалога на встрече см. `bot Id` `Notification Signal API`

## <a name="meeting-apps-api-reference"></a>Совещание приложений API ссылки

|API|Описание|Запрос|Источник|
|---|---|----|---|
|**GetUserContext**| Этот API позволяет получать контекстную информацию для отображения соответствующего контента в Teams вкладке. |_**microsoftTeams.getContext (>) / } )**_|Microsoft Teams клиент SDK|
|**ПолучитьПартийный**| Этот API позволяет боту получать информацию об участниках, вевея идентификатор и идентификатор участника. |**GET** _**/v1/meetings/«meetingId»/участники/«участникИ?арендаторИдеантия»**_ |Microsoft Bot Framework СДК|
|**УведомлениеСгальный** | Этот API позволяет предоставлять сигналы собрания, которые доставляются с помощью существующего API уведомления о разговоре для чата пользователя-бота. Это позволяет сигнализировать на основе действий пользователя, который показывает в заседании диалоговое окно. |**POST** _**/v3/разговоры/РазговорИде/деятельность**_|Microsoft Bot Framework СДК|

### <a name="getusercontext"></a>GetUserContext

Чтобы определить и получить контекстную информацию для содержимого вкладки, [смотрите контекст для вашей вкладки Teams вкладку.](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) `meetingId`используется вкладкой при запуске в контексте собрания и добавляется для полезной нагрузки ответа.

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * Не кэшировать роли участников, так как организатор собрания может изменить роль в любое время.
> * Teams в настоящее время не поддерживает большие списки рассылки или реестр размеров более 350 участников для `GetParticipant` API.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| string | Да | Идентификатор собрания доступен через Bot Invoke и Teams Client SDK.|
|**участникИ**| string | Да | Идентификатор участника является идентификатором пользователя. Он доступен в Tab SSO, Bot Invoke и Teams Client SDK. Рекомендуется получить идентификатор участника из Tab SSO. |
|**tenantId**| string | Да | Идентификатор арендатора требуется пользователям-арендаторам. Он доступен в Tab SSO, Bot Invoke и Teams Client SDK. Рекомендуется получить идентификатор арендатора в Tab SSO. |

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

Орган реагирования JSON `GetParticipant` для API:

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
| **403** | Приложение не имеет права получать информацию о участнике. Это наиболее распространенный ответ на ошибку и срабатывает, если приложение не установлено на собрании. Например, если приложение отключено администратором-арендатором или заблокировано во время миграции живого сайта.|
| **200** | Информация об участнике успешно извлекается.|
| **401** | Приложение отвечает недействительным маркером.|
| **404** | Заседание либо истекло, либо участник не может быть найден.|
| **500** | Срок действия собрания либо истек более чем на 60 дней с момента окончания собрания, либо у участника нет разрешений, основанных на его роли.|

### <a name="notificationsignal-api"></a>УведомлениеСеньальный API

Все пользователи на собрании получают уведомления, отправленные через `NotificationSignal` API.

> [!NOTE]
> * При вызываемом диалоговом поле на собрании содержимое представляется как сообщение чата.
> * В настоящее время отправка целевых уведомлений не поддерживается.

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| string | Да | Идентификатор разговора доступен как часть вызова бота. |

#### <a name="example"></a>Пример

Объявлен `Bot ID` в манифесте и бот получает объект результата.

> [!NOTE]
> * Параметр `completionBotId` не является обязательным в `externalResourceUrl` запрошенном примере полезной нагрузки. `Bot ID` объявляется в манифесте, и бот получает объект результата.
> * Параметры `externalResourceUrl` ширины и высоты должны быть в пикселях. Чтобы убедиться, что размеры находятся в пределах разрешенных пределов, [см.](design/designing-apps-in-meetings.md)
> * URL-адрес — это страница, загруженная `<iframe>` в диалоговое окно во время встречи. Домен должен быть в массиве приложения в `validDomains` манифесте приложения.

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
| **201** | Деятельность с сигналом успешно отправляется. |
| **401** | Приложение отвечает недействительным маркером. |
| **403** | Приложение не может послать сигнал. Это может произойти по разным причинам, таким как администратор-арендатор отключает приложение, приложение блокируется во время миграции живого сайта и так далее. В этом случае полезная нагрузка содержит подробное сообщение об ошибке. |
| **404** | Чат собрания не существует. |

## <a name="enable-your-app-for-teams-meetings"></a>Включить приложение для Teams собраний

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Возможности приложения для собраний заявлены в манифесте приложения `configurableTabs` с `scopes` использованием `context` массивов и массивов. Область данных определяет, кому и контекст определяет, где доступно ваше приложение.

> [!NOTE]
> Попробуйте обновить манифест приложения с помощью [явной схемы.](../resources/schema/manifest-schema-dev-preview.md)
> Приложения на собраниях нуждаются в *сфере группового* чата. Область *действия* команды работает только для вкладок в каналах.

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

### <a name="context-property"></a>Свойство контекста

Вкладка `context` и `scopes` свойства позволяют определить, где должно отображаться ваше приложение. Вкладки в `team` области или области могут иметь несколько `groupchat` контекстов. Ниже приведены значения для `context` свойства, из которого можно использовать все или некоторые значения:

|Значение|Описание|
|---|---|
| **каналТаб** | Вкладка в заголовке командный канал. |
| **privateChatTab** | Вкладка в заголовке группового чата между набором пользователей не в контексте группы или собрания. |
| **meetingChatTab** | Вкладка в заголовке группового чата между набором пользователей в контексте запланированного собрания. |
| **встречаДтейлТайлТаб** | Вкладка в заголовке представления деталей собрания календаря. |
| **meetingSidePanel** | Панель заседаний открылась через единый бар (U-bar). |
| **meetingStage** | Приложение с боковойпанеля может быть передано на стадию собрания. |

> [!NOTE]
> `Context` недвижимость в настоящее время не поддерживается на мобильных клиентов.

## <a name="configure-your-app-for-meeting-scenarios"></a>Настройка приложения для сценариев встреч

> [!NOTE]
> * Чтобы ваше приложение было видно в галерее вкладок, оно должно поддерживать настраиваемые вкладки и область группового чата.
> * Мобильные клиенты поддерживают вкладки только на стадии предварительного и после собрания.
> * Опыт встречи, который является диалоговым окном и вкладкой на встрече, в настоящее время не поддерживается мобильными клиентами. Для получения дополнительной информации, [см. руководство для вкладок на мобильный](../tabs/design/tabs-mobile.md) при создании вкладок для мобильных устройств.

### <a name="before-a-meeting"></a>Перед собранием

Перед собранием пользователи могут добавлять вкладки, боты и расширения обмена сообщениями на собрание. Пользователи с ролями организатора и докладчика могут добавлять вкладки на собрание.

**Добавление вкладки к собранию**

1. В календаре выберите собрание, к которому вы хотите добавить вкладку.
1. Выберите **вкладку Подробная** информация и выберите плюс <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. Появляется галерея вкладок.

    ![Опыт предварительного собрания](../assets/images/apps-in-meetings/PreMeeting.png)

1. В галерее вкладок выберите приложение, которое вы хотите добавить, и следуйте необходимым шагам. Приложение устанавливается в качестве вкладки.
    > [!NOTE] 
    > В настоящее время во вкладке заседаний получение информации о собраниях и участниках не поддерживается.

**Добавление расширения обмена сообщениями на собрание**

1. Выберите эллипсы или меню переполнения &#x25CF;&#x25CF;&#x25CF; , расположенных в области композиций сообщений в чате.
1. Выберите приложение, которое вы хотите добавить, и следуйте необходимым шагам. Приложение устанавливается в качестве расширения обмена сообщениями.

**Добавление бота на собрание**

В чате собрания введите **@** ключ и выберите **Get bots**.

> [!NOTE]
> * Личность пользователя должна быть подтверждена с [помощью Tabs SSO](../tabs/how-to/authentication/auth-aad-sso.md). После проверки подлинности приложение может получить роль пользователя с помощью `GetParticipant` API.
> * Основываясь на роли пользователя, приложение имеет возможность предоставлять ролевые опыты. Например, приложение для голосования позволяет создавать новый опрос только организаторам и докладчикам.
> * Назначения роли могут быть изменены во время собрания. Для получения дополнительной информации [см Teams.](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

### <a name="during-a-meeting"></a>Во время собрания

#### <a name="sidepanel"></a>sidePanel

С sidePanel, вы можете настроить опыт в заседании, которые позволяют организаторам и докладчикам иметь различный набор представлений и действий. В манифесте приложения необходимо добавить sidePanel в массив контекста. В собрании и во всех сценариях приложение отображается во вкладке, которая составляет 320 пикселей в ширину. Для получения дополнительной информации [см.](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

Чтобы использовать `userContext` API для соответствующих запросов маршрута, [см. Teams SDK](../tabs/how-to/access-teams-context.md#user-context). Можно [Teams потока аутентификации для вкладок.](../tabs/how-to/authentication/auth-flow-tab.md) Поток аутентификации для вкладок очень похож на поток ва-аута для веб-сайтов. Таким образом, вкладки могут использовать OAuth 2.0 напрямую. Смотрите, [платформа удостоверений Майкрософт и OAuth 2.0 поток кода авторизации](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

Расширение обмена сообщениями работает, как и ожидалось, когда пользователь находится в представлении на собрании, и пользователь может размещать карточки расширения составить сообщения. AppName in-meeting — это инструмент, в который упомятается имя приложения в собрании U-bar.

> [!NOTE]
> Используйте версию 1.7.0 [или выше Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), так как версии до нее не поддерживают боковую панель.

#### <a name="in-meeting-dialog"></a>Диалоговое окно собрания

Диалоговое окно на собрании может быть использовано для привлечения участников во время собрания и сбора информации или обратной связи во время собрания. Используйте [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API, чтобы сигнализировать о том, что уведомление о пузыре должно быть срабатывать. В рамках полезной нагрузки запроса уведомлений включите URL-адрес, в котором размещается содержимое, которое будет показано.

Диалог на встрече не должен использовать модуль задачи. Модуль задачи не вызывается в чате собрания. URL-адрес внешнего ресурса используется для отображения пузыря содержимого на собрании. Метод можно использовать `submitTask` для отправки данных в чате собрания.

> [!NOTE]
> * Вы должны вызвать [функцию submitTask ()](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического увольнения после того, как пользователь принимает меры в веб-представлении. Это требование для отправки приложения. Для получения дополнительной информации [с Teams м.](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)
> * Если вы хотите, чтобы ваше приложение поддержало анонимных пользователей, ваша первоначальная полезная нагрузка запроса на вызов `from.id` должна опираться на метаданные `from` запроса в объекте, а `from.aadObjectId` не на метаданные запроса. `from.id`является идентификатором пользователя `from.aadObjectId` и Azure Active Directory (AAD) идентификатором пользователя. Для получения дополнительной информации [см.](../task-modules-and-cards/task-modules/task-modules-tabs.md) [](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)

#### <a name="share-to-stage"></a>Делитесь на сцену 

> [!NOTE]
> * Эта возможность в настоящее время доступна только в предварительном просмотре разработчика.
> * Чтобы использовать эту функцию, приложение должно поддерживать боковойпанель в заседании.


Эта возможность дает разработчикам возможность поделиться приложением на этапе собрания. Включив совместное участие в стадии собрания, участники собрания могут сотрудничать в режиме реального времени. 

Необходимый контекст находится `meetingStage` в манифесте приложения. Предпосылкой для этого является иметь `meetingSidePanel` контекст. Это позволяет кнопку **Доля** в sidepanel как depecited в следующем изображении:

  ![share_to_stage_during_meeting опыт](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

Явное изменение, необходимое для включения этой возможности, заключается в следующем: 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a>После собрания

Конфигурации после собрания и предварительного собрания эквивалентны.

## <a name="code-sample"></a>Пример кода

|Название образца | Описание | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| Разгибаемость заседаний | Microsoft Teams образец разгибаемости для передачи токенов. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Встреча содержание пузырь бот | Microsoft Teams примеру разгибаемости для взаимодействия с ботом пузыря содержимого на собрании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Встреча SidePanel | Microsoft Teams выборка для итерактирования с боковой панелью в заседании. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a>См. также

* [Руководящие принципы проектирования диалогов на совещании](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams проверки подлинности для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
