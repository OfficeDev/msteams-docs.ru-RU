---
title: Использование Microsoft Graph для импорта сообщений внешней платформы в Teams
description: Описывает, как использовать Microsoft Graph для импорта сообщений с внешней платформы в Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: группы импортируют сообщения api graph Microsoft migrate migration post
ms.openlocfilehash: 8cf4f964aba7ce9375b1b259ae88a7fbcb620631
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176958"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a><span data-ttu-id="15246-104">Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="15246-104">Import third-party platform messages to Teams using Microsoft Graph</span></span>

>[!IMPORTANT]
> <span data-ttu-id="15246-105">Общедоступные предварительные просмотры Microsoft Graph и Microsoft Teams доступны для раннего доступа и отзывов.</span><span class="sxs-lookup"><span data-stu-id="15246-105">Microsoft Graph and Microsoft Teams public previews are available for early-access and feedback.</span></span> <span data-ttu-id="15246-106">Хотя этот выпуск прошел широкое тестирование, он не предназначен для использования в производстве.</span><span class="sxs-lookup"><span data-stu-id="15246-106">Although this release has undergone extensive testing, it is not intended for use in production.</span></span>

<span data-ttu-id="15246-107">С помощью Microsoft Graph можно перенести существующую историю сообщений и данные пользователей из внешней системы в канал Teams.</span><span class="sxs-lookup"><span data-stu-id="15246-107">With Microsoft Graph, you can migrate users' existing message history and data from an external system into a Teams channel.</span></span> <span data-ttu-id="15246-108">Включив воссоздание иерархии сообщений сторонних платформ внутри Teams, пользователи могут беспрепятственно продолжать общение и действовать без прерывания.</span><span class="sxs-lookup"><span data-stu-id="15246-108">By enabling the recreation of a third-party platform messaging hierarchy inside Teams, users can continue their communications in a seamless manner and proceed without interruption.</span></span>

> [!NOTE] 
> <span data-ttu-id="15246-109">В дальнейшем корпорация Майкрософт может потребовать у вас или ваших клиентов оплаты дополнительных сборов на основе количества импортированных данных.</span><span class="sxs-lookup"><span data-stu-id="15246-109">In the future, Microsoft may require you or your customers to pay additional fees based on the amount of data imported.</span></span>

## <a name="import-overview"></a><span data-ttu-id="15246-110">Обзор импорта</span><span class="sxs-lookup"><span data-stu-id="15246-110">Import overview</span></span>

<span data-ttu-id="15246-111">На высоком уровне процесс импорта состоит из следующих:</span><span class="sxs-lookup"><span data-stu-id="15246-111">At a high level, the import process consists of the following:</span></span>

1. [<span data-ttu-id="15246-112">Создание команды с помощью back-in-time timestamp</span><span class="sxs-lookup"><span data-stu-id="15246-112">Create a team with a back-in-time timestamp</span></span>](#step-one-create-a-team)
1. [<span data-ttu-id="15246-113">Создание канала с помощью back-in-timestamp</span><span class="sxs-lookup"><span data-stu-id="15246-113">Create a channel with a back-in-time timestamp</span></span>](#step-two-create-a-channel)  
1. [<span data-ttu-id="15246-114">Импорт внешних датируемых сообщений в обратном времени</span><span class="sxs-lookup"><span data-stu-id="15246-114">Import external back-in-time dated messages</span></span>](#step-three-import-messages)
1. [<span data-ttu-id="15246-115">Завершение процесса миграции группы и канала</span><span class="sxs-lookup"><span data-stu-id="15246-115">Complete the team and channel migration process</span></span>](#step-four-complete-migration-mode)
1. [<span data-ttu-id="15246-116">Добавление членов группы</span><span class="sxs-lookup"><span data-stu-id="15246-116">Add team members</span></span>](#step-five-add-team-members)

## <a name="necessary-requirements"></a><span data-ttu-id="15246-117">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="15246-117">Necessary requirements</span></span>

### <a name="analyze-and-prepare-message-data"></a><span data-ttu-id="15246-118">Анализ и подготовка данных сообщений</span><span class="sxs-lookup"><span data-stu-id="15246-118">Analyze and prepare message data</span></span>

<span data-ttu-id="15246-119">✔ просмотрите сторонние данные, чтобы определить, что будет перенесено.</span><span class="sxs-lookup"><span data-stu-id="15246-119">✔ Review the third-party data to decide what will be migrated.</span></span>  
<span data-ttu-id="15246-120">✔ извлекать выбранные данные из системы сторонних чатов.</span><span class="sxs-lookup"><span data-stu-id="15246-120">✔ Extract the selected data from the third-party chat system.</span></span>  
<span data-ttu-id="15246-121">✔ на карте структуру сторонних чатов в структуру Teams.</span><span class="sxs-lookup"><span data-stu-id="15246-121">✔ Map the third-party chat structure to the Teams structure.</span></span>  
<span data-ttu-id="15246-122">✔ импорт данных в формат, необходимый для миграции.</span><span class="sxs-lookup"><span data-stu-id="15246-122">✔ Convert import data into format needed for migration.</span></span>  

### <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="15246-123">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="15246-123">Set up your Office 365 tenant</span></span>

<span data-ttu-id="15246-124">✔ убедитесь, что клиент Office 365 существует для данных импорта.</span><span class="sxs-lookup"><span data-stu-id="15246-124">✔ Ensure that an Office 365 tenant exists for the import data.</span></span> <span data-ttu-id="15246-125">Дополнительные сведения о настройке аренды Office 365 для Teams см. в статью "Подготовка клиента [Office 365".](../../concepts/build-and-test/prepare-your-o365-tenant.md) </span><span class="sxs-lookup"><span data-stu-id="15246-125">For more information on setting up an Office 365 tenancy for Teams, *see*, [Prepare your Office 365 tenant](../../concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>  
<span data-ttu-id="15246-126">✔ убедитесь, что члены группы находятся в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="15246-126">✔ Make sure that team members are in Azure Active Directory (AAD).</span></span>  <span data-ttu-id="15246-127">Дополнительные сведения *см.* [в добавлении нового пользователя в](/azure/active-directory/fundamentals/add-users-azure-active-directory) Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15246-127">For more information *see* [Add a new user](/azure/active-directory/fundamentals/add-users-azure-active-directory) to Azure Active Directory.</span></span>

## <a name="step-one-create-a-team"></a><span data-ttu-id="15246-128">Шаг первый: создание команды</span><span class="sxs-lookup"><span data-stu-id="15246-128">Step One: Create a team</span></span>

<span data-ttu-id="15246-129">Так как существующие данные переносят, сохранение исходных периодов времени отправки сообщений и предотвращение активности обмена сообщениями в процессе миграции являются ключом к воссозданию существующего потока сообщений пользователя в Teams.</span><span class="sxs-lookup"><span data-stu-id="15246-129">Since existing data is being migrated, maintaining the original message timestamps and preventing messaging activity during the migration process are key to recreating the user's existing message flow in Teams.</span></span> <span data-ttu-id="15246-130">Это достигается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="15246-130">This is achieved as follows:</span></span>

> <span data-ttu-id="15246-131">[Создайте новую команду](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) со временем, используя свойство ресурсов  `createdDateTime`  группы.</span><span class="sxs-lookup"><span data-stu-id="15246-131">[Create a new team](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the team resource  `createdDateTime`  property.</span></span> <span data-ttu-id="15246-132">Поместите новую команду в специальное состояние, которое не позволяет пользователям выполнить большинство действий в команде до завершения процесса `migration mode` миграции.</span><span class="sxs-lookup"><span data-stu-id="15246-132">Place the new team in `migration mode`, a special state that bars users from most activities within the team until the migration process is complete.</span></span> <span data-ttu-id="15246-133">Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `teamCreationMode` `migration` как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="15246-133">Include the `teamCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  

> <span data-ttu-id="15246-134">**ПРИМЕЧАНИЕ.** Поле будет заполнено только для экземпляров команды или канала, которые `createdDateTime` были перенесены.</span><span class="sxs-lookup"><span data-stu-id="15246-134">**NOTE**:  The `createdDateTime` field will only be populated for instances of a team or channel that have been migrated.</span></span>

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a><span data-ttu-id="15246-135">Разрешения</span><span class="sxs-lookup"><span data-stu-id="15246-135">Permissions</span></span>

|<span data-ttu-id="15246-136">ScopeName</span><span class="sxs-lookup"><span data-stu-id="15246-136">ScopeName</span></span>|<span data-ttu-id="15246-137">DisplayName</span><span class="sxs-lookup"><span data-stu-id="15246-137">DisplayName</span></span>|<span data-ttu-id="15246-138">Описание</span><span class="sxs-lookup"><span data-stu-id="15246-138">Description</span></span>|<span data-ttu-id="15246-139">Тип</span><span class="sxs-lookup"><span data-stu-id="15246-139">Type</span></span>|<span data-ttu-id="15246-140">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="15246-140">Admin Consent?</span></span>|<span data-ttu-id="15246-141">Объекты/API, охваченные</span><span class="sxs-lookup"><span data-stu-id="15246-141">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="15246-142">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="15246-142">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="15246-143">Создание и управление ресурсами для миграции в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="15246-143">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="15246-144">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="15246-144">**Application-only**</span></span>|<span data-ttu-id="15246-145">**Да**</span><span class="sxs-lookup"><span data-stu-id="15246-145">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a><span data-ttu-id="15246-146">Запрос (создание группы в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="15246-146">Request (create a team in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="15246-147">Отклик</span><span class="sxs-lookup"><span data-stu-id="15246-147">Response</span></span>

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a><span data-ttu-id="15246-148">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="15246-148">Error messages</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="15246-149">`createdDateTime`  установлено на будущее.</span><span class="sxs-lookup"><span data-stu-id="15246-149">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="15246-150">`createdDateTime`  правильно задан, но `teamCreationMode`  атрибут экземпляра отсутствует или задан для значения недействительным.</span><span class="sxs-lookup"><span data-stu-id="15246-150">`createdDateTime`  correctly specified, but `teamCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-two-create-a-channel"></a><span data-ttu-id="15246-151">Шаг второй: создание канала</span><span class="sxs-lookup"><span data-stu-id="15246-151">Step Two: Create a channel</span></span>

<span data-ttu-id="15246-152">Создание канала для импортируемых сообщений аналогично сценарию создания группы:</span><span class="sxs-lookup"><span data-stu-id="15246-152">Creating a channel for the imported messages is similar to the create team scenario:</span></span>

> <span data-ttu-id="15246-153">[Создайте новый канал](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) с использованием свойства ресурса канала с помощью функции timestamp в обратном `createdDateTime` времени.</span><span class="sxs-lookup"><span data-stu-id="15246-153">[Create a new channel](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) with a back-in-time timestamp using the channel resource `createdDateTime` property.</span></span> <span data-ttu-id="15246-154">Поместите новый канал в специальное состояние, которое не позволяет пользователям от большинства действий чата в канале до завершения процесса `migration mode` миграции.</span><span class="sxs-lookup"><span data-stu-id="15246-154">Place the new channel in `migration mode`, a special state that bars users from most chat activities within the channel until the migration process is complete.</span></span>  <span data-ttu-id="15246-155">Включай атрибут экземпляра со значением в запросе POST, чтобы явно идентифицировать новую команду `channelCreationMode` `migration` как созданную для миграции.</span><span class="sxs-lookup"><span data-stu-id="15246-155">Include the `channelCreationMode` instance attribute with the `migration` value in the POST request to explicitly identify the new team as being created for migration.</span></span>  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a><span data-ttu-id="15246-156">Разрешения</span><span class="sxs-lookup"><span data-stu-id="15246-156">Permissions</span></span>

|<span data-ttu-id="15246-157">ScopeName</span><span class="sxs-lookup"><span data-stu-id="15246-157">ScopeName</span></span>|<span data-ttu-id="15246-158">DisplayName</span><span class="sxs-lookup"><span data-stu-id="15246-158">DisplayName</span></span>|<span data-ttu-id="15246-159">Описание</span><span class="sxs-lookup"><span data-stu-id="15246-159">Description</span></span>|<span data-ttu-id="15246-160">Тип</span><span class="sxs-lookup"><span data-stu-id="15246-160">Type</span></span>|<span data-ttu-id="15246-161">Согласие администратора?</span><span class="sxs-lookup"><span data-stu-id="15246-161">Admin Consent?</span></span>|<span data-ttu-id="15246-162">Объекты/API, охваченные</span><span class="sxs-lookup"><span data-stu-id="15246-162">Entities/APIs covered</span></span>|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|<span data-ttu-id="15246-163">Управление миграцией в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="15246-163">Manage migration to Microsoft Teams</span></span>|<span data-ttu-id="15246-164">Создание и управление ресурсами для миграции в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="15246-164">Creating, managing resources for migration to Microsoft Teams</span></span>|<span data-ttu-id="15246-165">**Только для приложений**</span><span class="sxs-lookup"><span data-stu-id="15246-165">**Application-only**</span></span>|<span data-ttu-id="15246-166">**Да**</span><span class="sxs-lookup"><span data-stu-id="15246-166">**Yes**</span></span>|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a><span data-ttu-id="15246-167">Запрос (создание канала в состоянии миграции)</span><span class="sxs-lookup"><span data-stu-id="15246-167">Request (create a channel in migration state)</span></span>

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

#### <a name="response"></a><span data-ttu-id="15246-168">Отклик</span><span class="sxs-lookup"><span data-stu-id="15246-168">Response</span></span>

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

#### <a name="error-message"></a><span data-ttu-id="15246-169">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="15246-169">Error message</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="15246-170">`createdDateTime`  установлено на будущее.</span><span class="sxs-lookup"><span data-stu-id="15246-170">`createdDateTime`  set for future.</span></span>
* <span data-ttu-id="15246-171">`createdDateTime`  правильно задан, но `channelCreationMode`  атрибут экземпляра отсутствует или задан для значения недействительным.</span><span class="sxs-lookup"><span data-stu-id="15246-171">`createdDateTime`  correctly specified but `channelCreationMode`  instance attribute  is missing or set to invalid value.</span></span>

## <a name="step-three-import-messages"></a><span data-ttu-id="15246-172">Шаг 3. Импорт сообщений</span><span class="sxs-lookup"><span data-stu-id="15246-172">Step Three: Import messages</span></span>

<span data-ttu-id="15246-173">После создания группы и канала можно приступить к отправке сообщений в обратном времени с помощью ключей и ключей в `createdDateTime` `from`  тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="15246-173">After the team and channel have been created, you can begin sending back-in-time messages using the `createdDateTime`  and `from`  keys in the request body.</span></span> <span data-ttu-id="15246-174">**ПРИМЕЧАНИЕ.** Сообщения, импортируемые с более ранним `createdDateTime` потоком `createdDateTime` сообщений, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="15246-174">**NOTE**: messages imported with `createdDateTime` earlier than the message thread `createdDateTime` is not supported.</span></span>

> [!NOTE]
> * <span data-ttu-id="15246-175">`createdDateTime` должны быть уникальными для сообщений в одном потоке.</span><span class="sxs-lookup"><span data-stu-id="15246-175">`createdDateTime` must be unique across messages in the same thread.</span></span>
> * <span data-ttu-id="15246-176">`createdDateTime` поддерживает периоды времени с точностью миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="15246-176">`createdDateTime` supports timestamps with milliseconds precision.</span></span> <span data-ttu-id="15246-177">Например, если входящий запрос сообщения имеет значение set `createdDateTime` as *2020-09-16T05:50:31.0025302Z,* то оно будет преобразовано в *2020-09-16T05:50:31.002Z,* когда сообщение будет ingested.</span><span class="sxs-lookup"><span data-stu-id="15246-177">For example, if the incoming request message has the value of `createdDateTime` set as *2020-09-16T05:50:31.0025302Z*, then it would be converted to *2020-09-16T05:50:31.002Z* when the message is ingested.</span></span>

#### <a name="request-post-message-that-is-text-only"></a><span data-ttu-id="15246-178">Запрос (сообщение POST, которое является текстовым)</span><span class="sxs-lookup"><span data-stu-id="15246-178">Request (POST message that is text-only)</span></span>

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

#### <a name="response"></a><span data-ttu-id="15246-179">Отклик</span><span class="sxs-lookup"><span data-stu-id="15246-179">Response</span></span>

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

#### <a name="error-messages"></a><span data-ttu-id="15246-180">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="15246-180">Error messages</span></span>

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a><span data-ttu-id="15246-181">Запрос (СООБЩЕНИЕ сообщения с inline image)</span><span class="sxs-lookup"><span data-stu-id="15246-181">Request (POST a message with inline image)</span></span>

> <span data-ttu-id="15246-182">**Примечание.** В этом сценарии нет специальных областей разрешений, так как запрос является частью chatMessage; Области для chatMessage применяются и здесь.</span><span class="sxs-lookup"><span data-stu-id="15246-182">**Note**: There are no special permission scopes in this scenario since the request is part of chatMessage; scopes for chatMessage apply here as well.</span></span>

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

#### <a name="response"></a><span data-ttu-id="15246-183">Отклик</span><span class="sxs-lookup"><span data-stu-id="15246-183">Response</span></span>

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

## <a name="step-four-complete-migration-mode"></a><span data-ttu-id="15246-184">Шаг 4. Полный режим миграции</span><span class="sxs-lookup"><span data-stu-id="15246-184">Step Four: Complete migration mode</span></span>

<span data-ttu-id="15246-185">После завершения процесса миграции сообщений команда и канал вывели из режима миграции с помощью  `completeMigration`  метода.</span><span class="sxs-lookup"><span data-stu-id="15246-185">Once the message migration process has completed, both the team and channel are taken out of migration mode using the  `completeMigration`  method.</span></span> <span data-ttu-id="15246-186">Этот шаг открывает ресурсы команды и канала для общего использования членами группы.</span><span class="sxs-lookup"><span data-stu-id="15246-186">This step opens the team and channel resources for general use by team members.</span></span> <span data-ttu-id="15246-187">Действие привязано к `team` экземпляру.</span><span class="sxs-lookup"><span data-stu-id="15246-187">The action is bound to the `team` instance.</span></span>

#### <a name="request-end-team-migration-mode"></a><span data-ttu-id="15246-188">Запрос (режим миграции конечных команд)</span><span class="sxs-lookup"><span data-stu-id="15246-188">Request (end team migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="15246-189">Отклик</span><span class="sxs-lookup"><span data-stu-id="15246-189">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a><span data-ttu-id="15246-190">Запрос (режим переноса конечных каналов)</span><span class="sxs-lookup"><span data-stu-id="15246-190">Request (end channel migration mode)</span></span>

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a><span data-ttu-id="15246-191">Отклик</span><span class="sxs-lookup"><span data-stu-id="15246-191">Response</span></span>

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a><span data-ttu-id="15246-192">Отклик с ошибкой</span><span class="sxs-lookup"><span data-stu-id="15246-192">Error response</span></span>

```http
400 Bad Request
```

* <span data-ttu-id="15246-193">Действие, которое `team` вызвано или `channel` которое не в `migrationMode` .</span><span class="sxs-lookup"><span data-stu-id="15246-193">Action called on a `team` or `channel` that is not in `migrationMode`.</span></span>

## <a name="step-five-add-team-members"></a><span data-ttu-id="15246-194">Шаг 5. Добавление членов группы</span><span class="sxs-lookup"><span data-stu-id="15246-194">Step Five: Add team members</span></span>

<span data-ttu-id="15246-195">Вы можете добавить участника в группу с [помощью API UI teams](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) или Microsoft Graph [Add:](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="15246-195">You can add a member to a team [using the Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) or Microsoft Graph [Add member](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API:</span></span>

#### <a name="request-add-member"></a><span data-ttu-id="15246-196">Запрос (добавление участника)</span><span class="sxs-lookup"><span data-stu-id="15246-196">Request (add member)</span></span>

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

#### <a name="response"></a><span data-ttu-id="15246-197">Отклик</span><span class="sxs-lookup"><span data-stu-id="15246-197">Response</span></span>

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a><span data-ttu-id="15246-198">Советы и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="15246-198">Tips and additional information</span></span>

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* <span data-ttu-id="15246-199">Вы можете импортировать сообщения от пользователей, которые не находятся в Teams.</span><span class="sxs-lookup"><span data-stu-id="15246-199">You can import messages from users who are not in Teams.</span></span> <span data-ttu-id="15246-200">**ПРИМЕЧАНИЕ.** Сообщения, импортируемые для пользователей, не присутствующих в клиенте, не будут искаться на клиентских порталах Teams или на порталах соответствия требованиям во время предварительного просмотра общего просмотра.</span><span class="sxs-lookup"><span data-stu-id="15246-200">**NOTE**: Messages imported for users not present in the tenant will not be searchable in the Teams client or compliance portals during Public Preview.</span></span>

* <span data-ttu-id="15246-201">После запроса нельзя импортировать дополнительные сообщения `completeMigration` в команду.</span><span class="sxs-lookup"><span data-stu-id="15246-201">Once the `completeMigration` request is made, you cannot import further messages into the team.</span></span>

* <span data-ttu-id="15246-202">Члены группы могут быть добавлены в новую команду только после успешного ответа на `completeMigration` запрос.</span><span class="sxs-lookup"><span data-stu-id="15246-202">Team members can only be added to the new team after the `completeMigration` request has returned a successful response.</span></span>

* <span data-ttu-id="15246-203">Регулирование: импорт сообщений по 5 RPS на канал.</span><span class="sxs-lookup"><span data-stu-id="15246-203">Throttling: Messages import at 5 RPS per channel.</span></span>

* <span data-ttu-id="15246-204">Если необходимо внести исправление в результаты миграции, необходимо удалить команду и повторить действия по созданию группы и каналу и повторной миграции сообщений.</span><span class="sxs-lookup"><span data-stu-id="15246-204">If you need to make a correction to the migration results, you need to delete the team and repeat the steps to create the team and channel and re-migrate the messages.</span></span>

> [!NOTE]
> <span data-ttu-id="15246-205">В настоящее время inline images are the only type of media supported by the import message API schpi.</span><span class="sxs-lookup"><span data-stu-id="15246-205">Currently, inline images are the only type of media supported by the import message API schema.</span></span>

##### <a name="import-content-scope"></a><span data-ttu-id="15246-206">Область импорта контента</span><span class="sxs-lookup"><span data-stu-id="15246-206">Import content scope</span></span>

|<span data-ttu-id="15246-207">В области</span><span class="sxs-lookup"><span data-stu-id="15246-207">In-scope</span></span> | <span data-ttu-id="15246-208">В настоящее время вне области</span><span class="sxs-lookup"><span data-stu-id="15246-208">Currently out-of-scope</span></span>|
|----------|--------------------------|
|<span data-ttu-id="15246-209">Сообщения группы и канала</span><span class="sxs-lookup"><span data-stu-id="15246-209">Team and channel messages</span></span>|<span data-ttu-id="15246-210">1:1 и групповые сообщения чата</span><span class="sxs-lookup"><span data-stu-id="15246-210">1:1 and group chat messages</span></span>|
|<span data-ttu-id="15246-211">Созданное время исходного сообщения</span><span class="sxs-lookup"><span data-stu-id="15246-211">Created time of the original message</span></span>|<span data-ttu-id="15246-212">Частные каналы</span><span class="sxs-lookup"><span data-stu-id="15246-212">Private channels</span></span>|
|<span data-ttu-id="15246-213">Inline images as part of the message</span><span class="sxs-lookup"><span data-stu-id="15246-213">Inline images as part of the message</span></span>|<span data-ttu-id="15246-214">При упоминаний</span><span class="sxs-lookup"><span data-stu-id="15246-214">At mentions</span></span>|
|<span data-ttu-id="15246-215">Ссылки на существующие файлы в SPO/OneDrive</span><span class="sxs-lookup"><span data-stu-id="15246-215">Links to existing files in SPO/OneDrive</span></span>|<span data-ttu-id="15246-216">Реакции</span><span class="sxs-lookup"><span data-stu-id="15246-216">Reactions</span></span>|
|<span data-ttu-id="15246-217">Сообщения с богатым текстом</span><span class="sxs-lookup"><span data-stu-id="15246-217">Messages with rich text</span></span>|<span data-ttu-id="15246-218">Видео</span><span class="sxs-lookup"><span data-stu-id="15246-218">Videos</span></span>|
|<span data-ttu-id="15246-219">Цепочка ответов на сообщения</span><span class="sxs-lookup"><span data-stu-id="15246-219">Message reply chain</span></span>|<span data-ttu-id="15246-220">Объявления</span><span class="sxs-lookup"><span data-stu-id="15246-220">Announcements</span></span>|
|<span data-ttu-id="15246-221">Обработка высокой пропускной способности</span><span class="sxs-lookup"><span data-stu-id="15246-221">High throughput processing</span></span>|<span data-ttu-id="15246-222">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="15246-222">Code snippets</span></span>|
||<span data-ttu-id="15246-223">Адаптивные карты</span><span class="sxs-lookup"><span data-stu-id="15246-223">Adaptive cards</span></span>|
||<span data-ttu-id="15246-224">Наклейки</span><span class="sxs-lookup"><span data-stu-id="15246-224">Stickers</span></span>|
||<span data-ttu-id="15246-225">Emojis</span><span class="sxs-lookup"><span data-stu-id="15246-225">Emojis</span></span>|
||<span data-ttu-id="15246-226">Котировки</span><span class="sxs-lookup"><span data-stu-id="15246-226">Quotes</span></span>|
||<span data-ttu-id="15246-227">Перекрестные сообщения между каналами</span><span class="sxs-lookup"><span data-stu-id="15246-227">Cross posts between channels</span></span>|


## <a name="see-also"></a><span data-ttu-id="15246-228">См. также</span><span class="sxs-lookup"><span data-stu-id="15246-228">See also</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="15246-229">Дополнительные данные об интеграции Microsoft Graph и Teams</span><span class="sxs-lookup"><span data-stu-id="15246-229">Learn more about Microsoft Graph and Teams integration</span></span>](/graph/teams-concept-overview)
