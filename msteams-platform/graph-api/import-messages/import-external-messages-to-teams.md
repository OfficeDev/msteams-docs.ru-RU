---
title: Используйте Microsoft Graph для импорта внешних сообщений платформы для Teams
description: Описывает, как использовать microsoft Graph для импорта сообщений с внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: команды импортируют сообщения api график Microsoft мигрировать миграции пост
ms.openlocfilehash: 5ea06e8b490bae0595abb31086848d0b050bded0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566161"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph

С помощью Graph Microsoft можно перенести существующую историю сообщений пользователей и данные из внешней системы в Teams канал. Позволяя воссоздать иерархию сторонних платформ обмена сообщениями внутри Teams, пользователи могут продолжать свои коммуникации бесшовно и действовать без перерыва.

> [!NOTE] 
> В дальнейшем корпорация Майкрософт может потребовать у вас или ваших клиентов оплаты дополнительных сборов на основе количества импортированных данных.

## <a name="import-overview"></a>Обзор импорта

На высоком уровне процесс импорта состоит из следующих:

1. [Создайте команду с резервной во времени тайм-штамп](#step-one-create-a-team)
1. [Создание канала с резервной во времени тайм-штамп](#step-two-create-a-channel) 
1. [Импорт внешних устаревших сообщений](#step-three-import-messages)
1. [Завершить процесс миграции команды и канала](#step-four-complete-migration-mode)
1. [Добавление членов команды](#step-five-add-team-members)

## <a name="necessary-requirements"></a>Необходимые требования

### <a name="analyze-and-prepare-message-data"></a>Анализ и подготовка данных сообщений

✔ данные третьей стороны, чтобы решить, что будет перенесено.  
✔ извлекаем выбранные данные из сторонняя система чата.  
✔ Карта сторонняя структура чата в Teams структуры.  
✔ преобразования данных импорта в формат, необходимый для миграции.  

### <a name="set-up-your-office-365-tenant"></a>Настройка клиента Office 365

✔, что Office 365 арендатора существует для данных об импорте. Для получения дополнительной информации о настройке Office 365 аренды для Teams, [см Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md)  
✔ убедитесь, что члены команды находятся Azure Active Directory (AAD).  Для получения дополнительной информации [см Azure Active Directory.](/azure/active-directory/fundamentals/add-users-azure-active-directory)

## <a name="step-one-create-a-team"></a>Шаг первый: Создайте команду

Поскольку существующие данные мигрируют, поддержание исходных времен сообщения и предотвращение активности обмена сообщениями в процессе миграции являются ключом к воссозданию существующего потока сообщений пользователя в Teams. Это достигается следующим образом:

> [Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) с резервной во времени timestamp с использованием свойства ресурсов  `createdDateTime`  команды. Поместите новую команду `migration mode` в специальное состояние, которое запрещает пользователям большинство действий в команде до завершения процесса миграции. Включите атрибут `teamCreationMode` экземпляра со `migration` значением в запрос POST, чтобы явно определить новую группу как созданную для миграции.  

> [!Note]
> Поле `createdDateTime` будет заполнено только для экземпляров группы или канала, которые были перенесены.

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>Разрешения

|ОбластьИмя|DisplayName|Описание|Тип|Согласие администратора?|Объекты/API, охватываемые|
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

* `createdDateTime`  набор для будущего.
* `createdDateTime`  правильно указано, но атрибут `teamCreationMode`  экземпляра отсутствует или устанавливается на недействительное значение.

## <a name="step-two-create-a-channel"></a>Шаг первый: Создание канала

Создание канала для импортированных сообщений аналогично сценарию группы создания:

> [Создайте новый канал](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) с резервной во времени timestamp с использованием свойства ресурса `createdDateTime` канала. Поместите новый канал в `migration mode` специальное состояние, которое запрещает пользователям большинство действий чата в канале до завершения процесса миграции.  Включите атрибут `channelCreationMode` экземпляра со `migration` значением в запрос POST, чтобы явно определить новую группу как созданную для миграции.  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>Разрешения

|ОбластьИмя|DisplayName|Описание|Тип|Согласие администратора?|Объекты/API, охватываемые|
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

* `createdDateTime`  набор для будущего.
* `createdDateTime`  правильно указанный, но атрибут `channelCreationMode`  экземпляра отсутствует или устанавливается на недействительное значение.

## <a name="step-three-import-messages"></a>Шаг третий: Импортные сообщения

После создания команды и канала можно начать отправлять сообщения, которые отправляются с помощью `createdDateTime`  ключей `from`  и ключей в корпусе запроса. **ПРИМЕЧАНИЕ**: сообщения, импортированные `createdDateTime` раньше, чем поток `createdDateTime` сообщений, не поддерживаются.

> [!NOTE]
> * `createdDateTime` должны быть уникальными в сообщениях в одном потоке.
> * `createdDateTime` поддерживает время метки с точностью миллисекунд. Например, если входящее сообщение запроса `createdDateTime` имеет значение набора как *2020-09-16T05:50:31.0025302*, то оно будет преобразовано *в 2020-09-16T05:50:31.002* , когда сообщение попадает.

#### <a name="request-post-message-that-is-text-only"></a>Запрос (POST сообщение, которое является текстовым)

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

#### <a name="request-post-a-message-with-inline-image"></a>Запрос (POST сообщение с изображением в ряд)

> [!Note]
> В этом сценарии нет специальных областей разрешений, так как запрос является частью chatMessage; области для chatMessage применяются и здесь.

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

## <a name="step-four-complete-migration-mode"></a>Шаг четвертый: Полный режим миграции

После завершения процесса миграции сообщений команда и канал выходят из режима миграции с помощью  `completeMigration`  метода. Этот шаг открывает ресурсы команды и канала для общего использования членами команды. Действие привязано к `team` экземпляру. Все каналы должны быть завершены из режима миграции, прежде чем команда может быть завершена.

#### <a name="request-end-channel-migration-mode"></a>Запрос (режим миграции конца канала)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>Запрос (режим миграции команды)

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>Отклик

```http
HTTP/1.1 204 NoContent
```

* Действия, называемые `team` или которые не в `channel` `migrationMode` .

## <a name="step-five-add-team-members"></a>Шаг пятый: Добавить членов команды

Вы можете добавить члена в группу, [используя пользовательский Teams или](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Microsoft Graph [Добавить API-участника:](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)

#### <a name="request-add-member"></a>Запрос (добавить участника)

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

## <a name="tips-and-additional-information"></a>Советы и дополнительная информация

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* После `completeMigration` того, как запрос сделан, вы не можете импортировать дополнительные сообщения в группу.

* Члены группы могут быть добавлены в новую группу только после `completeMigration` того, как запрос получил успешный ответ.

* Регулирование: Сообщения импортируются по 5 RPS за канал.

* Если необходимо внести коррективы в результаты миграции, необходимо удалить группу и повторить шаги по созданию команды и канала и повторной миграции сообщений.

> [!NOTE]
> В настоящее время вкошенные изображения являются единственным типом средств массовой информации, поддерживаемых схемой API сообщений импорта.

##### <a name="import-content-scope"></a>Область импортного контента

|В сфере охвата | В настоящее время вне сферы охвата|
|----------|--------------------------|
|Сообщения команд и каналов|1:1 и групповые сообщения чата|
|Создано время исходного сообщения|Частные каналы|
|Вколинные изображения как часть сообщения|При упоминаниях|
|Ссылки на существующие файлы в SPO/OneDrive|Реакции|
|Сообщения с богатым текстом|Видео|
|Цепочка ответов на сообщения|Объявления|
|Высокая пропускная способность|Фрагменты кода|
||Наклейки|
||Эмодзи|
||Цитаты|
||Кросс-посты между каналами|


## <a name="see-also"></a>См. также

[Узнайте больше об интеграции Graph и Teams Майкрософт](/graph/teams-concept-overview)
