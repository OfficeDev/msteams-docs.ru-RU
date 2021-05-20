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
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="aee7b-104">Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="aee7b-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="aee7b-105">С помощью Graph Microsoft можно перенести существующую историю сообщений пользователей и данные из внешней системы в Teams канал.</span><span class="sxs-lookup"><span data-stu-id="aee7b-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="aee7b-106">Позволяя воссоздать иерархию сторонних платформ обмена сообщениями внутри Teams, пользователи могут продолжать свои коммуникации бесшовно и действовать без перерыва.</span><span class="sxs-lookup"><span data-stu-id="aee7b-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="aee7b-107">В дальнейшем корпорация Майкрософт может потребовать у вас или ваших клиентов оплаты дополнительных сборов на основе количества импортированных данных.</span><span class="sxs-lookup"><span data-stu-id="aee7b-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="aee7b-108">Обзор импорта</span><span class="sxs-lookup"><span data-stu-id="aee7b-108">Import overview</span></span>

<span data-ttu-id="aee7b-109">На высоком уровне процесс импорта состоит из следующих:</span><span class="sxs-lookup"><span data-stu-id="aee7b-109">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="aee7b-110">Создайте команду с резервной во времени тайм-штамп</span><span class="sxs-lookup"><span data-stu-id="aee7b-110">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="aee7b-111">Создание канала с резервной во времени тайм-штамп</span><span class="sxs-lookup"><span data-stu-id="aee7b-111">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel) 
1. [<span data-ttu-id="aee7b-112">Импорт внешних устаревших сообщений</span><span class="sxs-lookup"><span data-stu-id="aee7b-112">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="aee7b-113">Завершить процесс миграции команды и канала</span><span class="sxs-lookup"><span data-stu-id="aee7b-113">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="aee7b-114">Добавление членов команды</span><span class="sxs-lookup"><span data-stu-id="aee7b-114">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="aee7b-115">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="aee7b-115">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="aee7b-116">Анализ и подготовка данных сообщений</span><span class="sxs-lookup"><span data-stu-id="aee7b-116">Analyze and prepare message data</span></span>

<span data-ttu-id="aee7b-117">✔ данные третьей стороны, чтобы решить, что будет перенесено.</span><span class="sxs-lookup"><span data-stu-id="aee7b-117">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="aee7b-118">✔ извлекаем выбранные данные из сторонняя система чата.</span><span class="sxs-lookup"><span data-stu-id="aee7b-118">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="aee7b-119">✔ Карта сторонняя структура чата в Teams структуры.</span><span class="sxs-lookup"><span data-stu-id="aee7b-119">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="aee7b-120">✔ преобразования данных импорта в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="aee7b-120">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="aee7b-121">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="aee7b-121">Set up your Office 365 tenant</span></span>

<span data-ttu-id="aee7b-122">✔, что Office 365 арендатора существует для данных об импорте.</span><span class="sxs-lookup"><span data-stu-id="aee7b-122">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="aee7b-123">Для получения дополнительной информации о настройке Office 365 аренды для Teams, [см Office 365.](../../concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="aee7b-123">For more information on setting up an Office 365 tenancy for Teams, see [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="aee7b-124">✔ убедитесь, что члены команды находятся Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="aee7b-124">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="aee7b-125">Для получения дополнительной информации [см Azure Active Directory.](/azure/active-directory/fundamentals/add-users-azure-active-directory)</span><span class="sxs-lookup"><span data-stu-id="aee7b-125">For more information, see [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="aee7b-126">Шаг первый: Создайте команду</span><span class="sxs-lookup"><span data-stu-id="aee7b-126">Step One: Create a team</span></span>

<span data-ttu-id="aee7b-127">Поскольку существующие данные мигрируют, поддержание исходных времен сообщения и предотвращение активности обмена сообщениями в процессе миграции являются ключом к воссозданию существующего потока сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="aee7b-127">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="aee7b-128">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="aee7b-128">This is achieved as follows:</span></span>

> <span data-ttu-id="aee7b-129">[Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) с резервной во времени timestamp с использованием свойства ресурсов  `createdDateTime`  команды.</span><span class="sxs-lookup"><span data-stu-id="aee7b-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="aee7b-130">Поместите новую команду `migration mode` в специальное состояние, которое запрещает пользователям большинство действий в команде до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="aee7b-130">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="aee7b-131">Включите атрибут `teamCreationMode` экземпляра со `migration` значением в запрос POST, чтобы явно определить новую группу как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="aee7b-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> [!Note]
> <span data-ttu-id="aee7b-132">Поле `createdDateTime` будет заполнено только для экземпляров группы или канала, которые были перенесены.</span><span class="sxs-lookup"><span data-stu-id="aee7b-132">The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="aee7b-133">Разрешения</span><span class="sxs-lookup"><span data-stu-id="aee7b-133">Permissions</span></span>

|<span data-ttu-id="aee7b-134">ОбластьИмя</span><span class="sxs-lookup"><span data-stu-id="aee7b-134">ScopeName</span></span>|<span data-ttu-id="aee7b-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="aee7b-135">DisplayName</span></span>|<span data-ttu-id="aee7b-136">Описание</span><span class="sxs-lookup"><span data-stu-id="aee7b-136">Description</span></span>|<span data-ttu-id="aee7b-137">Тип</span><span class="sxs-lookup"><span data-stu-id="aee7b-137">Type</span></span>|<span data-ttu-id="aee7b-138">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="aee7b-138">Admin Consent?</span></span>|<span data-ttu-id="aee7b-139">Объекты/API, охватываемые</span><span class="sxs-lookup"><span data-stu-id="aee7b-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="aee7b-140">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="aee7b-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="aee7b-141">Создание, управление ресурсами для миграции в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="aee7b-141">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="aee7b-142">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="aee7b-142">**Application-only**</span></span>|<span data-ttu-id="aee7b-143">**Да**</span><span class="sxs-lookup"><span data-stu-id="aee7b-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="aee7b-144">Запрос (создание группы в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="aee7b-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="aee7b-145">Отклик</span><span class="sxs-lookup"><span data-stu-id="aee7b-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-messages"></a><span data-ttu-id="aee7b-146">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="aee7b-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="aee7b-147">`createdDateTime`  набор для будущего.</span><span class="sxs-lookup"><span data-stu-id="aee7b-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="aee7b-148">`createdDateTime`  правильно указано, но атрибут `teamCreationMode`  экземпляра отсутствует или устанавливается на недействительное значение.</span><span class="sxs-lookup"><span data-stu-id="aee7b-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="aee7b-149">Шаг первый: Создание канала</span><span class="sxs-lookup"><span data-stu-id="aee7b-149">Step Two: Create a channel</span></span>

<span data-ttu-id="aee7b-150">Создание канала для импортированных сообщений аналогично сценарию группы создания:</span><span class="sxs-lookup"><span data-stu-id="aee7b-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="aee7b-151">[Создайте новый канал](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) с резервной во времени timestamp с использованием свойства ресурса `createdDateTime` канала.</span><span class="sxs-lookup"><span data-stu-id="aee7b-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="aee7b-152">Поместите новый канал в `migration mode` специальное состояние, которое запрещает пользователям большинство действий чата в канале до завершения процесса миграции.</span><span class="sxs-lookup"><span data-stu-id="aee7b-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="aee7b-153">Включите атрибут `channelCreationMode` экземпляра со `migration` значением в запрос POST, чтобы явно определить новую группу как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="aee7b-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="aee7b-154">Разрешения</span><span class="sxs-lookup"><span data-stu-id="aee7b-154">Permissions</span></span>

|<span data-ttu-id="aee7b-155">ОбластьИмя</span><span class="sxs-lookup"><span data-stu-id="aee7b-155">ScopeName</span></span>|<span data-ttu-id="aee7b-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="aee7b-156">DisplayName</span></span>|<span data-ttu-id="aee7b-157">Описание</span><span class="sxs-lookup"><span data-stu-id="aee7b-157">Description</span></span>|<span data-ttu-id="aee7b-158">Тип</span><span class="sxs-lookup"><span data-stu-id="aee7b-158">Type</span></span>|<span data-ttu-id="aee7b-159">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="aee7b-159">Admin Consent?</span></span>|<span data-ttu-id="aee7b-160">Объекты/API, охватываемые</span><span class="sxs-lookup"><span data-stu-id="aee7b-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="aee7b-161">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="aee7b-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="aee7b-162">Создание, управление ресурсами для миграции в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="aee7b-162">Creating, managing resources for migration to Microsoft Teams.</span></span>|<span data-ttu-id="aee7b-163">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="aee7b-163">**Application-only**</span></span>|<span data-ttu-id="aee7b-164">**Да**</span><span class="sxs-lookup"><span data-stu-id="aee7b-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="aee7b-165">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="aee7b-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="aee7b-166">Отклик</span><span class="sxs-lookup"><span data-stu-id="aee7b-166">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="aee7b-167">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="aee7b-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="aee7b-168">`createdDateTime`  набор для будущего.</span><span class="sxs-lookup"><span data-stu-id="aee7b-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="aee7b-169">`createdDateTime`  правильно указанный, но атрибут `channelCreationMode`  экземпляра отсутствует или устанавливается на недействительное значение.</span><span class="sxs-lookup"><span data-stu-id="aee7b-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="aee7b-170">Шаг третий: Импортные сообщения</span><span class="sxs-lookup"><span data-stu-id="aee7b-170">Step Three: Import messages</span></span>

<span data-ttu-id="aee7b-171">После создания команды и канала можно начать отправлять сообщения, которые отправляются с помощью `createdDateTime`  ключей `from`  и ключей в корпусе запроса.</span><span class="sxs-lookup"><span data-stu-id="aee7b-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="aee7b-172">**ПРИМЕЧАНИЕ**: сообщения, импортированные `createdDateTime` раньше, чем поток `createdDateTime` сообщений, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="aee7b-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="aee7b-173">`createdDateTime` должны быть уникальными в сообщениях в одном потоке.</span><span class="sxs-lookup"><span data-stu-id="aee7b-173">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="aee7b-174">`createdDateTime` поддерживает время метки с точностью миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="aee7b-174">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="aee7b-175">Например, если входящее сообщение запроса `createdDateTime` имеет значение набора как *2020-09-16T05:50:31.0025302*, то оно будет преобразовано *в 2020-09-16T05:50:31.002* , когда сообщение попадает.</span><span class="sxs-lookup"><span data-stu-id="aee7b-175">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="aee7b-176">Запрос (POST сообщение, которое является текстовым)</span><span class="sxs-lookup"><span data-stu-id="aee7b-176">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="aee7b-177">Отклик</span><span class="sxs-lookup"><span data-stu-id="aee7b-177">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="aee7b-178">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="aee7b-178">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="aee7b-179">Запрос (POST сообщение с изображением в ряд)</span><span class="sxs-lookup"><span data-stu-id="aee7b-179">Request (POST a message with inline image)</span></span>

> [!Note]
> <span data-ttu-id="aee7b-180">В этом сценарии нет специальных областей разрешений, так как запрос является частью chatMessage; области для chatMessage применяются и здесь.</span><span class="sxs-lookup"><span data-stu-id="aee7b-180">There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="aee7b-181">Отклик</span><span class="sxs-lookup"><span data-stu-id="aee7b-181">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="aee7b-182">Шаг четвертый: Полный режим миграции</span><span class="sxs-lookup"><span data-stu-id="aee7b-182">Step Four: Complete migration mode</span></span>

<span data-ttu-id="aee7b-183">После завершения процесса миграции сообщений команда и канал выходят из режима миграции с помощью  `completeMigration`  метода.</span><span class="sxs-lookup"><span data-stu-id="aee7b-183">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="aee7b-184">Этот шаг открывает ресурсы команды и канала для общего использования членами команды.</span><span class="sxs-lookup"><span data-stu-id="aee7b-184">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="aee7b-185">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="aee7b-185">The action is bound to the `team` instance.</span></span> <span data-ttu-id="aee7b-186">Все каналы должны быть завершены из режима миграции, прежде чем команда может быть завершена.</span><span class="sxs-lookup"><span data-stu-id="aee7b-186">All channels must be completed out of migration mode before the team can be completed.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="aee7b-187">Запрос (режим миграции конца канала)</span><span class="sxs-lookup"><span data-stu-id="aee7b-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="aee7b-188">Отклик</span><span class="sxs-lookup"><span data-stu-id="aee7b-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="aee7b-189">Запрос (режим миграции команды)</span><span class="sxs-lookup"><span data-stu-id="aee7b-189">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="aee7b-190">Отклик</span><span class="sxs-lookup"><span data-stu-id="aee7b-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

* <span data-ttu-id="aee7b-191">Действия, называемые `team` или которые не в `channel` `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="aee7b-191">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="aee7b-192">Шаг пятый: Добавить членов команды</span><span class="sxs-lookup"><span data-stu-id="aee7b-192">Step Five: Add team members</span></span>

<span data-ttu-id="aee7b-193">Вы можете добавить члена в группу, [используя пользовательский Teams или](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) Microsoft Graph [Добавить API-участника:](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="aee7b-193">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="aee7b-194">Запрос (добавить участника)</span><span class="sxs-lookup"><span data-stu-id="aee7b-194">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="aee7b-195">Отклик</span><span class="sxs-lookup"><span data-stu-id="aee7b-195">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="aee7b-196">Советы и дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="aee7b-196">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="aee7b-197">После `completeMigration` того, как запрос сделан, вы не можете импортировать дополнительные сообщения в группу.</span><span class="sxs-lookup"><span data-stu-id="aee7b-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="aee7b-198">Члены группы могут быть добавлены в новую группу только после `completeMigration` того, как запрос получил успешный ответ.</span><span class="sxs-lookup"><span data-stu-id="aee7b-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="aee7b-199">Регулирование: Сообщения импортируются по 5 RPS за канал.</span><span class="sxs-lookup"><span data-stu-id="aee7b-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="aee7b-200">Если необходимо внести коррективы в результаты миграции, необходимо удалить группу и повторить шаги по созданию команды и канала и повторной миграции сообщений.</span><span class="sxs-lookup"><span data-stu-id="aee7b-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="aee7b-201">В настоящее время вкошенные изображения являются единственным типом средств массовой информации, поддерживаемых схемой API сообщений импорта.</span><span class="sxs-lookup"><span data-stu-id="aee7b-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="aee7b-202">Область импортного контента</span><span class="sxs-lookup"><span data-stu-id="aee7b-202">Import content scope</span></span>

|<span data-ttu-id="aee7b-203">В сфере охвата</span><span class="sxs-lookup"><span data-stu-id="aee7b-203">In-scope</span></span> | <span data-ttu-id="aee7b-204">В настоящее время вне сферы охвата</span><span class="sxs-lookup"><span data-stu-id="aee7b-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="aee7b-205">Сообщения команд и каналов</span><span class="sxs-lookup"><span data-stu-id="aee7b-205">Team and channel messages</span></span>|<span data-ttu-id="aee7b-206">1:1 и групповые сообщения чата</span><span class="sxs-lookup"><span data-stu-id="aee7b-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="aee7b-207">Создано время исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="aee7b-207">Created time of the original message</span></span>|<span data-ttu-id="aee7b-208">Частные каналы</span><span class="sxs-lookup"><span data-stu-id="aee7b-208">Private channels</span></span>|
|<span data-ttu-id="aee7b-209">Вколинные изображения как часть сообщения</span><span class="sxs-lookup"><span data-stu-id="aee7b-209">Inline images as part of the message</span></span>|<span data-ttu-id="aee7b-210">При упоминаниях</span><span class="sxs-lookup"><span data-stu-id="aee7b-210">At mentions</span></span>|
|<span data-ttu-id="aee7b-211">Ссылки на существующие файлы в SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="aee7b-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="aee7b-212">Реакции</span><span class="sxs-lookup"><span data-stu-id="aee7b-212">Reactions</span></span>|
|<span data-ttu-id="aee7b-213">Сообщения с богатым текстом</span><span class="sxs-lookup"><span data-stu-id="aee7b-213">Messages with rich text</span></span>|<span data-ttu-id="aee7b-214">Видео</span><span class="sxs-lookup"><span data-stu-id="aee7b-214">Videos</span></span>|
|<span data-ttu-id="aee7b-215">Цепочка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="aee7b-215">Message reply chain</span></span>|<span data-ttu-id="aee7b-216">Объявления</span><span class="sxs-lookup"><span data-stu-id="aee7b-216">Announcements</span></span>|
|<span data-ttu-id="aee7b-217">Высокая пропускная способность</span><span class="sxs-lookup"><span data-stu-id="aee7b-217">High throughput processing</span></span>|<span data-ttu-id="aee7b-218">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="aee7b-218">Code snippets</span></span>|
||<span data-ttu-id="aee7b-219">Наклейки</span><span class="sxs-lookup"><span data-stu-id="aee7b-219">Stickers</span></span>|
||<span data-ttu-id="aee7b-220">Эмодзи</span><span class="sxs-lookup"><span data-stu-id="aee7b-220">Emojis</span></span>|
||<span data-ttu-id="aee7b-221">Цитаты</span><span class="sxs-lookup"><span data-stu-id="aee7b-221">Quotes</span></span>|
||<span data-ttu-id="aee7b-222">Кросс-посты между каналами</span><span class="sxs-lookup"><span data-stu-id="aee7b-222">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="aee7b-223">См. также</span><span class="sxs-lookup"><span data-stu-id="aee7b-223">See also</span></span>

[<span data-ttu-id="aee7b-224">Узнайте больше об интеграции Graph и Teams Майкрософт</span><span class="sxs-lookup"><span data-stu-id="aee7b-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
