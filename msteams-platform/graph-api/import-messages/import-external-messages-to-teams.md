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
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="4658d-104">Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="4658d-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="4658d-105">Общедоступные предварительные версии Microsoft Graph и Microsoft Teams доступны для раннего доступа и отзывов.</span><span class="sxs-lookup"><span data-stu-id="4658d-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="4658d-106">Хотя этот выпуск прошел тщательное тестирование, он не предназначен для использования в производственной версии.</span><span class="sxs-lookup"><span data-stu-id="4658d-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="4658d-107">С помощью Microsoft Graph вы можете перенести существующую историю сообщений и данные пользователей из внешней системы в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="4658d-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="4658d-108">Обеспечивая воссоздание иерархии обмена сообщениями на стороне платформы в Teams, пользователи могут бесперебойно продолжать общение и продолжать работу без перерывов.</span><span class="sxs-lookup"><span data-stu-id="4658d-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

## <a name="import-overview"></a><span data-ttu-id="4658d-109">Обзор импорта</span><span class="sxs-lookup"><span data-stu-id="4658d-109">Import overview</span></span>

<span data-ttu-id="4658d-110">На высоком уровне процесс импорта состоит из следующих процессов:</span><span class="sxs-lookup"><span data-stu-id="4658d-110">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="4658d-111">Создание команды с помощью запапамя времени</span><span class="sxs-lookup"><span data-stu-id="4658d-111">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="4658d-112">Создание канала с помощью запамяканного времени</span><span class="sxs-lookup"><span data-stu-id="4658d-112">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="4658d-113">Импорт внешних отсвещенных назад сообщений</span><span class="sxs-lookup"><span data-stu-id="4658d-113">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="4658d-114">Завершение процесса миграции команды и канала</span><span class="sxs-lookup"><span data-stu-id="4658d-114">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="4658d-115">Добавление участников команды</span><span class="sxs-lookup"><span data-stu-id="4658d-115">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="4658d-116">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="4658d-116">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="4658d-117">Анализ и подготовка данных сообщений</span><span class="sxs-lookup"><span data-stu-id="4658d-117">Analyze and prepare message data</span></span>

<span data-ttu-id="4658d-118">✔ просмотрите сторонние данные, чтобы решить, что будет перенесено.</span><span class="sxs-lookup"><span data-stu-id="4658d-118">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="4658d-119">✔ извлечь выбранные данные из стороной системы чата.</span><span class="sxs-lookup"><span data-stu-id="4658d-119">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="4658d-120">✔ со структурой чата сторонних сторон со структурой Teams.</span><span class="sxs-lookup"><span data-stu-id="4658d-120">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="4658d-121">✔ импорт данных в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="4658d-121">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="4658d-122">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="4658d-122">Set up your Office 365 tenant</span></span>

<span data-ttu-id="4658d-123">✔ убедитесь, что клиент Office 365 существует для данных импорта.</span><span class="sxs-lookup"><span data-stu-id="4658d-123">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="4658d-124">Дополнительные сведения о настройке клиента Office 365 для Teams см. в подготовьте клиент [Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md) </span><span class="sxs-lookup"><span data-stu-id="4658d-124">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="4658d-125">✔ убедитесь, что участники группы находятся в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="4658d-125">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="4658d-126">Дополнительные сведения *см.* [в записи "Добавление нового пользователя](/azure/active-directory/fundamentals/add-users-azure-active-directory) в Azure Active Directory".</span><span class="sxs-lookup"><span data-stu-id="4658d-126">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="4658d-127">Шаг 1. Создание команды</span><span class="sxs-lookup"><span data-stu-id="4658d-127">Step One: Create a team</span></span>

<span data-ttu-id="4658d-128">Так как существующие данные переносят, сохранение меток времени исходного сообщения и предотвращение активности обмена сообщениями во время миграции являются ключевым фактором для воссоздания существующего потока сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="4658d-128">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="4658d-129">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4658d-129">This is achieved as follows:</span></span>

> <span data-ttu-id="4658d-130">[Создайте новую команду со](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) временем с помощью свойства ресурса  `createdDateTime`  команды.</span><span class="sxs-lookup"><span data-stu-id="4658d-130">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="4658d-131">Поместите новую команду в специальное состояние, которое не позволяет пользователям выполнить большинство действий в команде до завершения процесса `migration mode` миграции.</span><span class="sxs-lookup"><span data-stu-id="4658d-131">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="4658d-132">Включив атрибут экземпляра со значением в запрос POST, чтобы явно определить новую команду как созданную `teamCreationMode` `migration` для миграции.</span><span class="sxs-lookup"><span data-stu-id="4658d-132">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="4658d-133">**ПРИМЕЧАНИЕ.** Поле будет заполнено только для перенесенных экземпляров команды или `createdDateTime` канала.</span><span class="sxs-lookup"><span data-stu-id="4658d-133">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="4658d-134">Разрешения</span><span class="sxs-lookup"><span data-stu-id="4658d-134">Permissions</span></span>

|<span data-ttu-id="4658d-135">ScopeName</span><span class="sxs-lookup"><span data-stu-id="4658d-135">ScopeName</span></span>|<span data-ttu-id="4658d-136">DisplayName</span><span class="sxs-lookup"><span data-stu-id="4658d-136">DisplayName</span></span>|<span data-ttu-id="4658d-137">Описание</span><span class="sxs-lookup"><span data-stu-id="4658d-137">Description</span></span>|<span data-ttu-id="4658d-138">Тип</span><span class="sxs-lookup"><span data-stu-id="4658d-138">Type</span></span>|<span data-ttu-id="4658d-139">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="4658d-139">Admin Consent?</span></span>|<span data-ttu-id="4658d-140">Объекты и API, охватываемых</span><span class="sxs-lookup"><span data-stu-id="4658d-140">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="4658d-141">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4658d-141">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="4658d-142">Создание и управление ресурсами для миграции в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4658d-142">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="4658d-143">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="4658d-143">**Application-only**</span></span>|<span data-ttu-id="4658d-144">**Да**</span><span class="sxs-lookup"><span data-stu-id="4658d-144">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="4658d-145">Запрос (создание команды в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="4658d-145">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="4658d-146">Отклик</span><span class="sxs-lookup"><span data-stu-id="4658d-146">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="4658d-147">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="4658d-147">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="4658d-148">`createdDateTime`  настроено на будущее.</span><span class="sxs-lookup"><span data-stu-id="4658d-148">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="4658d-149">`createdDateTime`  правильно указано, но атрибут `teamCreationMode`  экземпляра отсутствует или задан как недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="4658d-149">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="4658d-150">Шаг 2. Создание канала</span><span class="sxs-lookup"><span data-stu-id="4658d-150">Step Two: Create a channel</span></span>

<span data-ttu-id="4658d-151">Создание канала для импортируемых сообщений аналогично сценарию создания команды:</span><span class="sxs-lookup"><span data-stu-id="4658d-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="4658d-152">[Создайте новый канал](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) со временем с помощью свойства `createdDateTime` ресурса канала.</span><span class="sxs-lookup"><span data-stu-id="4658d-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="4658d-153">Поместите новый канал в специальное состояние, которое не позволяет пользователям от большинства действий чата в канале до завершения `migration mode` процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="4658d-153">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="4658d-154">Включив атрибут экземпляра со значением в запрос POST, чтобы явно определить новую команду как созданную `channelCreationMode` `migration` для миграции.</span><span class="sxs-lookup"><span data-stu-id="4658d-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="4658d-155">Разрешения</span><span class="sxs-lookup"><span data-stu-id="4658d-155">Permissions</span></span>

|<span data-ttu-id="4658d-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="4658d-156">ScopeName</span></span>|<span data-ttu-id="4658d-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="4658d-157">DisplayName</span></span>|<span data-ttu-id="4658d-158">Описание</span><span class="sxs-lookup"><span data-stu-id="4658d-158">Description</span></span>|<span data-ttu-id="4658d-159">Тип</span><span class="sxs-lookup"><span data-stu-id="4658d-159">Type</span></span>|<span data-ttu-id="4658d-160">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="4658d-160">Admin Consent?</span></span>|<span data-ttu-id="4658d-161">Объекты и API, охватываемых</span><span class="sxs-lookup"><span data-stu-id="4658d-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="4658d-162">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4658d-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="4658d-163">Создание и управление ресурсами для миграции в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="4658d-163">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="4658d-164">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="4658d-164">**Application-only**</span></span>|<span data-ttu-id="4658d-165">**Да**</span><span class="sxs-lookup"><span data-stu-id="4658d-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="4658d-166">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="4658d-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="4658d-167">Отклик</span><span class="sxs-lookup"><span data-stu-id="4658d-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="4658d-168">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="4658d-168">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="4658d-169">`createdDateTime`  настроено на будущее.</span><span class="sxs-lookup"><span data-stu-id="4658d-169">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="4658d-170">`createdDateTime`  правильно указано, но `channelCreationMode`  атрибут экземпляра отсутствует или задан как недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="4658d-170">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="4658d-171">Шаг 3. Импорт сообщений</span><span class="sxs-lookup"><span data-stu-id="4658d-171">Step Three: Import messages</span></span>

<span data-ttu-id="4658d-172">После создания команды и канала можно приступить к отправке сообщений о времени с помощью ключей и ключей `createdDateTime` `from`  в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="4658d-172">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="4658d-173">**ПРИМЕЧАНИЕ.** Сообщения, импортируемые раньше, `createdDateTime` чем поток сообщений, не `createdDateTime` поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4658d-173">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="4658d-174">`createdDateTime` должно быть уникальным для всех сообщений в одном потоке.</span><span class="sxs-lookup"><span data-stu-id="4658d-174">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="4658d-175">`createdDateTime` поддерживает метки времени с точностью в миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="4658d-175">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="4658d-176">Например, если для входящих запросов за установлено значение `createdDateTime` *2020-09-16T05:50:31.0025302Z,* то оно будет преобразовано в *2020-09-16T05:50:31.002Z* при входящих сообщениях.</span><span class="sxs-lookup"><span data-stu-id="4658d-176">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="4658d-177">Запрос (сообщение POST, которое является текстовым)</span><span class="sxs-lookup"><span data-stu-id="4658d-177">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="4658d-178">Отклик</span><span class="sxs-lookup"><span data-stu-id="4658d-178">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="4658d-179">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="4658d-179">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="4658d-180">Запрос (POST-сообщение со inline image)</span><span class="sxs-lookup"><span data-stu-id="4658d-180">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="4658d-181">**Примечание.** В этом сценарии нет особых областей разрешений, так как запрос является частью chatMessage; области для chatMessage применяются и здесь.</span><span class="sxs-lookup"><span data-stu-id="4658d-181">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="4658d-182">Отклик</span><span class="sxs-lookup"><span data-stu-id="4658d-182">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="4658d-183">Шаг 4. Полный режим миграции</span><span class="sxs-lookup"><span data-stu-id="4658d-183">Step Four: Complete migration mode</span></span>

<span data-ttu-id="4658d-184">После завершения процесса переноса сообщений команда и канал вывели команду и канал из режима миграции с помощью  `completeMigration`  этого метода.</span><span class="sxs-lookup"><span data-stu-id="4658d-184">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="4658d-185">Этот шаг открывает ресурсы команды и канала для общего использования участниками команды.</span><span class="sxs-lookup"><span data-stu-id="4658d-185">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="4658d-186">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="4658d-186">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="4658d-187">Запрос (режим миграции команды)</span><span class="sxs-lookup"><span data-stu-id="4658d-187">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="4658d-188">Отклик</span><span class="sxs-lookup"><span data-stu-id="4658d-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="4658d-189">Запрос (режим переноса конечных каналов)</span><span class="sxs-lookup"><span data-stu-id="4658d-189">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="4658d-190">Отклик</span><span class="sxs-lookup"><span data-stu-id="4658d-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="4658d-191">Отклик с ошибкой</span><span class="sxs-lookup"><span data-stu-id="4658d-191">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="4658d-192">Действие, которое вызвано `team` для действия, `channel` которое не находится в `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="4658d-192">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="4658d-193">Шаг 5. Добавление участников команды</span><span class="sxs-lookup"><span data-stu-id="4658d-193">Step Five: Add team members</span></span>

<span data-ttu-id="4658d-194">Вы можете добавить участника в команду с помощью пользовательского интерфейса [Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) или API [добавления](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) членов Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="4658d-194">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="4658d-195">Запрос (добавление участника)</span><span class="sxs-lookup"><span data-stu-id="4658d-195">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="4658d-196">Отклик</span><span class="sxs-lookup"><span data-stu-id="4658d-196">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="4658d-197">Советы и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="4658d-197">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="4658d-198">Вы можете импортировать сообщения от пользователей, которые не работают в Teams.</span><span class="sxs-lookup"><span data-stu-id="4658d-198">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="4658d-199">**ПРИМЕЧАНИЕ.** Сообщения, импортируемые для пользователей, не присутствующих в клиенте, не будут искаться в клиенте Teams или на порталах соответствия требованиям во время открытой предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="4658d-199">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="4658d-200">После `completeMigration` запроса вы не сможете импортировать дополнительные сообщения в команду.</span><span class="sxs-lookup"><span data-stu-id="4658d-200">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="4658d-201">Членов группы можно добавить в новую команду только после того, как запрос `completeMigration` возвратил успешный ответ.</span><span class="sxs-lookup"><span data-stu-id="4658d-201">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="4658d-202">Регулирование: импорт сообщений при 5 запросах в секунду на канал.</span><span class="sxs-lookup"><span data-stu-id="4658d-202">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="4658d-203">Если вам нужно внести изменения в результаты миграции, необходимо удалить команду и повторить действия, чтобы создать команду и канал и повторно перенести сообщения.</span><span class="sxs-lookup"><span data-stu-id="4658d-203">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="4658d-204">В настоящее время inline images are the only type of media supported by the import message API schema.</span><span class="sxs-lookup"><span data-stu-id="4658d-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="4658d-205">Импорт области контента</span><span class="sxs-lookup"><span data-stu-id="4658d-205">Import content scope</span></span>

|<span data-ttu-id="4658d-206">Область действия</span><span class="sxs-lookup"><span data-stu-id="4658d-206">In-scope</span></span> | <span data-ttu-id="4658d-207">В настоящее время выходит за рамки области</span><span class="sxs-lookup"><span data-stu-id="4658d-207">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="4658d-208">Сообщения о команде и канале</span><span class="sxs-lookup"><span data-stu-id="4658d-208">Team and channel messages</span></span>|<span data-ttu-id="4658d-209">1:1 и сообщения группового чата</span><span class="sxs-lookup"><span data-stu-id="4658d-209">1:1 and group chat messages</span></span>|
|<span data-ttu-id="4658d-210">Время создания исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="4658d-210">Created time of the original message</span></span>|<span data-ttu-id="4658d-211">Частные каналы</span><span class="sxs-lookup"><span data-stu-id="4658d-211">Private channels</span></span>|
|<span data-ttu-id="4658d-212">Inline images as part of the message</span><span class="sxs-lookup"><span data-stu-id="4658d-212">Inline images as part of the message</span></span>|<span data-ttu-id="4658d-213">При упоминаний</span><span class="sxs-lookup"><span data-stu-id="4658d-213">At mentions</span></span>|
|<span data-ttu-id="4658d-214">Ссылки на существующие файлы в SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="4658d-214">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="4658d-215">Реакции</span><span class="sxs-lookup"><span data-stu-id="4658d-215">Reactions</span></span>|
|<span data-ttu-id="4658d-216">Сообщения с химким текстом</span><span class="sxs-lookup"><span data-stu-id="4658d-216">Messages with rich text</span></span>|<span data-ttu-id="4658d-217">Видео</span><span class="sxs-lookup"><span data-stu-id="4658d-217">Videos</span></span>|
|<span data-ttu-id="4658d-218">Цепочка ответов сообщений</span><span class="sxs-lookup"><span data-stu-id="4658d-218">Message reply chain</span></span>|<span data-ttu-id="4658d-219">Объявления</span><span class="sxs-lookup"><span data-stu-id="4658d-219">Announcements</span></span>|
|<span data-ttu-id="4658d-220">Обработка высокой пропускной способности</span><span class="sxs-lookup"><span data-stu-id="4658d-220">High throughput processing</span></span>|<span data-ttu-id="4658d-221">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="4658d-221">Code snippets</span></span>|
||<span data-ttu-id="4658d-222">Адаптивные карточки</span><span class="sxs-lookup"><span data-stu-id="4658d-222">Adaptive cards</span></span>|
||<span data-ttu-id="4658d-223">Стикеры</span><span class="sxs-lookup"><span data-stu-id="4658d-223">Stickers</span></span>|
||<span data-ttu-id="4658d-224">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="4658d-224">Emojis</span></span>|
||<span data-ttu-id="4658d-225">Кавычка</span><span class="sxs-lookup"><span data-stu-id="4658d-225">Quotes</span></span>|
||<span data-ttu-id="4658d-226">Перекрестные публикации между каналами</span><span class="sxs-lookup"><span data-stu-id="4658d-226">Cross posts between channels</span></span>|

> [!div class="nextstepaction"]
>[<span data-ttu-id="4658d-227">Узнайте больше об интеграции Microsoft Graph и Teams</span><span class="sxs-lookup"><span data-stu-id="4658d-227">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
