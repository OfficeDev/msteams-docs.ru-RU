---
title: Импорт сообщений внешней платформы в Teams с помощью Microsoft Graph
description: Описание использования Microsoft Graph для импорта сообщений с внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams import messages api graph microsoft migrate migration post
ms.openlocfilehash: 97f24c34ebb825aad0fd104c9a814e46f9b5fa0d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093262"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph

>[!IMPORTANT]
> Общедоступные предварительные версии Microsoft Graph и Microsoft Teams доступны для раннего доступа и отзывов. Хотя этот выпуск прошел тщательное тестирование, он не предназначен для использования в производственной версии.

С помощью Microsoft Graph вы можете перенести существующую историю сообщений и данные пользователей из внешней системы в канал Teams. Обеспечивая воссоздание иерархии обмена сообщениями на стороне платформы в Teams, пользователи могут бесперебойно продолжать общение и продолжать работу без перерывов.

## <a name="import-overview"></a>Обзор импорта

На высоком уровне процесс импорта состоит из следующих процессов:

1. [Создание команды с помощью запапамя времени](#step-one-create-a-team)
1. [Создание канала с помощью запамяканного времени](#step-two-create-a-channel)  
1. [Импорт внешних отсвещенных назад сообщений](#step-three-import-messages)
1. [Завершение процесса миграции команды и канала](#step-four-complete-migration-mode)
1. [Добавление участников команды](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Необходимые требования

### <a name="analyze-and-prepare-message-data"></a>Анализ и подготовка данных сообщений

✔ просмотрите сторонние данные, чтобы решить, что будет перенесено.  
✔ извлечь выбранные данные из стороной системы чата.  
✔ со структурой чата сторонних сторон со структурой Teams.  
✔ импорт данных в формат, необходимый для миграции.  

### <a name="set-up-your-office-365-tenant"></a>Настройка клиента Office 365

✔ убедитесь, что клиент Office 365 существует для данных импорта. Дополнительные сведения о настройке клиента Office 365 для Teams см. в подготовьте клиент [Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md)   
✔ убедитесь, что участники группы находятся в Azure Active Directory (AAD).  Дополнительные сведения *см.* [в записи "Добавление нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure Active Directory".

## <a name="step-one-create-a-team"></a>Шаг 1. Создание команды

Так как существующие данные переносят, сохранение меток времени исходного сообщения и предотвращение активности обмена сообщениями во время миграции являются ключевым фактором для воссоздания существующего потока сообщений пользователя в Teams. Это достигается следующим образом:

> [Создайте новую команду со](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) временем с помощью свойства ресурса  `createdDateTime`  команды. Поместите новую команду в специальное состояние, которое не позволяет пользователям выполнить большинство действий в команде до завершения процесса `migration mode` миграции. Включив атрибут экземпляра со значением в запрос POST, чтобы явно определить новую команду как созданную `teamCreationMode` `migration` для миграции.  

> **ПРИМЕЧАНИЕ.** Поле будет заполнено только для перенесенных экземпляров команды или `createdDateTime` канала.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Разрешения

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Объекты и API, охватываемых|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание и управление ресурсами для миграции в Microsoft Teams|**Только для приложений**|**Да**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Запрос (создание команды в состоянии миграции)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a>Сообщения об ошибках

```http
400 Bad Request
```

* `createdDateTime`  настроено на будущее.
* `createdDateTime`  правильно указано, но атрибут `teamCreationMode`  экземпляра отсутствует или задан как недопустимое значение.

## <a name="step-two-create-a-channel"></a>Шаг 2. Создание канала

Создание канала для импортируемых сообщений аналогично сценарию создания команды:

> [Создайте новый канал](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) со временем с помощью свойства `createdDateTime` ресурса канала. Поместите новый канал в специальное состояние, которое не позволяет пользователям от большинства действий чата в канале до завершения `migration mode` процесса миграции.  Включив атрибут экземпляра со значением в запрос POST, чтобы явно определить новую команду как созданную `channelCreationMode` `migration` для миграции.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Разрешения

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Объекты и API, охватываемых|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание и управление ресурсами для миграции в Microsoft Teams|**Только для приложений**|**Да**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Запрос (создание канала в состоянии миграции)

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

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
   "@odata.context":"https://canary.graph.microsoft.com/testprodbetateamsgraphsvcncus/$metadata#teams('9cc6d6ab-07d8-4d14-bc2b-7db8995d6d23')/channels/$entity",
   "id":"19:e90f6814ce674072a4126206e7de485e@thread.tacv2",
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

* `createdDateTime`  настроено на будущее.
* `createdDateTime`  правильно указано, но `channelCreationMode`  атрибут экземпляра отсутствует или задан как недопустимое значение.

## <a name="step-three-import-messages"></a>Шаг 3. Импорт сообщений

После создания команды и канала можно приступить к отправке сообщений о времени с помощью ключей и ключей `createdDateTime` `from`  в тексте запроса. **ПРИМЕЧАНИЕ.** Сообщения, импортируемые раньше, `createdDateTime` чем поток сообщений, не `createdDateTime` поддерживаются.

> [!NOTE]
> * `createdDateTime` должно быть уникальным для всех сообщений в одном потоке.
> * `createdDateTime` поддерживает метки времени с точностью в миллисекунд. Например, если для входящих запросов за установлено значение `createdDateTime` *2020-09-16T05:50:31.0025302Z,* то оно будет преобразовано в *2020-09-16T05:50:31.002Z* при входящих сообщениях.

#### <a name="request-post-message-that-is-text-only"></a>Запрос (сообщение POST, которое является текстовым)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

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
   "@odata.context":"https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
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

#### <a name="error-messages"></a>Сообщения об ошибках

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Запрос (POST-сообщение со inline image)

> **Примечание.** В этом сценарии нет особых областей разрешений, так как запрос является частью chatMessage; области для chatMessage применяются и здесь.

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

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
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
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

## <a name="step-four-complete-migration-mode"></a>Шаг 4. Полный режим миграции

После завершения процесса переноса сообщений команда и канал вывели команду и канал из режима миграции с помощью  `completeMigration`  этого метода. Этот шаг открывает ресурсы команды и канала для общего использования участниками команды. Действие привязано к `team` экземпляру.

#### <a name="request-end-team-migration-mode"></a>Запрос (режим миграции команды)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>Запрос (режим переноса конечных каналов)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a>Отклик с ошибкой

```http
400 Bad Request
```

* Действие, которое вызвано `team` для действия, `channel` которое не находится в `migrationMode` .

## <a name="step-five-add-team-members"></a>Шаг 5. Добавление участников команды

Вы можете добавить участника в команду с помощью пользовательского интерфейса [Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) или API [добавления](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) членов Microsoft Graph:

#### <a name="request-add-member"></a>Запрос (добавление участника)

```http
POST https://graph.microsoft.com/beta/teams/{id}/members
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

* Вы можете импортировать сообщения от пользователей, которые не работают в Teams. **ПРИМЕЧАНИЕ.** Сообщения, импортируемые для пользователей, не присутствующих в клиенте, не будут искаться в клиенте Teams или на порталах соответствия требованиям во время открытой предварительной версии.

* После `completeMigration` запроса вы не сможете импортировать дополнительные сообщения в команду.

* Членов группы можно добавить в новую команду только после того, как запрос `completeMigration` возвратил успешный ответ.

* Регулирование: импорт сообщений при 5 запросах в секунду на канал.

* Если вам нужно внести изменения в результаты миграции, необходимо удалить команду и повторить действия, чтобы создать команду и канал и повторно перенести сообщения.

> [!NOTE]
> В настоящее время inline images are the only type of media supported by the import message API schema.

##### <a name="import-content-scope"></a>Импорт области контента

|Область действия | В настоящее время выходит за рамки области|
|----------|--------------------------|
|Сообщения о команде и канале|1:1 и сообщения группового чата|
|Время создания исходного сообщения|Частные каналы|
|Inline images as part of the message|При упоминаний|
|Ссылки на существующие файлы в SPO/OneDrive|Реакции|
|Сообщения с химким текстом|Видео|
|Цепочка ответов сообщений|Объявления|
|Обработка высокой пропускной способности|Фрагменты кода|
||Адаптивные карточки|
||Стикеры|
||Эмодзи|
||Кавычка|
||Перекрестные публикации между каналами|

> [!div class="nextstepaction"]
>[Узнайте больше об интеграции Microsoft Graph и Teams](/graph/teams-concept-overview)
