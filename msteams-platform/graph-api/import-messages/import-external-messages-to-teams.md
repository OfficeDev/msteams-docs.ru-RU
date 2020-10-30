---
title: Импорт сообщений о внешних платформах в Teams с помощью Microsoft Graph
description: В этой статье описывается, как использовать Microsoft Graph для импорта сообщений из внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Microsoft Teams Import messages API Graph перенесите запись миграции
ms.openlocfilehash: 934e00541773140c90c270a616d6bc50aacac6e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796297"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="48c0a-104">Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="48c0a-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="48c0a-105">Microsoft Graph и общедоступные предварительные обзоры Microsoft Teams доступны для раннего доступа и обратной связи.</span><span class="sxs-lookup"><span data-stu-id="48c0a-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="48c0a-106">Несмотря на то что этот выпуск протестировался, он не предназначен для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="48c0a-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="48c0a-107">С помощью Microsoft Graph вы можете перенести в канал Teams существующую историю сообщений и данные пользователей из внешней системы.</span><span class="sxs-lookup"><span data-stu-id="48c0a-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="48c0a-108">Благодаря повторному воссозданию иерархической структуры обмена сообщениями платформы в Teams пользователи могут беспрепятственно продолжить их работу и продолжить работу без перерывов.</span><span class="sxs-lookup"><span data-stu-id="48c0a-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="48c0a-109">Обзор импорта</span><span class="sxs-lookup"><span data-stu-id="48c0a-109">Import overview</span></span>

<span data-ttu-id="48c0a-110">На высоком уровне процесс импорта состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="48c0a-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="48c0a-111">Создание команды с отметкой времени обратного входа</span><span class="sxs-lookup"><span data-stu-id="48c0a-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="48c0a-112">Создание канала с обратной меткой времени</span><span class="sxs-lookup"><span data-stu-id="48c0a-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="48c0a-113">Импорт внешних сообщений с обратной датой после времени</span><span class="sxs-lookup"><span data-stu-id="48c0a-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="48c0a-114">Выполнение процесса миграции группы и канала</span><span class="sxs-lookup"><span data-stu-id="48c0a-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="48c0a-115">Добавление участников группы</span><span class="sxs-lookup"><span data-stu-id="48c0a-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="48c0a-116">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="48c0a-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="48c0a-117">Анализ и подготовка данных сообщения</span><span class="sxs-lookup"><span data-stu-id="48c0a-117">Analyze and prepare message data</span></span>

<span data-ttu-id="48c0a-118">✔ Проанализируйте сторонние данные, чтобы определить, что будет перенесено.</span><span class="sxs-lookup"><span data-stu-id="48c0a-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="48c0a-119">✔ Извлечения выбранных данных из сторонней системы чата.</span><span class="sxs-lookup"><span data-stu-id="48c0a-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="48c0a-120">✔ Сопоставить структуру чата сторонним разработчикам со структурой Teams.</span><span class="sxs-lookup"><span data-stu-id="48c0a-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="48c0a-121">✔ Преобразовать данные импорта в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="48c0a-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="48c0a-122">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="48c0a-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="48c0a-123">✔ Убедиться, что клиент Office 365 существует для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="48c0a-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="48c0a-124">Для получения дополнительных сведений о настройке Office 365 для Teams, *Ознакомьтесь* со статьей [подготовка клиента Office 365](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="48c0a-124">For more information on setting up an Office 365 tenancy for Teams, *see* , [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="48c0a-125">✔ Убедитесь, что участники группы находятся в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="48c0a-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="48c0a-126">Дополнительные сведения *см* . в статье [Добавление нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48c0a-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="48c0a-127">Шаг 1: создание группы</span><span class="sxs-lookup"><span data-stu-id="48c0a-127">Step One: Create a team</span></span>

<span data-ttu-id="48c0a-128">Так как существующие данные переносятся, поддержание исходных меток времени и предотвращение активности сообщений в процессе миграции является ключом к повторному созданию существующего процесса обработки сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="48c0a-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="48c0a-129">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="48c0a-129">This is achieved as follows:</span></span>

> <span data-ttu-id="48c0a-130">[Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) с обратной меткой времени, используя свойство ресурса Team  `createdDateTime`  .</span><span class="sxs-lookup"><span data-stu-id="48c0a-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="48c0a-131">Поместите новую команду в `migration mode` специальное состояние, которое откладывает пользователей от большинства действий в группе до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="48c0a-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="48c0a-132">Добавьте `teamCreationMode` атрибут экземпляра со `migration` значением в запросе POST, чтобы явным образом определить новую команду в качестве ее создания для миграции.</span><span class="sxs-lookup"><span data-stu-id="48c0a-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="48c0a-133">**Note** : `createdDateTime` поле будет заполнено только для тех экземпляров группы или канала, которые были перенесены.</span><span class="sxs-lookup"><span data-stu-id="48c0a-133">**NOTE** :  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="48c0a-134">Разрешения</span><span class="sxs-lookup"><span data-stu-id="48c0a-134">Permissions</span></span>

|<span data-ttu-id="48c0a-135">скопенаме</span><span class="sxs-lookup"><span data-stu-id="48c0a-135">ScopeName</span></span>|<span data-ttu-id="48c0a-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="48c0a-136">DisplayName</span></span>|<span data-ttu-id="48c0a-137">Описание</span><span class="sxs-lookup"><span data-stu-id="48c0a-137">Description</span></span>|<span data-ttu-id="48c0a-138">Тип</span><span class="sxs-lookup"><span data-stu-id="48c0a-138">Type</span></span>|<span data-ttu-id="48c0a-139">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="48c0a-139">Admin Consent?</span></span>|<span data-ttu-id="48c0a-140">Покрываемые сущности и API</span><span class="sxs-lookup"><span data-stu-id="48c0a-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="48c0a-141">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="48c0a-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="48c0a-142">Создание и управление ресурсами для переноса в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="48c0a-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="48c0a-143">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="48c0a-143">**Application-only**</span></span>|<span data-ttu-id="48c0a-144">**Да**</span><span class="sxs-lookup"><span data-stu-id="48c0a-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="48c0a-145">Запрос (создание команды в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="48c0a-145">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="48c0a-146">Отклик</span><span class="sxs-lookup"><span data-stu-id="48c0a-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="48c0a-147">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="48c0a-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="48c0a-148">`createdDateTime`  задается для будущего.</span><span class="sxs-lookup"><span data-stu-id="48c0a-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="48c0a-149">`createdDateTime`  указано правильно, но `teamCreationMode`  атрибут экземпляра отсутствует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="48c0a-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="48c0a-150">Шаг 2: создание канала</span><span class="sxs-lookup"><span data-stu-id="48c0a-150">Step Two: Create a channel</span></span>

<span data-ttu-id="48c0a-151">Создание канала для импортированных сообщений похоже на сценарий создания группы:</span><span class="sxs-lookup"><span data-stu-id="48c0a-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="48c0a-152">[Создайте новый канал](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) с обратной меткой времени, используя свойство Resource Channel `createdDateTime` .</span><span class="sxs-lookup"><span data-stu-id="48c0a-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="48c0a-153">Поместите новый канал в `migration mode` особое состояние, которое откладывает пользователей от большинства действий чата в канал до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="48c0a-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="48c0a-154">Добавьте `channelCreationMode` атрибут экземпляра со `migration` значением в запросе POST, чтобы явным образом определить новую команду в качестве ее создания для миграции.</span><span class="sxs-lookup"><span data-stu-id="48c0a-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="48c0a-155">Разрешения</span><span class="sxs-lookup"><span data-stu-id="48c0a-155">Permissions</span></span>

|<span data-ttu-id="48c0a-156">скопенаме</span><span class="sxs-lookup"><span data-stu-id="48c0a-156">ScopeName</span></span>|<span data-ttu-id="48c0a-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="48c0a-157">DisplayName</span></span>|<span data-ttu-id="48c0a-158">Описание</span><span class="sxs-lookup"><span data-stu-id="48c0a-158">Description</span></span>|<span data-ttu-id="48c0a-159">Тип</span><span class="sxs-lookup"><span data-stu-id="48c0a-159">Type</span></span>|<span data-ttu-id="48c0a-160">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="48c0a-160">Admin Consent?</span></span>|<span data-ttu-id="48c0a-161">Покрываемые сущности и API</span><span class="sxs-lookup"><span data-stu-id="48c0a-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="48c0a-162">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="48c0a-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="48c0a-163">Создание и управление ресурсами для переноса в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="48c0a-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="48c0a-164">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="48c0a-164">**Application-only**</span></span>|<span data-ttu-id="48c0a-165">**Да**</span><span class="sxs-lookup"><span data-stu-id="48c0a-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="48c0a-166">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="48c0a-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="48c0a-167">Отклик</span><span class="sxs-lookup"><span data-stu-id="48c0a-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="48c0a-168">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="48c0a-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="48c0a-169">`createdDateTime`  задается для будущего.</span><span class="sxs-lookup"><span data-stu-id="48c0a-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="48c0a-170">`createdDateTime`  указано правильно, но `channelCreationMode`  атрибут экземпляра отсутствует или задано недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="48c0a-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="48c0a-171">Этап 3: Импорт сообщений</span><span class="sxs-lookup"><span data-stu-id="48c0a-171">Step Three: Import messages</span></span>

<span data-ttu-id="48c0a-172">После создания группы и канала можно начать отправку сообщений в обратном времени, используя `createdDateTime` `from`  ключи и в теле запроса.</span><span class="sxs-lookup"><span data-stu-id="48c0a-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="48c0a-173">**Note** : сообщения, импортированные `createdDateTime` раньше, чем цепочка сообщений `createdDateTime` , не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="48c0a-173">**NOTE** : messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> <span data-ttu-id="48c0a-174">createdDateTime должны быть уникальными для всех сообщений в одном потоке.</span><span class="sxs-lookup"><span data-stu-id="48c0a-174">createdDateTime must be unique across messages in the same thread.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="48c0a-175">Request (сообщение POST, которое является текстовым)</span><span class="sxs-lookup"><span data-stu-id="48c0a-175">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="48c0a-176">Отклик</span><span class="sxs-lookup"><span data-stu-id="48c0a-176">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="48c0a-177">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="48c0a-177">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="48c0a-178">Запрос (публикация сообщения с встроенным изображением)</span><span class="sxs-lookup"><span data-stu-id="48c0a-178">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="48c0a-179">**Note** : в этом сценарии нет особых областей разрешений, так как запрос является частью chatMessage; Здесь также применяются области для chatMessage.</span><span class="sxs-lookup"><span data-stu-id="48c0a-179">**Note** : There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="48c0a-180">Отклик</span><span class="sxs-lookup"><span data-stu-id="48c0a-180">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="48c0a-181">Шаг 4: завершение режима миграции</span><span class="sxs-lookup"><span data-stu-id="48c0a-181">Step Four: Complete migration mode</span></span>

<span data-ttu-id="48c0a-182">После завершения процесса переноса сообщений команда и канал из режима миграции берутся из режима миграции с помощью  `completeMigration`  метода.</span><span class="sxs-lookup"><span data-stu-id="48c0a-182">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="48c0a-183">На этом этапе открываются ресурсы команды и канала для общего использования участниками группы.</span><span class="sxs-lookup"><span data-stu-id="48c0a-183">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="48c0a-184">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="48c0a-184">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="48c0a-185">Запрос (режим миграции команды End)</span><span class="sxs-lookup"><span data-stu-id="48c0a-185">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="48c0a-186">Отклик</span><span class="sxs-lookup"><span data-stu-id="48c0a-186">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="48c0a-187">Запрос (режим миграции конечного канала)</span><span class="sxs-lookup"><span data-stu-id="48c0a-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="48c0a-188">Отклик</span><span class="sxs-lookup"><span data-stu-id="48c0a-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="48c0a-189">Отклик с ошибкой</span><span class="sxs-lookup"><span data-stu-id="48c0a-189">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="48c0a-190">Действие вызвано для объекта a `team` или `channel` не в `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="48c0a-190">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="48c0a-191">Шаг 5: Добавление участников группы</span><span class="sxs-lookup"><span data-stu-id="48c0a-191">Step Five: Add team members</span></span>

<span data-ttu-id="48c0a-192">Добавить участника в команду можно [с помощью пользовательского интерфейса](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Teams или API [добавления элементов](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="48c0a-192">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="48c0a-193">Запрос (Добавление члена)</span><span class="sxs-lookup"><span data-stu-id="48c0a-193">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="48c0a-194">Отклик</span><span class="sxs-lookup"><span data-stu-id="48c0a-194">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="48c0a-195">Советы и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="48c0a-195">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="48c0a-196">Вы можете импортировать сообщения от пользователей, не включенных в Teams.</span><span class="sxs-lookup"><span data-stu-id="48c0a-196">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="48c0a-197">**Note** : сообщения, импортированные для пользователей, отсутствующих в клиенте, не будут поддерживать поиск в клиенте Teams или порталах соответствия требованиям во время общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="48c0a-197">**NOTE** : Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="48c0a-198">Когда `completeMigration` запрос будет выполнен, вы не сможете импортировать дальнейшие сообщения в команду.</span><span class="sxs-lookup"><span data-stu-id="48c0a-198">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="48c0a-199">Участники группы могут быть добавлены в новую группу только после того, как `completeMigration` запрос вернул успешный ответ.</span><span class="sxs-lookup"><span data-stu-id="48c0a-199">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="48c0a-200">Регулирование: сообщения импортируются по 5 RPS на канал.</span><span class="sxs-lookup"><span data-stu-id="48c0a-200">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="48c0a-201">Если необходимо внести исправления в результаты миграции, необходимо удалить команду и повторить действия, чтобы создать группу и канал и повторно перенести сообщения.</span><span class="sxs-lookup"><span data-stu-id="48c0a-201">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="48c0a-202">В настоящее время встроенными образами является единственный тип мультимедиа, поддерживаемый схемой API импорта сообщений.</span><span class="sxs-lookup"><span data-stu-id="48c0a-202">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="48c0a-203">Область импорта контента</span><span class="sxs-lookup"><span data-stu-id="48c0a-203">Import content scope</span></span>

|<span data-ttu-id="48c0a-204">В области</span><span class="sxs-lookup"><span data-stu-id="48c0a-204">In-scope</span></span> | <span data-ttu-id="48c0a-205">На данный момент вне области</span><span class="sxs-lookup"><span data-stu-id="48c0a-205">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="48c0a-206">Сообщения группы и канала</span><span class="sxs-lookup"><span data-stu-id="48c0a-206">Team and channel messages</span></span>|<span data-ttu-id="48c0a-207">1:1 и сообщения группового чата</span><span class="sxs-lookup"><span data-stu-id="48c0a-207">1:1 and group chat messages</span></span>|
|<span data-ttu-id="48c0a-208">Время создания исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="48c0a-208">Created time of the original message</span></span>|<span data-ttu-id="48c0a-209">Частные каналы</span><span class="sxs-lookup"><span data-stu-id="48c0a-209">Private channels</span></span>|
|<span data-ttu-id="48c0a-210">Встроенные изображения в составе сообщения</span><span class="sxs-lookup"><span data-stu-id="48c0a-210">Inline images as part of the message</span></span>|<span data-ttu-id="48c0a-211">С упоминаниями</span><span class="sxs-lookup"><span data-stu-id="48c0a-211">At mentions</span></span>|
|<span data-ttu-id="48c0a-212">Ссылки на существующие файлы в SPO и OneDrive</span><span class="sxs-lookup"><span data-stu-id="48c0a-212">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="48c0a-213">Реакция</span><span class="sxs-lookup"><span data-stu-id="48c0a-213">Reactions</span></span>|
|<span data-ttu-id="48c0a-214">Сообщения с форматированным текстом</span><span class="sxs-lookup"><span data-stu-id="48c0a-214">Messages with rich text</span></span>|<span data-ttu-id="48c0a-215">Видео</span><span class="sxs-lookup"><span data-stu-id="48c0a-215">Videos</span></span>|
|<span data-ttu-id="48c0a-216">Цепочка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="48c0a-216">Message reply chain</span></span>|<span data-ttu-id="48c0a-217">Объявления</span><span class="sxs-lookup"><span data-stu-id="48c0a-217">Announcements</span></span>|
|<span data-ttu-id="48c0a-218">Обработка высокой пропускной способности</span><span class="sxs-lookup"><span data-stu-id="48c0a-218">High throughput processing</span></span>|<span data-ttu-id="48c0a-219">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="48c0a-219">Code snippets</span></span>|
||<span data-ttu-id="48c0a-220">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="48c0a-220">Adaptive cards</span></span>|
||<span data-ttu-id="48c0a-221">Наклейки</span><span class="sxs-lookup"><span data-stu-id="48c0a-221">Stickers</span></span>|
||<span data-ttu-id="48c0a-222">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="48c0a-222">Emojis</span></span>|
||<span data-ttu-id="48c0a-223">Quote</span><span class="sxs-lookup"><span data-stu-id="48c0a-223">Quotes</span></span>|
||<span data-ttu-id="48c0a-224">Перекрестные публикации между каналами</span><span class="sxs-lookup"><span data-stu-id="48c0a-224">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="48c0a-225">Дополнительные сведения о интеграции Microsoft Graph и Teams</span><span class="sxs-lookup"><span data-stu-id="48c0a-225">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
