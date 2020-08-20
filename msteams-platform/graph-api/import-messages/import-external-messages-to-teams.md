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
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="a9ace-104">Импорт сообщений сторонних производителей в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a9ace-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="a9ace-105">Для раннего доступа и получения отзывов доступны общедоступные предварительные версии Microsoft Graph и Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="a9ace-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="a9ace-106">Хотя в этом выпуске прошло обширное тестирование, он не предназначен для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a9ace-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="a9ace-107">С помощью Microsoft Graph вы можете перенести существующие историю сообщений и данные из внешней системы в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="a9ace-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="a9ace-108">Включив иерархию сторонних служб сообщений в Teams, пользователи могут беспрепятственно и дальше идти без прерывания.</span><span class="sxs-lookup"><span data-stu-id="a9ace-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="a9ace-109">Общие сведения об импорте</span><span class="sxs-lookup"><span data-stu-id="a9ace-109">Import overview</span></span>

<span data-ttu-id="a9ace-110">На высоком уровне процесс импорта состоит из следующих элементов.</span><span class="sxs-lookup"><span data-stu-id="a9ace-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="a9ace-111">Создание команды с отметкой времени в дуйме времени</span><span class="sxs-lookup"><span data-stu-id="a9ace-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="a9ace-112">Создание канала с отметкой времени возврата</span><span class="sxs-lookup"><span data-stu-id="a9ace-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="a9ace-113">Импорт внешних сообщений с датой возврата времени</span><span class="sxs-lookup"><span data-stu-id="a9ace-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="a9ace-114">Завершение процесса миграции команд и каналов</span><span class="sxs-lookup"><span data-stu-id="a9ace-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="a9ace-115">Добавление участников команды</span><span class="sxs-lookup"><span data-stu-id="a9ace-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="a9ace-116">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="a9ace-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="a9ace-117">Анализ и подготовка данных сообщения</span><span class="sxs-lookup"><span data-stu-id="a9ace-117">Analyze and prepare message data</span></span>

<span data-ttu-id="a9ace-118">✔ сведения о сторонних данных и решите, что именно нужно перенести.</span><span class="sxs-lookup"><span data-stu-id="a9ace-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="a9ace-119">✔ данных из системы сторонних чатов.</span><span class="sxs-lookup"><span data-stu-id="a9ace-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="a9ace-120">✔ преобразуйте данные импорта в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="a9ace-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="a9ace-121">✔ Сопоставить структуру сторонних чатов со структурой Teams.</span><span class="sxs-lookup"><span data-stu-id="a9ace-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="a9ace-122">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="a9ace-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="a9ace-123">✔ убедиться, что клиент Office 365 существует для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="a9ace-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="a9ace-124">Дополнительные сведения о настройке клиента Office 365 для Teams см. в *статье*"Подготовка [клиента Office 365".](../../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="a9ace-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="a9ace-125">✔ убедитесь, что участники команды находятся в службе Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="a9ace-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="a9ace-126">Дополнительные сведения *см. в* [статье "Добавление нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="a9ace-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="a9ace-127">Первый шаг. Создание команды</span><span class="sxs-lookup"><span data-stu-id="a9ace-127">Step One: Create a team</span></span>

<span data-ttu-id="a9ace-128">Поскольку переносятся существующие данные, сохранение отметок времени исходного сообщения и предотвращение действий по обмену сообщениями во время миграции ключ к воссозданию существующего потока сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="a9ace-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="a9ace-129">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a9ace-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="a9ace-130">[Создание команды с меткой](/graph/api/team-post?view=graph-rest-beta&tabs=http) времени в ответ на запас времени с помощью свойства ресурса  `createdDateTime`  команды.</span><span class="sxs-lookup"><span data-stu-id="a9ace-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="a9ace-131">Разместите новую команду `migration mode` в специальное состояние для отбрасывания большинства действий в команде до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="a9ace-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="a9ace-132">Включите атрибут `teamCreationMode` экземпляра со значением `migration` в запрос POST, чтобы явно определить новую команду как создаваемую для переноса.</span><span class="sxs-lookup"><span data-stu-id="a9ace-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="a9ace-133">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a9ace-133">Permissions</span></span>

|<span data-ttu-id="a9ace-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="a9ace-134">ScopeName</span></span>|<span data-ttu-id="a9ace-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="a9ace-135">DisplayName</span></span>|<span data-ttu-id="a9ace-136">Описание</span><span class="sxs-lookup"><span data-stu-id="a9ace-136">Description</span></span>|<span data-ttu-id="a9ace-137">Тип</span><span class="sxs-lookup"><span data-stu-id="a9ace-137">Type</span></span>|<span data-ttu-id="a9ace-138">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="a9ace-138">Admin Consent?</span></span>|<span data-ttu-id="a9ace-139">Сущности и API включены</span><span class="sxs-lookup"><span data-stu-id="a9ace-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="a9ace-140">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a9ace-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="a9ace-141">Создание и управление ресурсами для переноса на Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a9ace-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="a9ace-142">**Только приложение**</span><span class="sxs-lookup"><span data-stu-id="a9ace-142">**Application-only**</span></span>|<span data-ttu-id="a9ace-143">**Да**</span><span class="sxs-lookup"><span data-stu-id="a9ace-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="a9ace-144">Запрос (создание команды в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="a9ace-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="a9ace-145">Отклик</span><span class="sxs-lookup"><span data-stu-id="a9ace-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="a9ace-146">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="a9ace-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="a9ace-147">`createdDateTime`  задайте для будущего задание.</span><span class="sxs-lookup"><span data-stu-id="a9ace-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="a9ace-148">`createdDateTime`  правильно определен, `teamCreationMode`  но атрибут экземпляра отсутствует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="a9ace-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="a9ace-149">Второй шаг. Создание канала</span><span class="sxs-lookup"><span data-stu-id="a9ace-149">Step Two: Create a channel</span></span>

<span data-ttu-id="a9ace-150">Создание канала для импортированных сообщений аналогично сценарию создания команды:</span><span class="sxs-lookup"><span data-stu-id="a9ace-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="a9ace-151">[Создайте канал с меткой](/graph/api/channel-post?view=graph-rest-beta&tabs=http) времени с меткой времени во время выполнения с помощью свойства ресурса `createdDateTime` канала.</span><span class="sxs-lookup"><span data-stu-id="a9ace-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="a9ace-152">Разместите новый канал `migration mode` в специальное состояние для отбрасывания пользователей в большинстве действий чата в канале до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="a9ace-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="a9ace-153">Включите атрибут `channelCreationMode` экземпляра со значением `migration` в запрос POST, чтобы явно определить новую команду как создаваемую для переноса.</span><span class="sxs-lookup"><span data-stu-id="a9ace-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="a9ace-154">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a9ace-154">Permissions</span></span>

|<span data-ttu-id="a9ace-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="a9ace-155">ScopeName</span></span>|<span data-ttu-id="a9ace-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="a9ace-156">DisplayName</span></span>|<span data-ttu-id="a9ace-157">Описание</span><span class="sxs-lookup"><span data-stu-id="a9ace-157">Description</span></span>|<span data-ttu-id="a9ace-158">Тип</span><span class="sxs-lookup"><span data-stu-id="a9ace-158">Type</span></span>|<span data-ttu-id="a9ace-159">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="a9ace-159">Admin Consent?</span></span>|<span data-ttu-id="a9ace-160">Сущности и API включены</span><span class="sxs-lookup"><span data-stu-id="a9ace-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="a9ace-161">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a9ace-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="a9ace-162">Создание и управление ресурсами для переноса на Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a9ace-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="a9ace-163">**Только приложение**</span><span class="sxs-lookup"><span data-stu-id="a9ace-163">**Application-only**</span></span>|<span data-ttu-id="a9ace-164">**Да**</span><span class="sxs-lookup"><span data-stu-id="a9ace-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="a9ace-165">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="a9ace-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="a9ace-166">Отклик</span><span class="sxs-lookup"><span data-stu-id="a9ace-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="a9ace-167">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="a9ace-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="a9ace-168">`createdDateTime`  задайте для будущего задание.</span><span class="sxs-lookup"><span data-stu-id="a9ace-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="a9ace-169">`createdDateTime`  правильно `channelCreationMode`  указанный, но атрибут экземпляра отсутствует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="a9ace-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="a9ace-170">Шаг 3. Импорт сообщений</span><span class="sxs-lookup"><span data-stu-id="a9ace-170">Step Three: Import messages</span></span>

<span data-ttu-id="a9ace-171">После создания команды и канала вы можете начать отправлять сообщения на задний длительное время с `createdDateTime`  помощью `from`  ключей и ключей в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="a9ace-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="a9ace-172">Запрос (только сообщение POST)</span><span class="sxs-lookup"><span data-stu-id="a9ace-172">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="a9ace-173">Отклик</span><span class="sxs-lookup"><span data-stu-id="a9ace-173">Response</span></span>

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

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="a9ace-174">Запрос (запрос POST с встроенным 'изображением)</span><span class="sxs-lookup"><span data-stu-id="a9ace-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="a9ace-175">**Примечание.** В этом сценарии нет специальных областей разрешений, так как запрос входит в chatMessage; также применимы области для chatMessage.</span><span class="sxs-lookup"><span data-stu-id="a9ace-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="a9ace-176">Отклик</span><span class="sxs-lookup"><span data-stu-id="a9ace-176">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="a9ace-177">Шаг 4. Завершение режима миграции</span><span class="sxs-lookup"><span data-stu-id="a9ace-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="a9ace-178">После завершения миграции сообщения команда и канал отводятся из режима миграции с помощью  `completeMigration`  этого метода.</span><span class="sxs-lookup"><span data-stu-id="a9ace-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="a9ace-179">Это действие открывает ресурсы команд и каналов для общего использования участниками команды.</span><span class="sxs-lookup"><span data-stu-id="a9ace-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="a9ace-180">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="a9ace-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="a9ace-181">Запрос (режим миграции конечной группы)</span><span class="sxs-lookup"><span data-stu-id="a9ace-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="a9ace-182">Отклик</span><span class="sxs-lookup"><span data-stu-id="a9ace-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="a9ace-183">Запрос (режим миграции в режиме завершения канала)</span><span class="sxs-lookup"><span data-stu-id="a9ace-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="a9ace-184">Отклик</span><span class="sxs-lookup"><span data-stu-id="a9ace-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="a9ace-185">Отклик с ошибкой</span><span class="sxs-lookup"><span data-stu-id="a9ace-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="a9ace-186">Действие, вызываемое для `team` него `channel` или неявляющиеся. `migrationMode`</span><span class="sxs-lookup"><span data-stu-id="a9ace-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="a9ace-187">Шаг 5. Добавление участников команды</span><span class="sxs-lookup"><span data-stu-id="a9ace-187">Step Five: Add team members</span></span>

<span data-ttu-id="a9ace-188">Вы можете добавить участника в команду с [помощью пользовательского интерфейса Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) или API добавления [участника в](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="a9ace-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="a9ace-189">Запрос (добавление участника)</span><span class="sxs-lookup"><span data-stu-id="a9ace-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="a9ace-190">Отклик</span><span class="sxs-lookup"><span data-stu-id="a9ace-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="a9ace-191">Советы и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="a9ace-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="a9ace-192">Вы можете импортировать сообщения от пользователей, которые отсутствуют в Teams.</span><span class="sxs-lookup"><span data-stu-id="a9ace-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="a9ace-193">После `completeMigration` создания запроса дальнейшие сообщения нельзя импортировать в команду.</span><span class="sxs-lookup"><span data-stu-id="a9ace-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="a9ace-194">Участников команды можно добавлять в новую группу только после `completeMigration` того, как запрос вернет успешный ответ.</span><span class="sxs-lookup"><span data-stu-id="a9ace-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="a9ace-195">Регулирование: импорт сообщений при 5 запросов в секунду на канал.</span><span class="sxs-lookup"><span data-stu-id="a9ace-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="a9ace-196">Если вам нужно внести исправления в результаты миграции, то потребуется удалить команду и повторить шаги, чтобы создать команду, канал и перенести сообщения повторно.</span><span class="sxs-lookup"><span data-stu-id="a9ace-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="a9ace-197">В настоящее время встроенные изображения — это один тип носителя, поддерживаемый схемой API сообщений импорта.</span><span class="sxs-lookup"><span data-stu-id="a9ace-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="a9ace-198">Импорт области контента</span><span class="sxs-lookup"><span data-stu-id="a9ace-198">Import content scope</span></span>

|<span data-ttu-id="a9ace-199">В достижении</span><span class="sxs-lookup"><span data-stu-id="a9ace-199">In-scope</span></span> | <span data-ttu-id="a9ace-200">В настоящее время не в области ставления</span><span class="sxs-lookup"><span data-stu-id="a9ace-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="a9ace-201">Сообщения о командах и каналах</span><span class="sxs-lookup"><span data-stu-id="a9ace-201">Team and channel messages</span></span>|<span data-ttu-id="a9ace-202">Индикансовая и групповые сообщения</span><span class="sxs-lookup"><span data-stu-id="a9ace-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="a9ace-203">Время создания исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="a9ace-203">Created time of the original message</span></span>|<span data-ttu-id="a9ace-204">Закрытые каналы</span><span class="sxs-lookup"><span data-stu-id="a9ace-204">Private channels</span></span>|
|<span data-ttu-id="a9ace-205">Встроенные изображения в состав сообщения.</span><span class="sxs-lookup"><span data-stu-id="a9ace-205">Inline images as part of the message</span></span>|<span data-ttu-id="a9ace-206">В упоминаниях</span><span class="sxs-lookup"><span data-stu-id="a9ace-206">At mentions</span></span>|
|<span data-ttu-id="a9ace-207">Ссылки на существующие файлы в SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="a9ace-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="a9ace-208">Реакции</span><span class="sxs-lookup"><span data-stu-id="a9ace-208">Reactions</span></span>|
|<span data-ttu-id="a9ace-209">Сообщения с форматированным текстом</span><span class="sxs-lookup"><span data-stu-id="a9ace-209">Messages with rich text</span></span>|<span data-ttu-id="a9ace-210">Видео</span><span class="sxs-lookup"><span data-stu-id="a9ace-210">Videos</span></span>|
|<span data-ttu-id="a9ace-211">Цепочка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="a9ace-211">Message reply chain</span></span>|<span data-ttu-id="a9ace-212">Объявления</span><span class="sxs-lookup"><span data-stu-id="a9ace-212">Announcements</span></span>|
|<span data-ttu-id="a9ace-213">Высокая пропускная способность обработки</span><span class="sxs-lookup"><span data-stu-id="a9ace-213">High throughput processing</span></span>|<span data-ttu-id="a9ace-214">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="a9ace-214">Code snippets</span></span>|
||<span data-ttu-id="a9ace-215">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="a9ace-215">Adaptive cards</span></span>|
||<span data-ttu-id="a9ace-216">Стикеры</span><span class="sxs-lookup"><span data-stu-id="a9ace-216">Stickers</span></span>|
||<span data-ttu-id="a9ace-217">Emojis</span><span class="sxs-lookup"><span data-stu-id="a9ace-217">Emojis</span></span>|
||<span data-ttu-id="a9ace-218">Кавычки</span><span class="sxs-lookup"><span data-stu-id="a9ace-218">Quotes</span></span>|
||<span data-ttu-id="a9ace-219">Перекрестные публикации между каналами</span><span class="sxs-lookup"><span data-stu-id="a9ace-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="a9ace-220">Подробнее об интеграции Microsoft Graph и Teams</span><span class="sxs-lookup"><span data-stu-id="a9ace-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
