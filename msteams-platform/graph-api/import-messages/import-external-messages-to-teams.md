---
title: Используйте microsoft Graph для импорта сообщений внешней платформы для Teams
description: Описывает, как использовать microsoft Graph для импорта сообщений с внешней платформы для Teams
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: группы импортируют сообщения api graph Microsoft migrate migration post
ms.openlocfilehash: ad4e494264a72a3fdb1d926323bc2878d10cf44d
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069136"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph

С помощью microsoft Graph можно перенести существующую историю сообщений и данные пользователей из внешней системы в Teams канал. Включив воссоздание иерархии обмена сообщениями сторонних платформ внутри Teams, пользователи могут беспрепятственно продолжать общение и действовать без прерывания.

> [!NOTE] 
> В дальнейшем корпорация Майкрософт может потребовать у вас или ваших клиентов оплаты дополнительных сборов на основе количества импортированных данных.

## <a name="import-overview"></a>Обзор импорта

На высоком уровне процесс импорта состоит из следующих:

1. [Создание команды с помощью back-in-time timestamp](#step-one-create-a-team)
1. [Создание канала с помощью back-in-timestamp](#step-two-create-a-channel) 
1. [Импорт внешних датируемых сообщений в обратном времени](#step-three-import-messages)
1. [Завершение процесса миграции группы и канала](#step-four-complete-migration-mode)
1. [Добавление членов группы](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Необходимые требования

### <a name="analyze-and-prepare-message-data"></a>Анализ и подготовка данных сообщений

✔ просмотрите сторонние данные, чтобы определить, что будет перенесено.  
✔ извлекать выбранные данные из системы сторонних чатов.  
✔ на карте сторонние структуры чата в Teams структуру.  
✔ импорт данных в формат, необходимый для миграции.  

### <a name="set-up-your-office-365-tenant"></a>Настройка клиента Office 365

✔ убедитесь, что Office 365 клиент существует для данных импорта. Дополнительные сведения о настройке Office 365 аренды для Teams см. в Office 365 [клиента.](../../concepts/build-and-test/prepare-your-o365-tenant.md)  
✔ убедитесь, что члены группы находятся в Azure Active Directory (AAD).  Дополнительные сведения см. в [добавлении нового](/azure/active-directory/fundamentals/add-users-azure-active-directory) пользователя к Azure Active Directory.

## <a name="step-one-create-a-team"></a>Шаг первый: создание команды

Так как существующие данные переносят, сохранение исходных периодов времени отправки сообщений и предотвращение активности обмена сообщениями в процессе миграции являются ключом к воссозданию существующего потока сообщений пользователя в Teams. Это достигается следующим образом:

> [Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) со временем, используя свойство ресурсов  `createdDateTime`  группы. Поместите новую команду в специальное состояние, которое не позволяет пользователям выполнить большинство действий в команде до завершения процесса `migration mode` миграции. Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `teamCreationMode` `migration` как созданную для миграции.  

> [!Note]
> Поле будет заполнено только для экземпляров команды или канала, которые `createdDateTime` были перенесены.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Разрешения

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Объекты/API, охваченные|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание, управление ресурсами для миграции в Microsoft Teams.|**Только для приложений**|**Да**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>Запрос (создание группы в состоянии миграции)

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

#### <a name="error-messages"></a>Сообщения об ошибках

```http
400 Bad Request
```

* `createdDateTime`  установлено на будущее.
* `createdDateTime`  правильно задан, но `teamCreationMode`  атрибут экземпляра отсутствует или задан для значения недействительным.

## <a name="step-two-create-a-channel"></a>Шаг второй: создание канала

Создание канала для импортируемых сообщений аналогично сценарию создания группы:

> [Создайте новый канал](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) с использованием свойства ресурса канала с помощью функции timestamp в обратном `createdDateTime` времени. Поместите новый канал в специальное состояние, которое не позволяет пользователям от большинства действий чата в канале до завершения процесса `migration mode` миграции.  Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `channelCreationMode` `migration` как созданную для миграции.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Разрешения

|ScopeName|DisplayName|Описание|Тип|Согласие администратора?|Объекты/API, охваченные|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|Управление миграцией в Microsoft Teams|Создание, управление ресурсами для миграции в Microsoft Teams.|**Только для приложений**|**Да**|`POST /teams`|

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

* `createdDateTime`  установлено на будущее.
* `createdDateTime`  правильно задан, но `channelCreationMode`  атрибут экземпляра отсутствует или задан для значения недействительным.

## <a name="step-three-import-messages"></a>Шаг 3. Импорт сообщений

После создания группы и канала можно приступить к отправке сообщений в обратном времени с помощью ключей и ключей в `createdDateTime` `from`  тексте запроса. **ПРИМЕЧАНИЕ.** Сообщения, импортируемые с более ранним `createdDateTime` потоком `createdDateTime` сообщений, не поддерживаются.

> [!NOTE]
> * `createdDateTime` должны быть уникальными для сообщений в одном потоке.
> * `createdDateTime` поддерживает периоды времени с точностью миллисекунд. Например, если входящий запрос сообщения имеет значение set `createdDateTime` as *2020-09-16T05:50:31.0025302Z,* то оно будет преобразовано в *2020-09-16T05:50:31.002Z,* когда сообщение будет ingested.

#### <a name="request-post-message-that-is-text-only"></a>Запрос (сообщение POST, которое является текстовым)

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

#### <a name="error-messages"></a>Сообщения об ошибках

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>Запрос (СООБЩЕНИЕ сообщения с inline image)

> [!Note]
> В этом сценарии нет специальных областей разрешений, так как запрос является частью chatMessage; Области для chatMessage применяются и здесь.

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

## <a name="step-four-complete-migration-mode"></a>Шаг 4. Полный режим миграции

После завершения процесса миграции сообщений команда и канал вывели из режима миграции с помощью  `completeMigration`  метода. Этот шаг открывает ресурсы команды и канала для общего использования членами группы. Действие привязано к `team` экземпляру. Все каналы должны быть завершены из режима миграции, прежде чем команда может быть завершена.

#### <a name="request-end-channel-migration-mode"></a>Запрос (режим переноса конечных каналов)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>Запрос (режим миграции конечных команд)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

* Действие, которое `team` вызвано или `channel` которое не в `migrationMode` .

## <a name="step-five-add-team-members"></a>Шаг 5. Добавление членов группы

Можно добавить участника в команду с помощью [пользовательского интерфейса Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Microsoft Graph [API](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) участника:

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

* После запроса нельзя импортировать дополнительные сообщения `completeMigration` в команду.

* Члены группы могут быть добавлены в новую команду только после успешного ответа на `completeMigration` запрос.

* Регулирование: импорт сообщений по 5 RPS на канал.

* Если необходимо внести исправление в результаты миграции, необходимо удалить команду и повторить действия по созданию группы и каналу и повторной миграции сообщений.

> [!NOTE]
> В настоящее время inline images are the only type of media supported by the import message API schpi.

##### <a name="import-content-scope"></a>Область импорта контента

|В области | В настоящее время вне области|
|----------|--------------------------|
|Сообщения группы и канала|1:1 и групповые сообщения чата|
|Созданное время исходного сообщения|Частные каналы|
|Inline images as part of the message|При упоминаний|
|Ссылки на существующие файлы в SPO/OneDrive|Реакции|
|Сообщения с богатым текстом|Видео|
|Цепочка ответов на сообщения|Объявления|
|Обработка высокой пропускной способности|Фрагменты кода|
||Наклейки|
||Emojis|
||Цитаты|
||Перекрестные сообщения между каналами|


## <a name="see-also"></a>Дополнительные материалы

[Узнайте больше об интеграции Graph и Teams Майкрософт](/graph/teams-concept-overview)
