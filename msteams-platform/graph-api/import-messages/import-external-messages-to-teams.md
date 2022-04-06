---
title: Использование Microsoft Graph для импорта сообщений внешней платформы в Teams
description: Описывается, как использовать Microsoft Graph для импорта сообщений с внешней платформы в Teams
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 5a33334367d0f5c229874decd5e45c5bb89ceafc
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685634"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph

С помощью microsoft Graph можно перенести существующий журнал сообщений и данные пользователей из внешней системы в Teams канала. Включив воссоздание иерархии обмена сообщениями на сторонней платформе внутри Teams, пользователи могут беспрепятственно продолжать общение и продолжать работу без прерывания.

> [!NOTE]
> В дальнейшем корпорация Майкрософт может потребовать у вас или ваших клиентов оплаты дополнительных сборов на основе количества импортированных данных.

## <a name="import-overview"></a>Общие сведения об импорте

На высоком уровне процесс импорта состоит из следующих элементов:

1. [Создайте команду со временной меткой](#step-1-create-a-team) времени.
1. [Создайте канал со временной меткой back-in-time](#step-2-create-a-channel).
1. [Импорт внешних сообщений с датой во времени](#step-3-import-messages).
1. [Завершите процесс миграции команды и канала](#step-4-complete-migration-mode).
1. [Добавление участников команды](#step-five-add-team-members).

## <a name="prerequisites"></a>Предварительные требования

### <a name="analyze-and-prepare-message-data"></a>Анализ и подготовка данных сообщений

* Просмотрите сторонние данные, чтобы решить, что будет перенесено.  
* Извлеките выбранные данные из сторонней системы чата.  
* Сопоставьте стороннюю структуру чата с Teams.  
* Преобразуйте данные импорта в формат, необходимый для миграции.  

### <a name="set-up-your-office-365-tenant"></a>Настройка клиента Office 365

* Убедитесь, Office 365 существует клиент для импорта данных. Дополнительные сведения о настройке Office 365 клиента для Teams см. в разделе Office 365 [клиента](../../concepts/build-and-test/prepare-your-o365-tenant.md).
* Убедитесь, что участники команды находятся в Azure Active Directory. Дополнительные сведения см. [в статье о добавлении нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure AD.

## <a name="step-1-create-a-team"></a>Шаг 1. Создание команды

Так как вы переносите существующие данные, сохранение исходных меток времени сообщений и предотвращение обмена сообщениями во время процесса миграции являются ключевыми для повторного создания существующего потока сообщений пользователя в Teams. Это достигается следующим образом:

> [Создайте новую команду с](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) временной меткой back-in-time, используя свойство ресурса `createdDateTime` группы. Поместите новую команду в специальное `migration mode`состояние, которое ограничивает пользователей от большинства действий в команде до завершения процесса миграции. Включите `teamCreationMode` атрибут экземпляра со значением `migration` в запрос POST, чтобы явно идентифицировать новую команду как созданную для миграции.  

> [!NOTE]
> Поле `createdDateTime` будет заполнено только для экземпляров команды или канала, которые были перенесены.

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a>Разрешение

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Рассматриваются сущности и API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание ресурсов для миграции в Microsoft Teams.|**Только для приложений**|**Да**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Запрос (создание команды в состоянии миграции)

```http
POST https://graph.microsoft.com/v1.0/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a>Сообщение об ошибке

```http
400 Bad Request
```

Сообщение об ошибке можно получить в следующих сценариях:

* Если `createdDateTime` задано на будущее.
* Если `createdDateTime` указан правильно, но атрибут `teamCreationMode` экземпляра отсутствует или задано недопустимое значение.

## <a name="step-2-create-a-channel"></a>Шаг 2. Создание канала

Создание канала для импортированных сообщений аналогично сценарию создания команды:

> [Создайте новый канал](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) со временной меткой back-in-time с помощью свойства ресурса `createdDateTime` канала. Поместите новый канал в `migration mode`специальное состояние, которое ограничивает пользователей от большинства действий чата в канале до завершения процесса миграции. Включите `channelCreationMode` атрибут экземпляра со значением `migration` в запрос POST, чтобы явно идентифицировать новую команду как созданную для миграции.  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a>Разрешение

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Рассматриваются сущности и API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание ресурсов для миграции в Microsoft Teams.|**Только для приложений**|**Да**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Запрос (создание канала в состоянии миграции)

```http
POST https://graph.microsoft.com/v1.0/teams/{team-id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels/$entity",
   "id":"id-value",
   "createdDateTime":null,
   "displayName":"Architecture Discussion",
   "description":"This channel is where we debate all future architecture plans",
   "isFavoriteByDefault":null,
   "email":null,
   "webUrl":null,
   "membershipType":null,
   "moderationSettings":null
}
```

#### <a name="error-message"></a>Сообщение об ошибке

```http
400 Bad Request
```

Сообщение об ошибке можно получить в следующих сценариях:

* Если `createdDateTime` задано на будущее.
* Если `createdDateTime` указан правильно, но атрибут `channelCreationMode` экземпляра отсутствует или задано недопустимое значение.

## <a name="step-3-import-messages"></a>Шаг 3. Импорт сообщений

После создания команды и канала `createdDateTime` `from` можно начать отправку сообщений во времени с помощью ключей и ключей в тексте запроса.

> [!NOTE]
>
> * Сообщения, импортированные раньше `createdDateTime` потока `createdDateTime` сообщений, не поддерживаются.
> * `createdDateTime` должен быть уникальным для сообщений в одном потоке.
> * `createdDateTime` поддерживает метки времени с точностью в миллисекундах. Например, `createdDateTime` если входящее сообщение запроса имеет значение *2020-09-16T05:50:31.0025302Z*, то оно будет преобразовано в *2020-09-16T05:50:31.002Z* при приеме сообщения.

#### <a name="request-post-message-that-is-text-only"></a>Запрос (сообщение POST, доступное только для текста)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

{
   "createdDateTime":"2019-02-04T19:58:15.511Z",
   "from":{
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   }
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
   "id":"id-value",
   "replyToId":null,
   "etag":"id-value",
   "messageType":"message",
   "createdDateTime":"2019-02-04T19:58:15.58Z",
   "lastModifiedDateTime":null,
   "deleted":false,
   "subject":null,
   "summary":null,
   "importance":"normal",
   "locale":"en-us",
   "policyViolation":null,
   "from":{
      "application":null,
      "device":null,
      "conversation":null,
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   },
   "attachments":[
   ],
   "mentions":[
   ],
   "reactions":[
   ]
}
```

#### <a name="error-message"></a>Сообщение об ошибке

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Запрос (POST-сообщение со встроенным изображением)

> [!NOTE]
>
> * В этом сценарии нет специальных областей разрешений, так как запрос является частью `chatMessage`.
> * Области, применяемые `chatMessage` здесь.

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

{
  "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"../hostedContents/1/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "hostedContents":[
        {
            "@microsoft.graph.temporaryId": "1",
            "contentBytes": "iVBORw0KGgoAAAANSUhEUgAAANcAAAExCAYAAADvFzeeAAAXjklEQVR4Ae2d/XNU1RnH+9e0FFrA0RCIyaS8hRA0HV5KbS1gHRgVpjMClY4GHJ3yYm1HCmXaWttaaZUZtIIFKYi8lFAkvOQ9u5vN225IARVBbX9/Os9NbrLZbMjmhCfJPX5+2Lmb3T25y3O+n/M599x7w9f+++UXwoMakIF7n4GvUdR7X1RqSk01A8CFuZm5GGUAuIwKi72wF3ABF+YyygBwGRUWc2Eu4AIuzGWUAeAyKizmwlzABVyYyygDwGVUWMyFuYALuDCXUQaAy6iwmAtzARdwfWXMdeuzT+TGxz3Sfb1LunrapL07IW3pePDQ5/qavqef0c+OdYAELuAac4jGGkLL9rdvfyo9N9ODQAqBGmmrwGlb/R0u3xG4gMspOC5hG882CoRaaCSA8n1ff9doIQMu4PIOrus3u+8ZVNnw6e/Od5AALuDKOyz5hmqiPnfnzi1J9bSbgRWCpvvQfY307wQu4BoxJCOFaDK8rwsQmQsUIQhWW93XSIsewAVckYdLQ24F0Ui/926AARdwRRounZ6Np7GyYdN9DzdFBC7gijRc43GMlQ1U9s/6HXJNjYELuHI<<-----Removed----->>>>",
            "contentType": "image/png"
        }
    ]
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
    "id": "id-value",
    "replyToId": null,
    "etag": "id-value",
    "messageType": "message",
    "createdDateTime": "2019-02-04T19:58:15.511Z",
    "lastModifiedDateTime": null,
    "deleted": false,
    "subject": null,
    "summary": null,
    "importance": "normal",
    "locale": "en-us",
    "policyViolation": null,
    "from": {
        "application": null,
        "device": null,
        "conversation": null,
        "user": {
            "id": "id-value",
            "displayName": "Joh Doe",
            "userIdentityType": "aadUser"
        }
    },
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-4-complete-migration-mode"></a>Шаг 4. Полный режим миграции

После завершения процесса переноса сообщений команда и канал выйдите из режима миграции с помощью этого  `completeMigration` метода. Этот шаг открывает ресурсы команды и канала для общего использования участниками команды. Действие привязано к экземпляру `team` . Прежде чем команда завершит работу, все каналы должны быть завершены из режима миграции.

#### <a name="request-end-channel-migration-mode"></a>Запрос (режим миграции конечного канала)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>Запрос (режим миграции конечной команды)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

Действие, вызывающееся для `team` или `channel` которое отсутствует в `migrationMode`.

## <a name="step-five-add-team-members"></a>Шаг 5. Добавление участников команды

Вы можете добавить участника в команду с помощью [](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Teams пользовательского интерфейса или Microsoft Graph [API-интерфейса](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true).

#### <a name="request-add-member"></a>Запрос (добавление участника)

```http
POST https://graph.microsoft.com/beta/teams/{team-id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>Советы и дополнительные сведения

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* После выполнения `completeMigration` запроса вы не сможете импортировать дополнительные сообщения в команду.

* Добавлять участников команды в новую команду можно только `completeMigration` после того, как запрос возвратит успешный ответ.

* Регулирование: импорт сообщений с пятью RPS на канал.

* Если необходимо внести исправление в результаты миграции, необходимо удалить команду и повторить действия, чтобы создать команду и канал и повторно перенести сообщения.

> [!NOTE]
> В настоящее время встроенные изображения являются единственным типом мультимедиа, поддерживаемым схемой API импорта сообщений.

##### <a name="import-content-scope"></a>Импорт области содержимого

В следующей таблице представлена область содержимого:

|В области | В настоящее время вне области|
|----------|--------------------------|
|Сообщения команды и канала|1:1 и групповые сообщения чата|
|Время создания исходного сообщения|Частные каналы|
|Встроенные изображения как часть сообщения|При упоминаний|
|Ссылки на существующие файлы в SPO или OneDrive|Реакции|
|Сообщения с форматированным текстом|Видео|
|Цепочка ответов сообщений|Объявления|
|Обработка с высокой пропускной способностью|Фрагменты кода|
||Наклейки|
||Смайлики|
||Цитаты|
||Перекрестные публикации между каналами|
||Общие каналы|

## <a name="see-also"></a>См. также

[Интеграция Graph и Teams Майкрософт](/graph/teams-concept-overview)
