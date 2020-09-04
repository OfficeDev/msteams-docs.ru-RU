---
title: Импорт сообщений о внешних платформах в Teams с помощью Microsoft Graph
description: В этой статье описывается, как использовать Microsoft Graph для импорта сообщений из внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: временной резерв команды импорта сообщений API Graph перенесите запись миграции
ms.openlocfilehash: 0e0aa96373d29f07893456adf54986ec23bdec3c
ms.sourcegitcommit: 02ab2cb7820dc8665bb4ec6a1a40c3b8b8f29d66
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/03/2020
ms.locfileid: "47340951"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="56245-104">Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="56245-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="56245-105">Microsoft Graph и общедоступные предварительные обзоры Microsoft Teams доступны для раннего доступа и обратной связи.</span><span class="sxs-lookup"><span data-stu-id="56245-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="56245-106">Несмотря на то что этот выпуск протестировался, он не предназначен для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="56245-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="56245-107">С помощью Microsoft Graph вы можете перенести в канал Teams существующую историю сообщений и данные пользователей из внешней системы.</span><span class="sxs-lookup"><span data-stu-id="56245-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="56245-108">Благодаря повторному воссозданию иерархической структуры обмена сообщениями платформы в Teams пользователи могут беспрепятственно продолжить их работу и продолжить работу без перерывов.</span><span class="sxs-lookup"><span data-stu-id="56245-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="56245-109">Обзор импорта</span><span class="sxs-lookup"><span data-stu-id="56245-109">Import overview</span></span>

<span data-ttu-id="56245-110">На высоком уровне процесс импорта состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="56245-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="56245-111">Создание команды с отметкой времени обратного входа</span><span class="sxs-lookup"><span data-stu-id="56245-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="56245-112">Создание канала с обратной меткой времени</span><span class="sxs-lookup"><span data-stu-id="56245-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="56245-113">Импорт внешних сообщений с обратной датой после времени</span><span class="sxs-lookup"><span data-stu-id="56245-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="56245-114">Выполнение процесса миграции группы и канала</span><span class="sxs-lookup"><span data-stu-id="56245-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="56245-115">Добавление участников группы</span><span class="sxs-lookup"><span data-stu-id="56245-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="56245-116">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="56245-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="56245-117">Анализ и подготовка данных сообщения</span><span class="sxs-lookup"><span data-stu-id="56245-117">Analyze and prepare message data</span></span>

<span data-ttu-id="56245-118">✔ Проанализируйте сторонние данные, чтобы определить, что будет перенесено.</span><span class="sxs-lookup"><span data-stu-id="56245-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="56245-119">✔ Извлечения выбранных данных из сторонней системы чата.</span><span class="sxs-lookup"><span data-stu-id="56245-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="56245-120">✔ Преобразовать данные импорта в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="56245-120">✔ Convert import data into format needed for migration.</span></span>  
<span data-ttu-id="56245-121">✔ Сопоставить структуру чата сторонним разработчикам со структурой Teams.</span><span class="sxs-lookup"><span data-stu-id="56245-121">✔ Map the third-party chat structure to the Teams structure.</span></span>

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="56245-122">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="56245-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="56245-123">✔ Убедиться, что клиент Office 365 существует для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="56245-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="56245-124">Для получения дополнительных сведений о настройке Office 365 для Teams, *Ознакомьтесь*со статьей [подготовка клиента Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="56245-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="56245-125">✔ Убедитесь, что участники группы находятся в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="56245-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="56245-126">Дополнительные сведения *см* . в статье [Добавление нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="56245-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="56245-127">Шаг 1: создание группы</span><span class="sxs-lookup"><span data-stu-id="56245-127">Step One: Create a team</span></span>

<span data-ttu-id="56245-128">Так как существующие данные переносятся, поддержание исходных меток времени и предотвращение активности сообщений в процессе миграции является ключом к повторному созданию существующего процесса обработки сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="56245-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="56245-129">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="56245-129">This is achieved as follows:</span></span>

1. <span data-ttu-id="56245-130">[Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http) с обратной меткой времени, используя свойство ресурса Team  `createdDateTime`  .</span><span class="sxs-lookup"><span data-stu-id="56245-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span>  

1. <span data-ttu-id="56245-131">Поместите новую команду в `migration mode` специальное состояние, которое откладывает пользователей от большинства действий в группе до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="56245-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="56245-132">Добавьте `teamCreationMode` атрибут экземпляра со `migration` значением в запросе POST, чтобы явным образом определить новую команду в качестве ее создания для миграции.</span><span class="sxs-lookup"><span data-stu-id="56245-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="56245-133">Разрешения</span><span class="sxs-lookup"><span data-stu-id="56245-133">Permissions</span></span>

|<span data-ttu-id="56245-134">скопенаме</span><span class="sxs-lookup"><span data-stu-id="56245-134">ScopeName</span></span>|<span data-ttu-id="56245-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="56245-135">DisplayName</span></span>|<span data-ttu-id="56245-136">Описание</span><span class="sxs-lookup"><span data-stu-id="56245-136">Description</span></span>|<span data-ttu-id="56245-137">Тип</span><span class="sxs-lookup"><span data-stu-id="56245-137">Type</span></span>|<span data-ttu-id="56245-138">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="56245-138">Admin Consent?</span></span>|<span data-ttu-id="56245-139">Покрываемые сущности и API</span><span class="sxs-lookup"><span data-stu-id="56245-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="56245-140">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="56245-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="56245-141">Создание и управление ресурсами для переноса в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="56245-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="56245-142">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="56245-142">**Application-only**</span></span>|<span data-ttu-id="56245-143">**Да**</span><span class="sxs-lookup"><span data-stu-id="56245-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="56245-144">Запрос (создание команды в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="56245-144">Request (create a team in migration state)</span></span>

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a><span data-ttu-id="56245-145">Отклик</span><span class="sxs-lookup"><span data-stu-id="56245-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="56245-146">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="56245-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="56245-147">`createdDateTime`  задается для будущего.</span><span class="sxs-lookup"><span data-stu-id="56245-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="56245-148">`createdDateTime`  указано правильно, но `teamCreationMode`  атрибут экземпляра отсутствует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="56245-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="56245-149">Шаг 2: создание канала</span><span class="sxs-lookup"><span data-stu-id="56245-149">Step Two: Create a channel</span></span>

<span data-ttu-id="56245-150">Создание канала для импортированных сообщений похоже на сценарий создания группы:</span><span class="sxs-lookup"><span data-stu-id="56245-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span> 

1. <span data-ttu-id="56245-151">[Создайте новый канал](/graph/api/channel-post?view=graph-rest-beta&tabs=http) с обратной меткой времени, используя свойство Resource Channel `createdDateTime` .</span><span class="sxs-lookup"><span data-stu-id="56245-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span>

1. <span data-ttu-id="56245-152">Поместите новый канал в `migration mode` особое состояние, которое откладывает пользователей от большинства действий чата в канал до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="56245-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="56245-153">Добавьте `channelCreationMode` атрибут экземпляра со `migration` значением в запросе POST, чтобы явным образом определить новую команду в качестве ее создания для миграции.</span><span class="sxs-lookup"><span data-stu-id="56245-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="56245-154">Разрешения</span><span class="sxs-lookup"><span data-stu-id="56245-154">Permissions</span></span>

|<span data-ttu-id="56245-155">скопенаме</span><span class="sxs-lookup"><span data-stu-id="56245-155">ScopeName</span></span>|<span data-ttu-id="56245-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="56245-156">DisplayName</span></span>|<span data-ttu-id="56245-157">Описание</span><span class="sxs-lookup"><span data-stu-id="56245-157">Description</span></span>|<span data-ttu-id="56245-158">Тип</span><span class="sxs-lookup"><span data-stu-id="56245-158">Type</span></span>|<span data-ttu-id="56245-159">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="56245-159">Admin Consent?</span></span>|<span data-ttu-id="56245-160">Покрываемые сущности и API</span><span class="sxs-lookup"><span data-stu-id="56245-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="56245-161">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="56245-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="56245-162">Создание и управление ресурсами для переноса в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="56245-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="56245-163">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="56245-163">**Application-only**</span></span>|<span data-ttu-id="56245-164">**Да**</span><span class="sxs-lookup"><span data-stu-id="56245-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="56245-165">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="56245-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="56245-166">Отклик</span><span class="sxs-lookup"><span data-stu-id="56245-166">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a><span data-ttu-id="56245-167">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="56245-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="56245-168">`createdDateTime`  задается для будущего.</span><span class="sxs-lookup"><span data-stu-id="56245-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="56245-169">`createdDateTime`  указано правильно, но `channelCreationMode`  атрибут экземпляра отсутствует или задано недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="56245-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="56245-170">Этап 3: Импорт сообщений</span><span class="sxs-lookup"><span data-stu-id="56245-170">Step Three: Import messages</span></span>

<span data-ttu-id="56245-171">После создания группы и канала можно начать отправку сообщений в обратном времени, используя `createdDateTime` `from`  ключи и в теле запроса.</span><span class="sxs-lookup"><span data-stu-id="56245-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="56245-172">Request (сообщение POST, которое является текстовым)</span><span class="sxs-lookup"><span data-stu-id="56245-172">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="56245-173">Отклик</span><span class="sxs-lookup"><span data-stu-id="56245-173">Response</span></span>

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

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="56245-174">Запрос (публикация сообщения с встроенным изображением)</span><span class="sxs-lookup"><span data-stu-id="56245-174">Request (POST a message with inline \`image)</span></span>

> <span data-ttu-id="56245-175">**Note**: в этом сценарии нет особых областей разрешений, так как запрос является частью chatMessage; Здесь также применяются области для chatMessage.</span><span class="sxs-lookup"><span data-stu-id="56245-175">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="56245-176">Отклик</span><span class="sxs-lookup"><span data-stu-id="56245-176">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="56245-177">Шаг 4: завершение режима миграции</span><span class="sxs-lookup"><span data-stu-id="56245-177">Step Four: Complete migration mode</span></span>

<span data-ttu-id="56245-178">После завершения процесса переноса сообщений команда и канал из режима миграции берутся из режима миграции с помощью  `completeMigration`  метода.</span><span class="sxs-lookup"><span data-stu-id="56245-178">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="56245-179">На этом этапе открываются ресурсы команды и канала для общего использования участниками группы.</span><span class="sxs-lookup"><span data-stu-id="56245-179">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="56245-180">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="56245-180">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="56245-181">Запрос (режим миграции команды End)</span><span class="sxs-lookup"><span data-stu-id="56245-181">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="56245-182">Отклик</span><span class="sxs-lookup"><span data-stu-id="56245-182">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="56245-183">Запрос (режим миграции конечного канала)</span><span class="sxs-lookup"><span data-stu-id="56245-183">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="56245-184">Отклик</span><span class="sxs-lookup"><span data-stu-id="56245-184">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="56245-185">Отклик с ошибкой</span><span class="sxs-lookup"><span data-stu-id="56245-185">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="56245-186">Действие вызвано для объекта a `team` или `channel` не в `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="56245-186">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="56245-187">Шаг 5: Добавление участников группы</span><span class="sxs-lookup"><span data-stu-id="56245-187">Step Five: Add team members</span></span>

<span data-ttu-id="56245-188">Добавить участника в команду можно [с помощью пользовательского интерфейса](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Teams или API [добавления элементов](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="56245-188">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="56245-189">Запрос (Добавление члена)</span><span class="sxs-lookup"><span data-stu-id="56245-189">Request (add member)</span></span>

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a><span data-ttu-id="56245-190">Отклик</span><span class="sxs-lookup"><span data-stu-id="56245-190">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="56245-191">Советы и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="56245-191">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="56245-192">Вы можете импортировать сообщения от пользователей, не включенных в Teams.</span><span class="sxs-lookup"><span data-stu-id="56245-192">You can import messages from users who are not in Teams.</span></span>

* <span data-ttu-id="56245-193">Когда `completeMigration` запрос будет выполнен, вы не сможете импортировать дальнейшие сообщения в команду.</span><span class="sxs-lookup"><span data-stu-id="56245-193">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="56245-194">Участники группы могут быть добавлены в новую группу только после того, как `completeMigration` запрос вернул успешный ответ.</span><span class="sxs-lookup"><span data-stu-id="56245-194">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="56245-195">Регулирование: сообщения импортируются по 5 RPS на канал.</span><span class="sxs-lookup"><span data-stu-id="56245-195">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="56245-196">Если необходимо внести исправления в результаты миграции, необходимо удалить команду и повторить действия, чтобы создать группу и канал и повторно перенести сообщения.</span><span class="sxs-lookup"><span data-stu-id="56245-196">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="56245-197">В настоящее время встроенными образами является единственный тип мультимедиа, поддерживаемый схемой API импорта сообщений.</span><span class="sxs-lookup"><span data-stu-id="56245-197">Currently, Inline images is the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="56245-198">Область импорта контента</span><span class="sxs-lookup"><span data-stu-id="56245-198">Import content scope</span></span>

|<span data-ttu-id="56245-199">В области</span><span class="sxs-lookup"><span data-stu-id="56245-199">In-scope</span></span> | <span data-ttu-id="56245-200">На данный момент вне области</span><span class="sxs-lookup"><span data-stu-id="56245-200">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="56245-201">Сообщения группы и канала</span><span class="sxs-lookup"><span data-stu-id="56245-201">Team and channel messages</span></span>|<span data-ttu-id="56245-202">1:1 и сообщения группового чата</span><span class="sxs-lookup"><span data-stu-id="56245-202">1:1 and group chat messages</span></span>|
|<span data-ttu-id="56245-203">Время создания исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="56245-203">Created time of the original message</span></span>|<span data-ttu-id="56245-204">Частные каналы</span><span class="sxs-lookup"><span data-stu-id="56245-204">Private channels</span></span>|
|<span data-ttu-id="56245-205">Встроенные изображения в составе сообщения</span><span class="sxs-lookup"><span data-stu-id="56245-205">Inline images as part of the message</span></span>|<span data-ttu-id="56245-206">С упоминаниями</span><span class="sxs-lookup"><span data-stu-id="56245-206">At mentions</span></span>|
|<span data-ttu-id="56245-207">Ссылки на существующие файлы в SPO и OneDrive</span><span class="sxs-lookup"><span data-stu-id="56245-207">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="56245-208">Реакция</span><span class="sxs-lookup"><span data-stu-id="56245-208">Reactions</span></span>|
|<span data-ttu-id="56245-209">Сообщения с форматированным текстом</span><span class="sxs-lookup"><span data-stu-id="56245-209">Messages with rich text</span></span>|<span data-ttu-id="56245-210">Видео</span><span class="sxs-lookup"><span data-stu-id="56245-210">Videos</span></span>|
|<span data-ttu-id="56245-211">Цепочка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="56245-211">Message reply chain</span></span>|<span data-ttu-id="56245-212">Объявления</span><span class="sxs-lookup"><span data-stu-id="56245-212">Announcements</span></span>|
|<span data-ttu-id="56245-213">Обработка высокой пропускной способности</span><span class="sxs-lookup"><span data-stu-id="56245-213">High throughput processing</span></span>|<span data-ttu-id="56245-214">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="56245-214">Code snippets</span></span>|
||<span data-ttu-id="56245-215">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="56245-215">Adaptive cards</span></span>|
||<span data-ttu-id="56245-216">Наклейки</span><span class="sxs-lookup"><span data-stu-id="56245-216">Stickers</span></span>|
||<span data-ttu-id="56245-217">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="56245-217">Emojis</span></span>|
||<span data-ttu-id="56245-218">Quote</span><span class="sxs-lookup"><span data-stu-id="56245-218">Quotes</span></span>|
||<span data-ttu-id="56245-219">Перекрестные публикации между каналами</span><span class="sxs-lookup"><span data-stu-id="56245-219">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="56245-220">Дополнительные сведения о интеграции Microsoft Graph и Teams</span><span class="sxs-lookup"><span data-stu-id="56245-220">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
