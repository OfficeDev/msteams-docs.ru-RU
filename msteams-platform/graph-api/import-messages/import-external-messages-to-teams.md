---
title: Импорт сообщений о внешних платформах в Teams с помощью Microsoft Graph
description: В этой статье описывается, как использовать Microsoft Graph для импорта сообщений из внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Microsoft Teams Import messages API Graph перенесите запись миграции
ms.openlocfilehash: 0f53e27ec849e18be49f233a754658587343f68b
ms.sourcegitcommit: 25afe104d10c9a6a2849decf5ec1d08969d827c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2020
ms.locfileid: "48465910"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph

>[!IMPORTANT]
> Microsoft Graph и общедоступные предварительные обзоры Microsoft Teams доступны для раннего доступа и обратной связи. Несмотря на то что этот выпуск протестировался, он не предназначен для использования в рабочей среде.

С помощью Microsoft Graph вы можете перенести в канал Teams существующую историю сообщений и данные пользователей из внешней системы. Благодаря повторному воссозданию иерархической структуры обмена сообщениями платформы в Teams пользователи могут беспрепятственно продолжить их работу и продолжить работу без перерывов.

## <a name="import-overview"></a>Обзор импорта

На высоком уровне процесс импорта состоит из следующих элементов:

1. [Создание команды с отметкой времени обратного входа](#step-one-create-a-team)
1. [Создание канала с обратной меткой времени](#step-two-create-a-channel)  
1. [Импорт внешних сообщений с обратной датой после времени](#step-three-import-messages)
1. [Выполнение процесса миграции группы и канала](#step-four-complete-migration-mode)
1. [Добавление участников группы](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Необходимые требования

### <a name="analyze-and-prepare-message-data"></a>Анализ и подготовка данных сообщения

✔ Проанализируйте сторонние данные, чтобы определить, что будет перенесено.  
✔ Извлечения выбранных данных из сторонней системы чата.  
✔ Сопоставить структуру чата сторонним разработчикам со структурой Teams.  
✔ Преобразовать данные импорта в формат, необходимый для миграции.  

### <a name="set-up-your-office-365-tenant"></a>Настройка клиента Office 365

✔ Убедиться, что клиент Office 365 существует для импорта данных. Для получения дополнительных сведений о настройке Office 365 для Teams, *Ознакомьтесь*со статьей [подготовка клиента Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).  
✔ Убедитесь, что участники группы находятся в Azure Active Directory (AAD).  Дополнительные сведения *см* . в статье [Добавление нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure Active Directory.

## <a name="step-one-create-a-team"></a>Шаг 1: создание группы

Так как существующие данные переносятся, поддержание исходных меток времени и предотвращение активности сообщений в процессе миграции является ключом к повторному созданию существующего процесса обработки сообщений пользователя в Teams. Это достигается следующим образом:

> [Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) с обратной меткой времени, используя свойство ресурса Team  `createdDateTime`  . Поместите новую команду в `migration mode` специальное состояние, которое откладывает пользователей от большинства действий в группе до завершения процесса миграции. Добавьте `teamCreationMode` атрибут экземпляра со `migration` значением в запросе POST, чтобы явным образом определить новую команду в качестве ее создания для миграции.  

> **Note**: `createdDateTime` поле будет заполнено только для тех экземпляров группы или канала, которые были перенесены.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Разрешения

|скопенаме|DisplayName|Описание|Тип|Согласие администратора?|Покрываемые сущности и API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание и управление ресурсами для переноса в Microsoft Teams|**Только для приложений**|**Да**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Запрос (создание команды в состоянии миграции)

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
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

* `createdDateTime`  задается для будущего.
* `createdDateTime`  указано правильно, но `teamCreationMode`  атрибут экземпляра отсутствует или имеет недопустимое значение.

## <a name="step-two-create-a-channel"></a>Шаг 2: создание канала

Создание канала для импортированных сообщений похоже на сценарий создания группы:

> [Создайте новый канал](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) с обратной меткой времени, используя свойство Resource Channel `createdDateTime` . Поместите новый канал в `migration mode` особое состояние, которое откладывает пользователей от большинства действий чата в канал до завершения процесса миграции.  Добавьте `channelCreationMode` атрибут экземпляра со `migration` значением в запросе POST, чтобы явным образом определить новую команду в качестве ее создания для миграции.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Разрешения

|скопенаме|DisplayName|Описание|Тип|Согласие администратора?|Покрываемые сущности и API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание и управление ресурсами для переноса в Microsoft Teams|**Только для приложений**|**Да**|`POST /teams`|

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

#### Error message

```http
400 Bad Request
```

* `createdDateTime`  задается для будущего.
* `createdDateTime`  указано правильно, но `channelCreationMode`  атрибут экземпляра отсутствует или задано недопустимое значение.

## <a name="step-three-import-messages"></a>Этап 3: Импорт сообщений

После создания группы и канала можно начать отправку сообщений в обратном времени, используя `createdDateTime` `from`  ключи и в теле запроса. **Note**: сообщения, импортированные `createdDateTime` раньше, чем цепочка сообщений `createdDateTime` , не поддерживаются.

> [!NOTE]
> createdDateTime должны быть уникальными для всех сообщений в одном потоке.

#### <a name="request-post-message-that-is-text-only"></a>Request (сообщение POST, которое является текстовым)

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

#### <a name="request-post-a-message-with-inline-image"></a>Запрос (публикация сообщения с встроенным изображением)

> **Note**: в этом сценарии нет особых областей разрешений, так как запрос является частью chatMessage; Здесь также применяются области для chatMessage.

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

## <a name="step-four-complete-migration-mode"></a>Шаг 4: завершение режима миграции

После завершения процесса переноса сообщений команда и канал из режима миграции берутся из режима миграции с помощью  `completeMigration`  метода. На этом этапе открываются ресурсы команды и канала для общего использования участниками группы. Действие привязано к `team` экземпляру.

#### <a name="request-end-team-migration-mode"></a>Запрос (режим миграции команды End)

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>Запрос (режим миграции конечного канала)

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

* Действие вызвано для объекта a `team` или `channel` не в `migrationMode` .

## <a name="step-five-add-team-members"></a>Шаг 5: Добавление участников группы

Добавить участника в команду можно [с помощью пользовательского интерфейса](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Teams или API [добавления элементов](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft Graph:

#### <a name="request-add-member"></a>Запрос (Добавление члена)

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

* Вы можете импортировать сообщения от пользователей, не включенных в Teams. **Note**: сообщения, импортированные для пользователей, отсутствующих в клиенте, не будут поддерживать поиск в клиенте Teams или порталах соответствия требованиям во время общедоступной предварительной версии.

* Когда `completeMigration` запрос будет выполнен, вы не сможете импортировать дальнейшие сообщения в команду.

* Участники группы могут быть добавлены в новую группу только после того, как `completeMigration` запрос вернул успешный ответ.

* Регулирование: сообщения импортируются по 5 RPS на канал.

* Если необходимо внести исправления в результаты миграции, необходимо удалить команду и повторить действия, чтобы создать группу и канал и повторно перенести сообщения.

> [!NOTE]
> В настоящее время встроенными образами является единственный тип мультимедиа, поддерживаемый схемой API импорта сообщений.

##### <a name="import-content-scope"></a>Область импорта контента

|В области | На данный момент вне области|
|----------|--------------------------|
|Сообщения группы и канала|1:1 и сообщения группового чата|
|Время создания исходного сообщения|Закрытые каналы|
|Встроенные изображения в составе сообщения|С упоминаниями|
|Ссылки на существующие файлы в SPO и OneDrive|Реакция|
|Сообщения с форматированным текстом|Видео|
|Цепочка ответов на сообщения|Объявления|
|Обработка высокой пропускной способности|Фрагменты кода|
||Адаптивные карты|
||Наклейки|
||Эмодзи|
||Quote|
||Перекрестные публикации между каналами|

> [!div class="nextstepaction"]
>[Дополнительные сведения о интеграции Microsoft Graph и Teams](/graph/teams-concept-overview)
