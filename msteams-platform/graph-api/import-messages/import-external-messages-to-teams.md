---
title: Использование Microsoft Graph для импорта сообщений внешней платформы в Teams
description: Описывает, как использовать Microsoft Graph для импорта сообщений с внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: группы импортируют сообщения api graph Microsoft migrate migration post
ms.openlocfilehash: 1b5a8ccc243c795801552519b4b52f51366e047d
ms.sourcegitcommit: c9446200b8e76fbd434d012dc11dd9f191776d13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2021
ms.locfileid: "51403971"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="5cc97-104">Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="5cc97-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

<span data-ttu-id="5cc97-105">С помощью Microsoft Graph можно перенести существующую историю сообщений и данные пользователей из внешней системы в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc97-105">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="5cc97-106">Включив воссоздание иерархии сообщений сторонних платформ внутри Teams, пользователи могут беспрепятственно продолжать общение и действовать без прерывания.</span><span class="sxs-lookup"><span data-stu-id="5cc97-106">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="5cc97-107">В дальнейшем корпорация Майкрософт может потребовать у вас или ваших клиентов оплаты дополнительных сборов на основе количества импортированных данных.</span><span class="sxs-lookup"><span data-stu-id="5cc97-107">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="5cc97-108">Обзор импорта</span><span class="sxs-lookup"><span data-stu-id="5cc97-108">Import overview</span></span>

<span data-ttu-id="5cc97-109">На высоком уровне процесс импорта состоит из следующих:</span><span class="sxs-lookup"><span data-stu-id="5cc97-109">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="5cc97-110">Создание команды с помощью back-in-time timestamp</span><span class="sxs-lookup"><span data-stu-id="5cc97-110">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="5cc97-111">Создание канала с помощью back-in-timestamp</span><span class="sxs-lookup"><span data-stu-id="5cc97-111">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="5cc97-112">Импорт внешних датируемых сообщений в обратном времени</span><span class="sxs-lookup"><span data-stu-id="5cc97-112">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="5cc97-113">Завершение процесса миграции группы и канала</span><span class="sxs-lookup"><span data-stu-id="5cc97-113">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="5cc97-114">Добавление членов группы</span><span class="sxs-lookup"><span data-stu-id="5cc97-114">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="5cc97-115">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="5cc97-115">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="5cc97-116">Анализ и подготовка данных сообщений</span><span class="sxs-lookup"><span data-stu-id="5cc97-116">Analyze and prepare message data</span></span>

<span data-ttu-id="5cc97-117">✔ просмотрите сторонние данные, чтобы определить, что будет перенесено.</span><span class="sxs-lookup"><span data-stu-id="5cc97-117">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="5cc97-118">✔ извлекать выбранные данные из системы сторонних чатов.</span><span class="sxs-lookup"><span data-stu-id="5cc97-118">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="5cc97-119">✔ на карте структуру сторонних чатов в структуру Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc97-119">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="5cc97-120">✔ импорт данных в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="5cc97-120">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="5cc97-121">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="5cc97-121">Set up your Office 365 tenant</span></span>

<span data-ttu-id="5cc97-122">✔ убедитесь, что клиент Office 365 существует для данных импорта.</span><span class="sxs-lookup"><span data-stu-id="5cc97-122">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="5cc97-123">Дополнительные сведения о настройке аренды Office 365 для Teams см. в статью "Подготовка клиента [Office 365".](../../concepts/build-and-test/prepare-your-o365-tenant.md) </span><span class="sxs-lookup"><span data-stu-id="5cc97-123">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="5cc97-124">✔ убедитесь, что члены группы находятся в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="5cc97-124">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="5cc97-125">Дополнительные сведения *см.* [в добавлении нового пользователя в](/azure/active-directory/fundamentals/add-users-azure-active-directory) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5cc97-125">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="5cc97-126">Шаг первый: создание команды</span><span class="sxs-lookup"><span data-stu-id="5cc97-126">Step One: Create a team</span></span>

<span data-ttu-id="5cc97-127">Так как существующие данные переносят, сохранение исходных периодов времени отправки сообщений и предотвращение активности обмена сообщениями в процессе миграции являются ключом к воссозданию существующего потока сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="5cc97-127">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="5cc97-128">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5cc97-128">This is achieved as follows:</span></span>

> <span data-ttu-id="5cc97-129">[Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) со временем, используя свойство ресурсов  `createdDateTime`  группы.</span><span class="sxs-lookup"><span data-stu-id="5cc97-129">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="5cc97-130">Поместите новую команду в специальное состояние, которое не позволяет пользователям выполнить большинство действий в команде до завершения процесса `migration mode` миграции.</span><span class="sxs-lookup"><span data-stu-id="5cc97-130">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="5cc97-131">Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `teamCreationMode` `migration` как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="5cc97-131">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="5cc97-132">**ПРИМЕЧАНИЕ.** Поле будет заполнено только для экземпляров команды или канала, которые `createdDateTime` были перенесены.</span><span class="sxs-lookup"><span data-stu-id="5cc97-132">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="5cc97-133">Разрешения</span><span class="sxs-lookup"><span data-stu-id="5cc97-133">Permissions</span></span>

|<span data-ttu-id="5cc97-134">ScopeName</span><span class="sxs-lookup"><span data-stu-id="5cc97-134">ScopeName</span></span>|<span data-ttu-id="5cc97-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="5cc97-135">DisplayName</span></span>|<span data-ttu-id="5cc97-136">Описание</span><span class="sxs-lookup"><span data-stu-id="5cc97-136">Description</span></span>|<span data-ttu-id="5cc97-137">Тип</span><span class="sxs-lookup"><span data-stu-id="5cc97-137">Type</span></span>|<span data-ttu-id="5cc97-138">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="5cc97-138">Admin Consent?</span></span>|<span data-ttu-id="5cc97-139">Объекты/API, охваченные</span><span class="sxs-lookup"><span data-stu-id="5cc97-139">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="5cc97-140">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5cc97-140">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="5cc97-141">Создание и управление ресурсами для миграции в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5cc97-141">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="5cc97-142">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="5cc97-142">**Application-only**</span></span>|<span data-ttu-id="5cc97-143">**Да**</span><span class="sxs-lookup"><span data-stu-id="5cc97-143">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="5cc97-144">Запрос (создание группы в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="5cc97-144">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="5cc97-145">Отклик</span><span class="sxs-lookup"><span data-stu-id="5cc97-145">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-messages"></a><span data-ttu-id="5cc97-146">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="5cc97-146">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="5cc97-147">`createdDateTime`  установлено на будущее.</span><span class="sxs-lookup"><span data-stu-id="5cc97-147">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="5cc97-148">`createdDateTime`  правильно задан, но `teamCreationMode`  атрибут экземпляра отсутствует или задан для значения недействительным.</span><span class="sxs-lookup"><span data-stu-id="5cc97-148">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="5cc97-149">Шаг второй: создание канала</span><span class="sxs-lookup"><span data-stu-id="5cc97-149">Step Two: Create a channel</span></span>

<span data-ttu-id="5cc97-150">Создание канала для импортируемых сообщений аналогично сценарию создания группы:</span><span class="sxs-lookup"><span data-stu-id="5cc97-150">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="5cc97-151">[Создайте новый канал](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) с использованием свойства ресурса канала с помощью функции timestamp в обратном `createdDateTime` времени.</span><span class="sxs-lookup"><span data-stu-id="5cc97-151">[Create a new channel](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="5cc97-152">Поместите новый канал в специальное состояние, которое не позволяет пользователям от большинства действий чата в канале до завершения процесса `migration mode` миграции.</span><span class="sxs-lookup"><span data-stu-id="5cc97-152">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="5cc97-153">Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `channelCreationMode` `migration` как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="5cc97-153">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="5cc97-154">Разрешения</span><span class="sxs-lookup"><span data-stu-id="5cc97-154">Permissions</span></span>

|<span data-ttu-id="5cc97-155">ScopeName</span><span class="sxs-lookup"><span data-stu-id="5cc97-155">ScopeName</span></span>|<span data-ttu-id="5cc97-156">DisplayName</span><span class="sxs-lookup"><span data-stu-id="5cc97-156">DisplayName</span></span>|<span data-ttu-id="5cc97-157">Описание</span><span class="sxs-lookup"><span data-stu-id="5cc97-157">Description</span></span>|<span data-ttu-id="5cc97-158">Тип</span><span class="sxs-lookup"><span data-stu-id="5cc97-158">Type</span></span>|<span data-ttu-id="5cc97-159">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="5cc97-159">Admin Consent?</span></span>|<span data-ttu-id="5cc97-160">Объекты/API, охваченные</span><span class="sxs-lookup"><span data-stu-id="5cc97-160">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="5cc97-161">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5cc97-161">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="5cc97-162">Создание и управление ресурсами для миграции в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="5cc97-162">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="5cc97-163">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="5cc97-163">**Application-only**</span></span>|<span data-ttu-id="5cc97-164">**Да**</span><span class="sxs-lookup"><span data-stu-id="5cc97-164">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="5cc97-165">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="5cc97-165">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="5cc97-166">Отклик</span><span class="sxs-lookup"><span data-stu-id="5cc97-166">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="5cc97-167">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="5cc97-167">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="5cc97-168">`createdDateTime`  установлено на будущее.</span><span class="sxs-lookup"><span data-stu-id="5cc97-168">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="5cc97-169">`createdDateTime`  правильно задан, но `channelCreationMode`  атрибут экземпляра отсутствует или задан для значения недействительным.</span><span class="sxs-lookup"><span data-stu-id="5cc97-169">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="5cc97-170">Шаг 3. Импорт сообщений</span><span class="sxs-lookup"><span data-stu-id="5cc97-170">Step Three: Import messages</span></span>

<span data-ttu-id="5cc97-171">После создания группы и канала можно приступить к отправке сообщений в обратном времени с помощью ключей и ключей в `createdDateTime` `from`  тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="5cc97-171">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="5cc97-172">**ПРИМЕЧАНИЕ.** Сообщения, импортируемые с более ранним `createdDateTime` потоком `createdDateTime` сообщений, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="5cc97-172">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="5cc97-173">`createdDateTime` должны быть уникальными для сообщений в одном потоке.</span><span class="sxs-lookup"><span data-stu-id="5cc97-173">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="5cc97-174">`createdDateTime` поддерживает периоды времени с точностью миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="5cc97-174">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="5cc97-175">Например, если входящий запрос сообщения имеет значение set `createdDateTime` as *2020-09-16T05:50:31.0025302Z,* то оно будет преобразовано в *2020-09-16T05:50:31.002Z,* когда сообщение будет ingested.</span><span class="sxs-lookup"><span data-stu-id="5cc97-175">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="5cc97-176">Запрос (сообщение POST, которое является текстовым)</span><span class="sxs-lookup"><span data-stu-id="5cc97-176">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="5cc97-177">Отклик</span><span class="sxs-lookup"><span data-stu-id="5cc97-177">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="5cc97-178">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="5cc97-178">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="5cc97-179">Запрос (СООБЩЕНИЕ сообщения с inline image)</span><span class="sxs-lookup"><span data-stu-id="5cc97-179">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="5cc97-180">**Примечание.** В этом сценарии нет специальных областей разрешений, так как запрос является частью chatMessage; Области для chatMessage применяются и здесь.</span><span class="sxs-lookup"><span data-stu-id="5cc97-180">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="5cc97-181">Отклик</span><span class="sxs-lookup"><span data-stu-id="5cc97-181">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="5cc97-182">Шаг 4. Полный режим миграции</span><span class="sxs-lookup"><span data-stu-id="5cc97-182">Step Four: Complete migration mode</span></span>

<span data-ttu-id="5cc97-183">После завершения процесса миграции сообщений команда и канал вывели из режима миграции с помощью  `completeMigration`  метода.</span><span class="sxs-lookup"><span data-stu-id="5cc97-183">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="5cc97-184">Этот шаг открывает ресурсы команды и канала для общего использования членами группы.</span><span class="sxs-lookup"><span data-stu-id="5cc97-184">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="5cc97-185">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="5cc97-185">The action is bound to the `team` instance.</span></span> <span data-ttu-id="5cc97-186">Все каналы должны быть завершены из режима миграции, прежде чем команда может быть завершена.</span><span class="sxs-lookup"><span data-stu-id="5cc97-186">All channels must be completed out of migration mode before the team can be completed.</span></span>

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="5cc97-187">Запрос (режим переноса конечных каналов)</span><span class="sxs-lookup"><span data-stu-id="5cc97-187">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a><span data-ttu-id="5cc97-188">Отклик</span><span class="sxs-lookup"><span data-stu-id="5cc97-188">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="5cc97-189">Запрос (режим миграции конечных команд)</span><span class="sxs-lookup"><span data-stu-id="5cc97-189">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a><span data-ttu-id="5cc97-190">Отклик</span><span class="sxs-lookup"><span data-stu-id="5cc97-190">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

* <span data-ttu-id="5cc97-191">Действие, которое `team` вызвано или `channel` которое не в `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="5cc97-191">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="5cc97-192">Шаг 5. Добавление членов группы</span><span class="sxs-lookup"><span data-stu-id="5cc97-192">Step Five: Add team members</span></span>

<span data-ttu-id="5cc97-193">Вы можете добавить участника в группу с [помощью API UI teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) или Microsoft Graph [Add:](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="5cc97-193">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="5cc97-194">Запрос (добавление участника)</span><span class="sxs-lookup"><span data-stu-id="5cc97-194">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="5cc97-195">Отклик</span><span class="sxs-lookup"><span data-stu-id="5cc97-195">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="5cc97-196">Советы и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="5cc97-196">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="5cc97-197">После запроса нельзя импортировать дополнительные сообщения `completeMigration` в команду.</span><span class="sxs-lookup"><span data-stu-id="5cc97-197">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="5cc97-198">Члены группы могут быть добавлены в новую команду только после успешного ответа на `completeMigration` запрос.</span><span class="sxs-lookup"><span data-stu-id="5cc97-198">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="5cc97-199">Регулирование: импорт сообщений по 5 RPS на канал.</span><span class="sxs-lookup"><span data-stu-id="5cc97-199">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="5cc97-200">Если необходимо внести исправление в результаты миграции, необходимо удалить команду и повторить действия по созданию группы и каналу и повторной миграции сообщений.</span><span class="sxs-lookup"><span data-stu-id="5cc97-200">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="5cc97-201">В настоящее время inline images are the only type of media supported by the import message API schpi.</span><span class="sxs-lookup"><span data-stu-id="5cc97-201">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="5cc97-202">Область импорта контента</span><span class="sxs-lookup"><span data-stu-id="5cc97-202">Import content scope</span></span>

|<span data-ttu-id="5cc97-203">В области</span><span class="sxs-lookup"><span data-stu-id="5cc97-203">In-scope</span></span> | <span data-ttu-id="5cc97-204">В настоящее время вне области</span><span class="sxs-lookup"><span data-stu-id="5cc97-204">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="5cc97-205">Сообщения группы и канала</span><span class="sxs-lookup"><span data-stu-id="5cc97-205">Team and channel messages</span></span>|<span data-ttu-id="5cc97-206">1:1 и групповые сообщения чата</span><span class="sxs-lookup"><span data-stu-id="5cc97-206">1:1 and group chat messages</span></span>|
|<span data-ttu-id="5cc97-207">Созданное время исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc97-207">Created time of the original message</span></span>|<span data-ttu-id="5cc97-208">Частные каналы</span><span class="sxs-lookup"><span data-stu-id="5cc97-208">Private channels</span></span>|
|<span data-ttu-id="5cc97-209">Inline images as part of the message</span><span class="sxs-lookup"><span data-stu-id="5cc97-209">Inline images as part of the message</span></span>|<span data-ttu-id="5cc97-210">При упоминаний</span><span class="sxs-lookup"><span data-stu-id="5cc97-210">At mentions</span></span>|
|<span data-ttu-id="5cc97-211">Ссылки на существующие файлы в SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="5cc97-211">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="5cc97-212">Реакции</span><span class="sxs-lookup"><span data-stu-id="5cc97-212">Reactions</span></span>|
|<span data-ttu-id="5cc97-213">Сообщения с богатым текстом</span><span class="sxs-lookup"><span data-stu-id="5cc97-213">Messages with rich text</span></span>|<span data-ttu-id="5cc97-214">Видео</span><span class="sxs-lookup"><span data-stu-id="5cc97-214">Videos</span></span>|
|<span data-ttu-id="5cc97-215">Цепочка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="5cc97-215">Message reply chain</span></span>|<span data-ttu-id="5cc97-216">Объявления</span><span class="sxs-lookup"><span data-stu-id="5cc97-216">Announcements</span></span>|
|<span data-ttu-id="5cc97-217">Обработка высокой пропускной способности</span><span class="sxs-lookup"><span data-stu-id="5cc97-217">High throughput processing</span></span>|<span data-ttu-id="5cc97-218">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="5cc97-218">Code snippets</span></span>|
||<span data-ttu-id="5cc97-219">Наклейки</span><span class="sxs-lookup"><span data-stu-id="5cc97-219">Stickers</span></span>|
||<span data-ttu-id="5cc97-220">Emojis</span><span class="sxs-lookup"><span data-stu-id="5cc97-220">Emojis</span></span>|
||<span data-ttu-id="5cc97-221">Котировки</span><span class="sxs-lookup"><span data-stu-id="5cc97-221">Quotes</span></span>|
||<span data-ttu-id="5cc97-222">Перекрестные сообщения между каналами</span><span class="sxs-lookup"><span data-stu-id="5cc97-222">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="5cc97-223">См. также</span><span class="sxs-lookup"><span data-stu-id="5cc97-223">See also</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="5cc97-224">Дополнительные данные об интеграции Microsoft Graph и Teams</span><span class="sxs-lookup"><span data-stu-id="5cc97-224">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
