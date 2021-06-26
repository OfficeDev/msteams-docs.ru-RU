---
title: Используйте microsoft Graph для импорта сообщений внешней платформы для Teams
description: Описывает, как использовать microsoft Graph для импорта сообщений с внешней платформы для Teams
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: группы импортируют сообщения api graph Microsoft migrate migration post
ms.openlocfilehash: 95cbf6bf2deac4ea71e60fe0fece06c1dd3ad24c
ms.sourcegitcommit: 656a1de9e23e0ad90dddcb93a2bbfcc63848a856
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53130096"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="8eacc-104">Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="8eacc-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="8eacc-105">С помощью microsoft Graph можно перенести существующую историю сообщений и данные пользователей из внешней системы в Teams канал.</span><span class="sxs-lookup"><span data-stu-id="8eacc-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="8eacc-106">Включив воссоздание иерархии обмена сообщениями сторонних платформ внутри Teams, пользователи могут беспрепятственно продолжать общение и действовать без прерывания.</span><span class="sxs-lookup"><span data-stu-id="8eacc-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE]
> <span data-ttu-id="8eacc-107">В дальнейшем корпорация Майкрософт может потребовать у вас или ваших клиентов оплаты дополнительных сборов на основе количества импортированных данных.</span><span class="sxs-lookup"><span data-stu-id="8eacc-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="8eacc-108">Обзор импорта</span><span class="sxs-lookup"><span data-stu-id="8eacc-108">Import overview</span></span>

<span data-ttu-id="8eacc-109">На высоком уровне процесс импорта состоит из следующих:</span><span class="sxs-lookup"><span data-stu-id="8eacc-109">At a high level, the import process consists of the following:</span></span>

1. <span data-ttu-id="8eacc-110">[Создайте команду с помощью back-in-timestamp](#step-1-create-a-team).</span><span class="sxs-lookup"><span data-stu-id="8eacc-110">[Create a team with a back-in-time timestamp](#step-1-create-a-team).</span></span>
1. <span data-ttu-id="8eacc-111">[Создайте канал со временем.](#step-2-create-a-channel)</span><span class="sxs-lookup"><span data-stu-id="8eacc-111">[Create a channel with a back-in-time timestamp](#step-2-create-a-channel).</span></span>
1. <span data-ttu-id="8eacc-112">[Импорт внешних сообщений,](#step-3-import-messages)датируемых временем.</span><span class="sxs-lookup"><span data-stu-id="8eacc-112">[Import external back-in-time dated messages](#step-3-import-messages).</span></span>
1. <span data-ttu-id="8eacc-113">[Завершите процесс миграции группы и канала.](#step-4-complete-migration-mode)</span><span class="sxs-lookup"><span data-stu-id="8eacc-113">[Complete the team and channel migration process](#step-4-complete-migration-mode).</span></span>
1. <span data-ttu-id="8eacc-114">[Добавление участников группы.](#step-five-add-team-members)</span><span class="sxs-lookup"><span data-stu-id="8eacc-114">[Add team members](#step-five-add-team-members).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8eacc-115">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="8eacc-115">Prerequisites</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="8eacc-116">Анализ и подготовка данных сообщений</span><span class="sxs-lookup"><span data-stu-id="8eacc-116">Analyze and prepare message data</span></span>

* <span data-ttu-id="8eacc-117">Просмотрите сторонние данные, чтобы определить, что будет перенесено.</span><span class="sxs-lookup"><span data-stu-id="8eacc-117">Review the third-party data to decide what will be migrated.</span></span>  
* <span data-ttu-id="8eacc-118">Извлечение выбранных данных из системы сторонних чатов.</span><span class="sxs-lookup"><span data-stu-id="8eacc-118">Extract the selected data from the third-party chat system.</span></span>  
* <span data-ttu-id="8eacc-119">Составить карту структуры сторонних чатов с Teams структурой.</span><span class="sxs-lookup"><span data-stu-id="8eacc-119">Map the third-party chat structure to the Teams structure.</span></span>  
* <span data-ttu-id="8eacc-120">Преобразование данных импорта в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="8eacc-120">Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="8eacc-121">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="8eacc-121">Set up your Office 365 tenant</span></span>

* <span data-ttu-id="8eacc-122">Убедитесь, что Office 365 клиент существует для данных импорта.</span><span class="sxs-lookup"><span data-stu-id="8eacc-122">Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="8eacc-123">Дополнительные сведения о настройке Office 365 аренды для Teams см. в Office 365 [клиента.](../../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="8eacc-123">For more information on setting up an Office 365 tenancy for Teams, see [prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
* <span data-ttu-id="8eacc-124">Убедитесь, что члены группы находятся в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="8eacc-124">Make sure that team members are in Azure Active Directory (AAD).</span></span> <span data-ttu-id="8eacc-125">Дополнительные сведения [см. в добавлении нового пользователя в](/azure/active-directory/fundamentals/add-users-azure-active-directory) AAD.</span><span class="sxs-lookup"><span data-stu-id="8eacc-125">For more information, see [add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to AAD.</span></span>

## <a name="step-1-create-a-team"></a><span data-ttu-id="8eacc-126">Шаг 1. Создание команды</span><span class="sxs-lookup"><span data-stu-id="8eacc-126">Step 1: Create a team</span></span>

<span data-ttu-id="8eacc-127">Так как вы переносили существующие данные, сохранение исходных периодов времени отправки сообщений и предотвращение активности обмена сообщениями в процессе миграции являются ключом к воссозданию существующего потока сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="8eacc-127">Since you are migrating existing data, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="8eacc-128">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8eacc-128">This is achieved as follows:</span></span>

> <span data-ttu-id="8eacc-129">[Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) со временем, используя свойство ресурсов `createdDateTime` группы.</span><span class="sxs-lookup"><span data-stu-id="8eacc-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource `createdDateTime` property.</span></span> <span data-ttu-id="8eacc-130">Поместите новую команду в специальное состояние, которое ограничивает пользователей от большинства действий в группе до завершения `migration mode` процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="8eacc-130">Place the new team in `migration mode`, a special state that restricts users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="8eacc-131">Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `teamCreationMode` `migration` как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="8eacc-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!NOTE]
> <span data-ttu-id="8eacc-132">Поле будет заполнено только для экземпляров команды или канала, которые `createdDateTime` были перенесены.</span><span class="sxs-lookup"><span data-stu-id="8eacc-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a><span data-ttu-id="8eacc-133">Разрешение</span><span class="sxs-lookup"><span data-stu-id="8eacc-133">Permission</span></span>

|<span data-ttu-id="8eacc-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="8eacc-134">ScopeName</span></span>|<span data-ttu-id="8eacc-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8eacc-135">DisplayName</span></span>|<span data-ttu-id="8eacc-136">Описание</span><span class="sxs-lookup"><span data-stu-id="8eacc-136">Description</span></span>|<span data-ttu-id="8eacc-137">Тип</span><span class="sxs-lookup"><span data-stu-id="8eacc-137">Type</span></span>|<span data-ttu-id="8eacc-138">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="8eacc-138">Admin Consent?</span></span>|<span data-ttu-id="8eacc-139">Объекты/API, охваченные</span><span class="sxs-lookup"><span data-stu-id="8eacc-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="8eacc-140">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8eacc-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="8eacc-141">Создание и управление ресурсами для миграции в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8eacc-141">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="8eacc-142">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="8eacc-142">**Application-only**</span></span>|<span data-ttu-id="8eacc-143">**Да**</span><span class="sxs-lookup"><span data-stu-id="8eacc-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="8eacc-144">Запрос (создание группы в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="8eacc-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8eacc-145">Отклик</span><span class="sxs-lookup"><span data-stu-id="8eacc-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a><span data-ttu-id="8eacc-146">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="8eacc-146">Error message</span></span>

```http
400 Bad Request
```

<span data-ttu-id="8eacc-147">Сообщение об ошибке можно получить в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="8eacc-147">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="8eacc-148">Если `createdDateTime` настроено на будущее.</span><span class="sxs-lookup"><span data-stu-id="8eacc-148">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="8eacc-149">Если `createdDateTime` правильно указано, но атрибут `teamCreationMode` экземпляра отсутствует или задан для значения недействительным.</span><span class="sxs-lookup"><span data-stu-id="8eacc-149">If `createdDateTime` is correctly specified, but `teamCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-2-create-a-channel"></a><span data-ttu-id="8eacc-150">Шаг 2. Создание канала</span><span class="sxs-lookup"><span data-stu-id="8eacc-150">Step 2: Create a channel</span></span>

<span data-ttu-id="8eacc-151">Создание канала для импортируемых сообщений аналогично сценарию создания группы:</span><span class="sxs-lookup"><span data-stu-id="8eacc-151">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="8eacc-152">[Создайте новый канал](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) с использованием свойства ресурса канала с помощью функции timestamp в обратном `createdDateTime` времени.</span><span class="sxs-lookup"><span data-stu-id="8eacc-152">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="8eacc-153">Поместите новый канал в специальное состояние, которое ограничивает пользователей от большинства действий чата в канале до завершения `migration mode` процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="8eacc-153">Place the new channel in `migration mode`, a special state that restricts users from most chat activities within the channel until the migration process is complete.</span></span> <span data-ttu-id="8eacc-154">Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `channelCreationMode` `migration` как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="8eacc-154">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a><span data-ttu-id="8eacc-155">Разрешение</span><span class="sxs-lookup"><span data-stu-id="8eacc-155">Permission</span></span>

|<span data-ttu-id="8eacc-156">ScopeName</span><span class="sxs-lookup"><span data-stu-id="8eacc-156">ScopeName</span></span>|<span data-ttu-id="8eacc-157">DisplayName</span><span class="sxs-lookup"><span data-stu-id="8eacc-157">DisplayName</span></span>|<span data-ttu-id="8eacc-158">Описание</span><span class="sxs-lookup"><span data-stu-id="8eacc-158">Description</span></span>|<span data-ttu-id="8eacc-159">Тип</span><span class="sxs-lookup"><span data-stu-id="8eacc-159">Type</span></span>|<span data-ttu-id="8eacc-160">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="8eacc-160">Admin Consent?</span></span>|<span data-ttu-id="8eacc-161">Объекты/API, охваченные</span><span class="sxs-lookup"><span data-stu-id="8eacc-161">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="8eacc-162">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8eacc-162">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="8eacc-163">Создание и управление ресурсами для миграции в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8eacc-163">Creating and managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="8eacc-164">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="8eacc-164">**Application-only**</span></span>|<span data-ttu-id="8eacc-165">**Да**</span><span class="sxs-lookup"><span data-stu-id="8eacc-165">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="8eacc-166">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="8eacc-166">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8eacc-167">Отклик</span><span class="sxs-lookup"><span data-stu-id="8eacc-167">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="8eacc-168">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="8eacc-168">Error message</span></span>

```http
400 Bad Request
```
<span data-ttu-id="8eacc-169">Сообщение об ошибке можно получить в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="8eacc-169">You can receive the error message in the following scenarios:</span></span>

* <span data-ttu-id="8eacc-170">Если `createdDateTime` настроено на будущее.</span><span class="sxs-lookup"><span data-stu-id="8eacc-170">If `createdDateTime` is set for future.</span></span>
* <span data-ttu-id="8eacc-171">Если `createdDateTime` правильно указано, но `channelCreationMode` атрибут экземпляра отсутствует или задан недействительным значением.</span><span class="sxs-lookup"><span data-stu-id="8eacc-171">If `createdDateTime` is correctly specified but `channelCreationMode` instance attribute is missing or set to invalid value.</span></span>

## <a name="step-3-import-messages"></a><span data-ttu-id="8eacc-172">Шаг 3. Импорт сообщений</span><span class="sxs-lookup"><span data-stu-id="8eacc-172">Step 3: Import messages</span></span>

<span data-ttu-id="8eacc-173">После создания группы и канала можно приступить к отправке сообщений в обратном времени с помощью ключей и ключей в `createdDateTime` `from` тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="8eacc-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from` keys in the request body.</span></span>

> [!NOTE]
> * <span data-ttu-id="8eacc-174">Сообщения, импортируемые с более `createdDateTime` ранним потоком `createdDateTime` сообщений, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="8eacc-174">Messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>
> * <span data-ttu-id="8eacc-175">`createdDateTime` должны быть уникальными для сообщений в одном потоке.</span><span class="sxs-lookup"><span data-stu-id="8eacc-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="8eacc-176">`createdDateTime` поддерживает периоды времени с точностью миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="8eacc-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="8eacc-177">Например, если входящий запрос сообщения имеет значение set `createdDateTime` as *2020-09-16T05:50:31.0025302Z,* то оно будет преобразовано в *2020-09-16T05:50:31.002Z,* когда сообщение будет ingested.</span><span class="sxs-lookup"><span data-stu-id="8eacc-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="8eacc-178">Запрос (сообщение POST, которое является текстовым)</span><span class="sxs-lookup"><span data-stu-id="8eacc-178">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8eacc-179">Отклик</span><span class="sxs-lookup"><span data-stu-id="8eacc-179">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="8eacc-180">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="8eacc-180">Error message</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="8eacc-181">Запрос (СООБЩЕНИЕ сообщения с inline image)</span><span class="sxs-lookup"><span data-stu-id="8eacc-181">Request (POST a message with inline image)</span></span>

> [!NOTE]
> * <span data-ttu-id="8eacc-182">В этом сценарии нет специальных областей разрешений, так как запрос является частью `chatMessage` .</span><span class="sxs-lookup"><span data-stu-id="8eacc-182">There are no special permission scopes in this scenario since the request is part of `chatMessage`.</span></span>
> * <span data-ttu-id="8eacc-183">Области применения `chatMessage` здесь.</span><span class="sxs-lookup"><span data-stu-id="8eacc-183">The scopes for `chatMessage` apply here.</span></span>

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

#### <a name="response"></a><span data-ttu-id="8eacc-184">Отклик</span><span class="sxs-lookup"><span data-stu-id="8eacc-184">Response</span></span>

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

## <a name="step-4-complete-migration-mode"></a><span data-ttu-id="8eacc-185">Шаг 4. Полный режим миграции</span><span class="sxs-lookup"><span data-stu-id="8eacc-185">Step 4: Complete migration mode</span></span>

<span data-ttu-id="8eacc-186">После завершения процесса миграции сообщений команда и канал вывели из режима миграции с помощью  `completeMigration` метода.</span><span class="sxs-lookup"><span data-stu-id="8eacc-186">After the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration` method.</span></span> <span data-ttu-id="8eacc-187">Этот шаг открывает ресурсы команды и канала для общего использования членами группы.</span><span class="sxs-lookup"><span data-stu-id="8eacc-187">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="8eacc-188">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="8eacc-188">The action is bound to the `team` instance.</span></span> <span data-ttu-id="8eacc-189">Перед завершением работы группы все каналы должны быть завершены из режима миграции.</span><span class="sxs-lookup"><span data-stu-id="8eacc-189">Before the team completes, all channels must be completed out of migration mode.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="8eacc-190">Запрос (режим переноса конечных каналов)</span><span class="sxs-lookup"><span data-stu-id="8eacc-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="8eacc-191">Отклик</span><span class="sxs-lookup"><span data-stu-id="8eacc-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="8eacc-192">Запрос (режим миграции конечных команд)</span><span class="sxs-lookup"><span data-stu-id="8eacc-192">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="8eacc-193">Отклик</span><span class="sxs-lookup"><span data-stu-id="8eacc-193">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

<span data-ttu-id="8eacc-194">Действие, которое `team` вызвано или `channel` которое не в `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="8eacc-194">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="8eacc-195">Шаг 5. Добавление членов группы</span><span class="sxs-lookup"><span data-stu-id="8eacc-195">Step five: Add team members</span></span>

<span data-ttu-id="8eacc-196">Вы можете добавить участника в команду с помощью [пользовательского Teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) или Microsoft Graph API [участника:](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="8eacc-196">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="8eacc-197">Запрос (добавление участника)</span><span class="sxs-lookup"><span data-stu-id="8eacc-197">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="8eacc-198">Отклик</span><span class="sxs-lookup"><span data-stu-id="8eacc-198">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="8eacc-199">Советы и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="8eacc-199">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="8eacc-200">После запроса нельзя импортировать дополнительные сообщения `completeMigration` в команду.</span><span class="sxs-lookup"><span data-stu-id="8eacc-200">After the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="8eacc-201">Вы можете добавить членов группы в новую команду только после успешного ответа на `completeMigration` запрос.</span><span class="sxs-lookup"><span data-stu-id="8eacc-201">You can only add team members to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="8eacc-202">Регулирование. Импорт сообщений по пять RPS на канал.</span><span class="sxs-lookup"><span data-stu-id="8eacc-202">Throttling: Messages import at five RPS per channel.</span></span>

* <span data-ttu-id="8eacc-203">Если требуется внести исправление в результаты миграции, необходимо удалить команду и повторить действия по созданию группы и каналу и повторной миграции сообщений.</span><span class="sxs-lookup"><span data-stu-id="8eacc-203">If you need to make a correction to the migration results, you must delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="8eacc-204">В настоящее время inline images are the only type of media supported by the import message API schpi.</span><span class="sxs-lookup"><span data-stu-id="8eacc-204">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="8eacc-205">Область импорта контента</span><span class="sxs-lookup"><span data-stu-id="8eacc-205">Import content scope</span></span>

<span data-ttu-id="8eacc-206">В следующей таблице содержится область контента:</span><span class="sxs-lookup"><span data-stu-id="8eacc-206">The following table provides the content scope:</span></span>

|<span data-ttu-id="8eacc-207">В области</span><span class="sxs-lookup"><span data-stu-id="8eacc-207">In-scope</span></span> | <span data-ttu-id="8eacc-208">В настоящее время вне области</span><span class="sxs-lookup"><span data-stu-id="8eacc-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="8eacc-209">Сообщения группы и канала</span><span class="sxs-lookup"><span data-stu-id="8eacc-209">Team and channel messages</span></span>|<span data-ttu-id="8eacc-210">1:1 и групповые сообщения чата</span><span class="sxs-lookup"><span data-stu-id="8eacc-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="8eacc-211">Созданное время исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="8eacc-211">Created time of the original message</span></span>|<span data-ttu-id="8eacc-212">Частные каналы</span><span class="sxs-lookup"><span data-stu-id="8eacc-212">Private channels</span></span>|
|<span data-ttu-id="8eacc-213">Inline images as part of the message</span><span class="sxs-lookup"><span data-stu-id="8eacc-213">Inline images as part of the message</span></span>|<span data-ttu-id="8eacc-214">При упоминаний</span><span class="sxs-lookup"><span data-stu-id="8eacc-214">At mentions</span></span>|
|<span data-ttu-id="8eacc-215">Ссылки на существующие файлы в SPO или OneDrive</span><span class="sxs-lookup"><span data-stu-id="8eacc-215">Links to existing files in SPO or OneDrive</span></span>|<span data-ttu-id="8eacc-216">Реакции</span><span class="sxs-lookup"><span data-stu-id="8eacc-216">Reactions</span></span>|
|<span data-ttu-id="8eacc-217">Сообщения с богатым текстом</span><span class="sxs-lookup"><span data-stu-id="8eacc-217">Messages with rich text</span></span>|<span data-ttu-id="8eacc-218">Видео</span><span class="sxs-lookup"><span data-stu-id="8eacc-218">Videos</span></span>|
|<span data-ttu-id="8eacc-219">Цепочка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="8eacc-219">Message reply chain</span></span>|<span data-ttu-id="8eacc-220">Объявления</span><span class="sxs-lookup"><span data-stu-id="8eacc-220">Announcements</span></span>|
|<span data-ttu-id="8eacc-221">Обработка высокой пропускной способности</span><span class="sxs-lookup"><span data-stu-id="8eacc-221">High throughput processing</span></span>|<span data-ttu-id="8eacc-222">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="8eacc-222">Code snippets</span></span>|
||<span data-ttu-id="8eacc-223">Наклейки</span><span class="sxs-lookup"><span data-stu-id="8eacc-223">Stickers</span></span>|
||<span data-ttu-id="8eacc-224">Emojis</span><span class="sxs-lookup"><span data-stu-id="8eacc-224">Emojis</span></span>|
||<span data-ttu-id="8eacc-225">Цитаты</span><span class="sxs-lookup"><span data-stu-id="8eacc-225">Quotes</span></span>|
||<span data-ttu-id="8eacc-226">Перекрестные сообщения между каналами</span><span class="sxs-lookup"><span data-stu-id="8eacc-226">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="8eacc-227">См. также</span><span class="sxs-lookup"><span data-stu-id="8eacc-227">See also</span></span>

[<span data-ttu-id="8eacc-228">Интеграция Graph и Teams Майкрософт</span><span class="sxs-lookup"><span data-stu-id="8eacc-228">Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
