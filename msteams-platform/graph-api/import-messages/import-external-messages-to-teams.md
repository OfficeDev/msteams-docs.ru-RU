---
title: Импорт сообщений внешней платформы в Teams с помощью Microsoft Graph
description: Описано, как использовать Microsoft Graph для импорта сообщений из внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Граф api для сообщений teams slack graph, microsoft migration post
ms.openlocfilehash: 8e8b21c9a38570d7ede745e27b9316b7aba29956
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46820372"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Импорт сообщений сторонних производителей в Teams с помощью Microsoft Graph

>[!IMPORTANT]
> Для раннего доступа и получения отзывов доступны общедоступные предварительные версии Microsoft Graph и Microsoft Teams. Хотя в этом выпуске прошло обширное тестирование, он не предназначен для использования в рабочей среде.

С помощью Microsoft Graph вы можете перенести существующие историю сообщений и данные из внешней системы в канал Teams. Включив иерархию сторонних служб сообщений в Teams, пользователи могут беспрепятственно и дальше идти без прерывания.

## <a name="import-overview"></a>Общие сведения об импорте

На высоком уровне процесс импорта состоит из следующих элементов.

1. [Создание команды с отметкой времени в дуйме времени](#step-one-create-a-team)
1. [Создание канала с отметкой времени возврата](#step-two-create-a-channel)  
1. [Импорт внешних сообщений с датой возврата времени](#step-three-import-messages)
1. [Завершение процесса миграции команд и каналов](#step-four-complete-migration-mode)
1. [Добавление участников команды](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Необходимые требования

### <a name="analyze-and-prepare-message-data"></a>Анализ и подготовка данных сообщения

✔ сведения о сторонних данных и решите, что именно нужно перенести.  
✔ данных из системы сторонних чатов.  
✔ преобразуйте данные импорта в формат, необходимый для миграции.  
✔ Сопоставить структуру сторонних чатов со структурой Teams.

### <a name="set-up-your-office-365-tenant"></a>Настройка клиента Office 365

✔ убедиться, что клиент Office 365 существует для импорта данных. Дополнительные сведения о настройке клиента Office 365 для Teams см. в *статье*"Подготовка [клиента Office 365".](../../concepts/build-and-test/prepare-your-o365-tenant.md)  
✔ убедитесь, что участники команды находятся в службе Azure Active Directory (AAD).  Дополнительные сведения *см. в* [статье "Добавление нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure Active Directory".

## <a name="step-one-create-a-team"></a>Первый шаг. Создание команды

Поскольку переносятся существующие данные, сохранение отметок времени исходного сообщения и предотвращение действий по обмену сообщениями во время миграции ключ к воссозданию существующего потока сообщений пользователя в Teams. Это достигается следующим образом:

1. [Создание команды с меткой](/graph/api/team-post?view=graph-rest-beta&tabs=http) времени в ответ на запас времени с помощью свойства ресурса  `createdDateTime`  команды.  

1. Разместите новую команду `migration mode` в специальное состояние для отбрасывания большинства действий в команде до завершения процесса миграции. Включите атрибут `teamCreationMode` экземпляра со значением `migration` в запрос POST, чтобы явно определить новую команду как создаваемую для переноса.  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Разрешения

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Сущности и API включены|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание и управление ресурсами для переноса на Microsoft Teams|**Только приложение**|**Да**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Запрос (создание команды в состоянии миграции)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
  "createdDateTime": "2020-03-14T11:22:17.067Z"
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

* `createdDateTime`  задайте для будущего задание.
* `createdDateTime`  правильно определен, `teamCreationMode`  но атрибут экземпляра отсутствует или имеет недопустимое значение.

## <a name="step-two-create-a-channel"></a>Второй шаг. Создание канала

Создание канала для импортированных сообщений аналогично сценарию создания команды: 

1. [Создайте канал с меткой](/graph/api/channel-post?view=graph-rest-beta&tabs=http) времени с меткой времени во время выполнения с помощью свойства ресурса `createdDateTime` канала.

1. Разместите новый канал `migration mode` в специальное состояние для отбрасывания пользователей в большинстве действий чата в канале до завершения процесса миграции.  Включите атрибут `channelCreationMode` экземпляра со значением `migration` в запрос POST, чтобы явно определить новую команду как создаваемую для переноса.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Разрешения

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Сущности и API включены|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание и управление ресурсами для переноса на Microsoft Teams|**Только приложение**|**Да**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>Запрос (создание канала в состоянии миграции)

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a>Сообщение об ошибке

```http
400 Bad Request
```

* `createdDateTime`  задайте для будущего задание.
* `createdDateTime`  правильно `channelCreationMode`  указанный, но атрибут экземпляра отсутствует или имеет недопустимое значение.

## <a name="step-three-import-messages"></a>Шаг 3. Импорт сообщений

После создания команды и канала вы можете начать отправлять сообщения на задний длительное время с `createdDateTime`  помощью `from`  ключей и ключей в тексте запроса.

#### <a name="request-post-message-that-is-text-only"></a>Запрос (только сообщение POST)

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
    "replyToId": null,
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="request-post-a-message-with-inline-image"></a>Запрос (запрос POST с встроенным 'изображением)

> **Примечание.** В этом сценарии нет специальных областей разрешений, так как запрос входит в chatMessage; также применимы области для chatMessage.

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
    {
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a>Шаг 4. Завершение режима миграции

После завершения миграции сообщения команда и канал отводятся из режима миграции с помощью  `completeMigration`  этого метода. Это действие открывает ресурсы команд и каналов для общего использования участниками команды. Действие привязано к `team` экземпляру.

#### <a name="request-end-team-migration-mode"></a>Запрос (режим миграции конечной группы)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>Запрос (режим миграции в режиме завершения канала)

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

* Действие, вызываемое для `team` него `channel` или неявляющиеся. `migrationMode`

## <a name="step-five-add-team-members"></a>Шаг 5. Добавление участников команды

Вы можете добавить участника в команду с [помощью пользовательского интерфейса Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) или API добавления [участника в](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) Microsoft Graph:

#### <a name="request-add-member"></a>Запрос (добавление участника)

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>Советы и дополнительные сведения

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* Вы можете импортировать сообщения от пользователей, которые отсутствуют в Teams.

* После `completeMigration` создания запроса дальнейшие сообщения нельзя импортировать в команду.

* Участников команды можно добавлять в новую группу только после `completeMigration` того, как запрос вернет успешный ответ.

* Регулирование: импорт сообщений при 5 запросов в секунду на канал.

* Если вам нужно внести исправления в результаты миграции, то потребуется удалить команду и повторить шаги, чтобы создать команду, канал и перенести сообщения повторно.

> [!NOTE]
> В настоящее время встроенные изображения — это один тип носителя, поддерживаемый схемой API сообщений импорта.

##### <a name="import-content-scope"></a>Импорт области контента

|В достижении | В настоящее время не в области ставления|
|----------|--------------------------|
|Сообщения о командах и каналах|Индикансовая и групповые сообщения|
|Время создания исходного сообщения|Закрытые каналы|
|Встроенные изображения в состав сообщения.|В упоминаниях|
|Ссылки на существующие файлы в SPO/OneDrive|Реакции|
|Сообщения с форматированным текстом|Видео|
|Цепочка ответов на сообщения|Объявления|
|Высокая пропускная способность обработки|Фрагменты кода|
||Адаптивные карты|
||Стикеры|
||Emojis|
||Кавычки|
||Перекрестные публикации между каналами|

> [!div class="nextstepaction"]
>[Подробнее об интеграции Microsoft Graph и Teams](/graph/teams-concept-overview)
