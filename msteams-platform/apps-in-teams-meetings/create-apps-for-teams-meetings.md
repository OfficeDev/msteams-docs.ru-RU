---
title: Создание приложений для собраний групп
author: laujan
description: Создание приложений для собраний в Teams
ms.topic: conceptual
ms.author: lajanuar
keywords: API роли участника для собраний приложений Teams
ms.openlocfilehash: cf42d660c9b4a82f8e28d4d4379194c1bcc681e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796171"
---
# <a name="create-apps-for-teams-meetings-developer-preview"></a>Создание приложений для собраний в Teams (Предварительная версия для разработчиков)

>[!IMPORTANT]
> Функции, включенные в Microsoft Teams Preview, предоставляются только для раннего доступа, тестирования и создания отзывов. Они могут быть подвергнуты изменениям, прежде чем стать доступными в общедоступном выпуске и не должны использоваться в рабочих приложениях.

## <a name="prerequisites-and-considerations"></a>Необходимые условия и рекомендации

1. Приложения в собраниях требуют некоторых базовых знаний о [разработке приложений Teams](../overview.md). Приложение на собрании может состоять из компонентов [вкладок](../tabs/what-are-tabs.md), [Боты](../bots/what-are-bots.md)и [расширений обмена сообщениями](../messaging-extensions/what-are-messaging-extensions.md) и потребует обновления [манифеста приложения](#update-your-app-manifest) Teams, чтобы указать, что приложение доступно для собраний.

1. Чтобы ваше приложение функционировало в жизненном цикле собрания как вкладка, оно должно поддерживать настраиваемые вкладки в [области groupchat](../resources/schema/manifest-schema.md#configurabletabs). *Ознакомьтесь* [со статьей расширение приложения Teams с помощью настраиваемой вкладки](../tabs/how-to/add-tab.md). Поддержка `groupchat` области позволит приложению в беседах, [выполняемых перед собранием](teams-apps-in-meetings.md#pre-meeting-app-experience) и [после](teams-apps-in-meetings.md#post-meeting-app-experience) него.

1. Параметры URL-адреса API собраний могут потребоваться `meetingId` , `userId` а значение [tenantId](/onedrive/find-your-office-365-tenant-id) — в составе клиента Teams SDK и действия Bot. Кроме того, можно получить сведения о надежной информации для идентификатора пользователя и идентификатора клиента с помощью [проверки подлинности на основе единого входа](../tabs/how-to/authentication/auth-aad-sso.md).

1. Некоторые API собраний, например, `GetParticipant` требуют [регистрации Bot и идентификатора приложения Bot](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) для создания маркеров проверки подлинности.

1. Разработчикам следует соблюдать общие [рекомендации по проектированию вкладок Teams](../tabs/design/tabs.md) для сценариев, выполняемых перед и после собраний, а также [указания по диалоговому](design/designing-in-meeting-dialog.md) окну для собраний в диалоговом окне для собраний, инициированном во время собрания Teams.

## <a name="meeting-apps-api-reference"></a>Справочные материалы по API приложений для собраний

|API|Описание|Запрос|Источник|
|---|---|----|---|
|**жетусерконтекст**| Получение контекстной информации для отображения релевантного контента на вкладке "команды". |_**microsoftTeams. SPContext (() => {/ *...* / } )**_|Пакет SDK для клиента Microsoft Teams|
|**В качестве имени участника**|Этот API позволяет интерфейсу Bot получать сведения об участниках по идентификатору собрания и идентификатору участника.|**Получение** _**/v1/meetings/{meetingId}/Participants/{participantId}? tenantId = {tenantId}**_ |Пакет SDK Microsoft Bot Framework|
|**нотификатионсигнал** |Сигналы собраний будут доставляться с помощью следующего существующего API уведомления о беседе (для разговора пользователя в Bot). Этот API позволяет разработчикам сообщать на основании действий пользователя, чтобы показывать всплывающее диалоговое окно в собрании.|**POST** _**/v3/conversations/{conversationId}/Activities**_|Пакет SDK Microsoft Bot Framework|

### <a name="getusercontext"></a>жетусерконтекст

Обратитесь к нашему [контексту Get for Teams](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) , чтобы узнать, как идентифицировать и получить контекстные сведения для содержимого вкладки. В рамках расширяемости собраний для полезных данных ответа было добавлено новое значение.

✔ **meetingId** : используется вкладкой при запуске в контексте собрания.

### <a name="getparticipant-api"></a>API-интерфейс-участник

> [!NOTE]
>
> * Не кэшировать роли участников, так как организатор собрания может изменить роль в любой момент времени.
>
> * В настоящее время Teams не поддерживает большие списки рассылки или размеры списков, более 350 участников для `GetParticipant` API.
>
> * Поддержка пакет SDK для ленты скоро будет доступна.

#### <a name="request"></a>Запрос

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

*Ознакомьтесь* со статьей [Справочник по API-интерфейсу Bot Framework](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).

<!-- markdownlint-disable MD025 -->

**Пример на языке C#**

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
}
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**meetingId**| string | Да | Идентификатор собрания можно получить с помощью вызова Bot и клиента Teams SDK Teams.|
|**партиЦипантид**| string | Да | Это поле является ИДЕНТИФИКАТОРом пользователя и доступно в разделе SSO, вызове Bot и пакете SDK Teams. Настоятельно рекомендуется использовать единый вход.|
|**tenantId**| string | Да | Это необходимо для пользователей клиента. Он доступен при вводе-вызываемой клавишей TAB, с использованием ленты и клиента Teams SDK. Настоятельно рекомендуется использовать единый вход.|

#### <a name="response-payload"></a>Полезные данные ответа
<!-- markdownlint-disable MD036 -->

**роль** в разделе "собрание" может быть *организатором* , *докладчиком* или *участником* .

**Пример 1**

```json
{
  "user":
  {
      "id": "29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId": "6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name": "Allan Deyoung",
      "givenName": "Allan",
      "surname": "Deyoung",
      "email": "Allan.Deyoung@microsoft.com",
      "userPrincipalName": "Allan.Deyoung@microsoft.com",
      "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
      "userRole": "user"
  },
  "meeting":
  {
      "role ": "Presenter",
      "inMeeting":true
  },
  "conversation":
  {
      "id": "<conversation id>"
  }
}
```
#### <a name="response-codes"></a>Коды ответов

**403** : приложению не разрешено получать сведения об участнике. Это наиболее распространенный ответ об ошибке, который активируется, когда приложение не установлено в собрании, например, когда приложение отключено администратором клиента или блокируется во время снижения риска для Live сайта.  
**200** : сведения о участниках успешно получены  
**401** : недопустимый маркер  
**404** : собрание не существует или не удается найти его участника.

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a>API Нотификатионсигнал

> [!NOTE]
> Когда вызывается диалоговое окно для собраний, то то же самое содержимое также будет представлено в виде сообщения чата.

#### <a name="request"></a>Запрос

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a>Параметры запроса

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**conversationId**| string | Да | Идентификатор беседы доступен в составе вызова по методу Bot |

#### <a name="request-payload"></a>Полезные данные запроса

> [!NOTE]
>
> Комплетионботид в Екстерналресаурцеурл в полезных данных запроса является необязательным параметром. Это идентификатор Bot, объявленный в манифесте. Bot получит объект Result.

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
  };
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript

const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

* * *

> [!IMPORTANT]
> URL-адрес в пузырьке содержимого (URL-адрес Таскинфо) должен быть включен в список [допустимых доменов](../resources/schema/manifest-schema.md#validdomains) , включенный в манифест приложения Teams.

#### <a name="response-codes"></a>Коды ответов

**201** : действие с сигналом успешно отправлено  
**401** : недопустимый маркер  
**403** : приложению не разрешено отправлять сигнал. В этом случае полезная нагрузка должна содержать более подробное сообщение об ошибке. Может быть несколько причин: приложение отключено администратором клиента, заблокировано во время снижения риска на сайте Live и т. д.  
**404** : чат для собрания не существует  

## <a name="enable-your-app-for-teams-meetings"></a>Включение собраний для приложений в Teams

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Возможности приложений для собраний объявляются в манифесте приложения с **configurableTabs** помощью  ->  **областей** конфигураблетабс и **контекстных** массивов. *Область* определяет, для кого и *контекст* определяет, где будет доступно ваше приложение.

> [!NOTE]
> * Используйте [схему манифеста Preview для разработчиков](../resources/schema/manifest-schema-dev-preview.md) , чтобы попробовать это в манифесте приложения.

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

Вкладка `context` и `scopes` свойства работают по гармонии, чтобы определить, где должно отображаться ваше приложение. Вкладки в `team` `groupchat` области действия могут иметь более одного контекста. Для свойства Context возможны следующие значения:

* **чаннелтаб** : вкладка в заголовке канала команды.
* **приватечаттаб** : вкладка в заголовке группового чата между набором пользователей, которых нет в контексте команды или собрания.
* **митингчаттаб** : вкладка в заголовке группового чата между набором пользователей в контексте запланированного собрания.
* **митингдетаилстаб** : вкладка в заголовке представления сведений о собрании календаря.
* **митингсидепанел** : панель для собраний, открытая с помощью унифицированной панели (u-борта).

> [!NOTE]
> В настоящее время свойство "Context" в настоящее время не поддерживается и поэтому будет игнорироваться на мобильных клиентах

## <a name="configure-your-app-for-meeting-scenarios"></a>Настройка приложения для сценариев собраний

> [!NOTE]
> * Чтобы ваше приложение отображалось в коллекции вкладок, оно должно **поддерживать настраиваемые вкладки** и **область применения группового чата** .
>
> * Мобильные клиенты поддерживают вкладки только на поверхностях предварительных и посылаемых собраний. Скоро будет доступен интерфейс для собраний (диалоговое окно и панель на собрании) на мобильном устройстве. Следуйте [указаниям по использованию вкладок на мобильном устройстве](../tabs/design/tabs-mobile.md) при создании вкладок для мобильного устройства. 

### <a name="pre-meeting"></a>Предварительное собрание

Пользователи с ролями органайзера и докладчика добавляют вкладки на собрание с помощью кнопки "плюс ➕" в разделе " **беседы** для собраний" и " **сведения о** собрании". Расширения обмена сообщениями добавляются в меню "многоточия/переполнение" &#x25CF;&#x25CF;&#x25CF; , расположенного под областью создание сообщения в чате. Боты добавляются в чат для собрания с помощью **@** ключа "" и выбора **Get Боты** .

✔ Удостоверение пользователя *должно* быть подтверждено с помощью [единого входа вкладок](../tabs/how-to/authentication/auth-aad-sso.md). После проверки подлинности приложение может получить роль пользователя через API-участник.

 ✔ На основе роли пользователя, приложение теперь будет иметь возможность для отображения специальных интерфейсов для ролей. Например, приложение опроса может разрешить только организаторов и докладчикам создавать новый опрос.

> **Note** : назначения ролей могут быть изменены во время собрания.  *Просмотр* [ролей в собрании Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019). 

### <a name="in-meeting"></a>На собрании

#### <a name="sidepanel"></a>**сидепанел**

✔ В манифесте приложения добавьте **сидепанел** в массив **контекста** , как описано выше.

✔ На собрании, так же, как и во всех сценариях, приложение будет отображаться на вкладке, расположенной в собрании, 320 пикселей по ширине. Для этого необходимо оптимизировать вкладку. *Просмотр* , [интерфейс фрамеконтекст](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)

✔ Ссылаться на [пакет SDK Teams](../tabs/how-to/access-teams-context.md#user-context) , чтобы использовать API **UserContext** для соответствующей маршрутизации запросов.

✔ Ссылаться на [процесс проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md). Процесс проверки подлинности для вкладок очень похож на процесс проверки подлинности для веб-сайтов. Таким образом, вкладки могут напрямую использовать OAuth 2,0. *Кроме того, можно просмотреть* [потоки кода авторизации для платформы Microsoft identity и OAuth 2,0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

#### <a name="in-meeting-dialog"></a>**диалоговое окно "в собрании"**

✔ Необходимо следовать [рекомендациям по разработке диалоговых окон для собраний](design/designing-in-meeting-dialog.md).

✔ Ссылаться на [процесс проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md).

✔ Использовать API [уведомлений](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) для сигнализации о необходимости запуска пузырькового уведомления.

✔ Как часть полезных данных запроса уведомления, укажите URL-адрес, по которому размещается контент, предназначенный для демонстрации.

> [!NOTE]
>
> * Эти уведомления постоянны. Необходимо вызвать функцию [**субмиттаск ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) для автоматического закрытия после того, как пользователь выполняет действие в веб-представлении. Это требование для отправки приложения. *Раздел* [пакет SDK для teams: Task module](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true).
>
> * Если вы хотите, чтобы приложение поддерживало анонимных пользователей, полезные данные начального запроса вызова должны полагаться на `from.id`  метаданные запроса (ID пользователя) в `from` объекте, а не на `from.aadObjectId` метаданные запроса (идентификатор Azure Active Directory для пользователя). *Просмотрите раздел* [Использование модулей задач на вкладках](../task-modules-and-cards/task-modules/task-modules-tabs.md) и [Создайте и отправьте модуль задач](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request).

### <a name="post-meeting"></a>Завершающее собрание

Конфигурации после собрания и предварительного собрания эквивалентны.

## <a name="meeting-app-sample"></a>Пример приложения для собраний

 > [!div class="nextstepaction"]
> [Приложение генератора маркеров собраний](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
