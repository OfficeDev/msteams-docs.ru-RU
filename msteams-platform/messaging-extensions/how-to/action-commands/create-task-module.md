---
title: Создание и отправка модуля задач
author: clearab
description: Обработка начального действия вызова и реагирование с помощью модуля задач из команды расширения обмена сообщениями действий
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1245edba88dcd256f77c55cfe049ec2e846522c2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019848"
---
# <a name="create-and-send-the-task-module"></a><span data-ttu-id="9795c-103">Создание и отправка модуля задач</span><span class="sxs-lookup"><span data-stu-id="9795c-103">Create and send the task module</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="9795c-104">Модуль задач можно создать с помощью адаптивной карты или встроенного веб-представления.</span><span class="sxs-lookup"><span data-stu-id="9795c-104">You can create the task module using an Adaptive Card or an embedded web view.</span></span> <span data-ttu-id="9795c-105">Чтобы создать модуль задач, необходимо выполнить процесс, называемый начальным запросом на вызов.</span><span class="sxs-lookup"><span data-stu-id="9795c-105">To create a task module, you must perform the process called the initial invoke request.</span></span> <span data-ttu-id="9795c-106">Этот документ охватывает начальный запрос на вызов, свойства активности полезной нагрузки при вызове модуля задачи из чата 1:1, группового чата, канала (новая должность), канала (ответ на поток) и командного окна.</span><span class="sxs-lookup"><span data-stu-id="9795c-106">This document covers the initial invoke request, payload activity properties when a task module is invoked from 1:1 chat, group chat, channel (new post), channel (reply to thread), and command box.</span></span> 
> [!NOTE]
> <span data-ttu-id="9795c-107">Если вы не заполняете модуль задач параметрами, определенными в манифесте приложения, необходимо создать модуль задач для пользователей с помощью адаптивной карты или встроенного веб-представления.</span><span class="sxs-lookup"><span data-stu-id="9795c-107">If you are not populating the task module with parameters defined in the app manifest, you must create the task module for users with either an Adaptive Card or an embedded web view.</span></span>

## <a name="the-initial-invoke-request"></a><span data-ttu-id="9795c-108">Начальный запрос на вызов</span><span class="sxs-lookup"><span data-stu-id="9795c-108">The initial invoke request</span></span>

<span data-ttu-id="9795c-109">В процессе первоначального запроса на вызов служба получает объект типа, и необходимо ответить объектом, содержащим адаптивную карту или URL-адрес встроенного `Activity` `composeExtension/fetchTask` `task` веб-представления.</span><span class="sxs-lookup"><span data-stu-id="9795c-109">In the process of the initial invoke request, your service receives an `Activity` object of type `composeExtension/fetchTask`, and you must respond with a `task` object containing either an Adaptive Card or a URL to the embedded web view.</span></span> <span data-ttu-id="9795c-110">Наряду со стандартными свойствами активности бота, начальная загрузка ссылок содержит следующие метаданные запроса:</span><span class="sxs-lookup"><span data-stu-id="9795c-110">Along with the standard bot activity properties, the initial invoke payload contains the following request metadata:</span></span>

|<span data-ttu-id="9795c-111">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-111">Property name</span></span>|<span data-ttu-id="9795c-112">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-112">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9795c-113">Тип запроса.</span><span class="sxs-lookup"><span data-stu-id="9795c-113">Type of request.</span></span> <span data-ttu-id="9795c-114">Это должно быть `invoke` .</span><span class="sxs-lookup"><span data-stu-id="9795c-114">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="9795c-115">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="9795c-115">Type of command that is issued to your service.</span></span> <span data-ttu-id="9795c-116">Это должно быть `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="9795c-116">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="9795c-117">ID пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-117">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="9795c-118">Имя пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-118">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="9795c-119">ID объекта Azure Active Directory пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-119">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="9795c-120">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9795c-120">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="9795c-121">ID канала (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9795c-121">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="9795c-122">Team ID (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9795c-122">Team ID (if the request was made in a channel).</span></span> |
|`value.commandId` | <span data-ttu-id="9795c-123">Содержит ID вызываемой команды.</span><span class="sxs-lookup"><span data-stu-id="9795c-123">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="9795c-124">Контекст, который вызвал событие.</span><span class="sxs-lookup"><span data-stu-id="9795c-124">The context that triggered the event.</span></span> <span data-ttu-id="9795c-125">Это должно быть `compose` .</span><span class="sxs-lookup"><span data-stu-id="9795c-125">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="9795c-126">Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра.</span><span class="sxs-lookup"><span data-stu-id="9795c-126">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="9795c-127">Он должен быть `default` или `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="9795c-127">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="9795c-128">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-128">Example</span></span>

<span data-ttu-id="9795c-129">Код начального запроса на вызов приводится в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9795c-129">The code for the initial invoke request is given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-11-chat"></a><span data-ttu-id="9795c-130">Свойства активности полезной нагрузки при вызове модуля задач из чата 1:1</span><span class="sxs-lookup"><span data-stu-id="9795c-130">Payload activity properties when a task module is invoked from 1:1 chat</span></span> 

<span data-ttu-id="9795c-131">Свойства активности полезной нагрузки при вызове модуля задач из чата 1:1 перечислены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9795c-131">The payload activity properties when a task module is invoked from 1:1 chat are listed as follows:</span></span>

|<span data-ttu-id="9795c-132">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-132">Property name</span></span>|<span data-ttu-id="9795c-133">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-133">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9795c-134">Тип запроса.</span><span class="sxs-lookup"><span data-stu-id="9795c-134">Type of request.</span></span> <span data-ttu-id="9795c-135">Это должно быть `invoke` .</span><span class="sxs-lookup"><span data-stu-id="9795c-135">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="9795c-136">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="9795c-136">Type of command that is issued to your service.</span></span> <span data-ttu-id="9795c-137">Это должно быть `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="9795c-137">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="9795c-138">ID пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-138">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="9795c-139">Имя пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-139">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="9795c-140">ID объекта Azure Active Directory пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-140">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="9795c-141">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9795c-141">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="9795c-142">Имя источника, из которого вызывается модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-142">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="9795c-143">Получает или задает ID сообщения, на которое это сообщение является ответом.</span><span class="sxs-lookup"><span data-stu-id="9795c-143">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="9795c-144">Содержит ID вызываемой команды.</span><span class="sxs-lookup"><span data-stu-id="9795c-144">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="9795c-145">Контекст, который вызвал событие.</span><span class="sxs-lookup"><span data-stu-id="9795c-145">The context that triggered the event.</span></span> <span data-ttu-id="9795c-146">Это должно быть `compose` .</span><span class="sxs-lookup"><span data-stu-id="9795c-146">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="9795c-147">Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра.</span><span class="sxs-lookup"><span data-stu-id="9795c-147">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="9795c-148">Он должен быть `default` или `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="9795c-148">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="9795c-149">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-149">Example</span></span>

<span data-ttu-id="9795c-150">Свойства активности полезной нагрузки при вызове модуля задач из чата 1:1 приводятся в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9795c-150">The payload activity properties when a task module is invoked from 1:1 chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bc319b1d-571a-194d-9ffb-11d7ab37c9ff",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  }
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "fe50f49e5c74440bb2ebf07f49e9553c",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```
## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-group-chat"></a><span data-ttu-id="9795c-151">Свойства активности полезной нагрузки при вызове модуля задач из группового чата</span><span class="sxs-lookup"><span data-stu-id="9795c-151">Payload activity properties when a task module is invoked from a group chat</span></span> 

<span data-ttu-id="9795c-152">Свойства активности полезной нагрузки при вызове модуля задач из группового чата перечислены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9795c-152">The payload activity properties when a task module is invoked from a group chat are listed as follows:</span></span>

|<span data-ttu-id="9795c-153">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-153">Property name</span></span>|<span data-ttu-id="9795c-154">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-154">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9795c-155">Тип запроса.</span><span class="sxs-lookup"><span data-stu-id="9795c-155">Type of request.</span></span> <span data-ttu-id="9795c-156">Это должно быть `invoke` .</span><span class="sxs-lookup"><span data-stu-id="9795c-156">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="9795c-157">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="9795c-157">Type of command that is issued to your service.</span></span> <span data-ttu-id="9795c-158">Это должно быть `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="9795c-158">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="9795c-159">ID пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-159">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="9795c-160">Имя пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-160">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="9795c-161">ID объекта Azure Active Directory пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-161">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="9795c-162">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9795c-162">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="9795c-163">Имя источника, из которого вызывается модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-163">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="9795c-164">Получает или задает ID сообщения, на которое это сообщение является ответом.</span><span class="sxs-lookup"><span data-stu-id="9795c-164">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="9795c-165">Содержит ID вызываемой команды.</span><span class="sxs-lookup"><span data-stu-id="9795c-165">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="9795c-166">Контекст, который вызвал событие.</span><span class="sxs-lookup"><span data-stu-id="9795c-166">The context that triggered the event.</span></span> <span data-ttu-id="9795c-167">Это должно быть `compose` .</span><span class="sxs-lookup"><span data-stu-id="9795c-167">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="9795c-168">Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра.</span><span class="sxs-lookup"><span data-stu-id="9795c-168">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="9795c-169">Он должен быть `default` или `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="9795c-169">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="9795c-170">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-170">Example</span></span>

<span data-ttu-id="9795c-171">Свойства активности полезной нагрузки при вызове модуля задач из группового чата приводятся в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9795c-171">The payload activity properties when a task module is invoked from a group chat are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:bf72031f-a17e-f99c-48dc-5c0714950d87",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "groupChat",
    "id": "19:d77be72390a1416e9644261e9064fa00@thread.skype",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "213167a1e3b6428b93e186ea5407c759",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-new-post"></a><span data-ttu-id="9795c-172">Свойства активности полезной нагрузки при вызове модуля задач из канала (новая публикация)</span><span class="sxs-lookup"><span data-stu-id="9795c-172">Payload activity properties when a task module is invoked from a channel (new post)</span></span> 

<span data-ttu-id="9795c-173">Свойства активности полезной нагрузки при вызове модуля задач из канала (новая должность) перечислены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9795c-173">The payload activity properties when a task module is invoked from a channel (new post) are listed as follows:</span></span>

|<span data-ttu-id="9795c-174">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-174">Property name</span></span>|<span data-ttu-id="9795c-175">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-175">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9795c-176">Тип запроса.</span><span class="sxs-lookup"><span data-stu-id="9795c-176">Type of request.</span></span> <span data-ttu-id="9795c-177">Это должно быть `invoke` .</span><span class="sxs-lookup"><span data-stu-id="9795c-177">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="9795c-178">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="9795c-178">Type of command that is issued to your service.</span></span> <span data-ttu-id="9795c-179">Это должно быть `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="9795c-179">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="9795c-180">ID пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-180">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="9795c-181">Имя пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-181">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="9795c-182">ID объекта Azure Active Directory пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-182">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="9795c-183">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9795c-183">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="9795c-184">ID канала (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9795c-184">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="9795c-185">Team ID (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9795c-185">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="9795c-186">Имя источника, из которого вызывается модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-186">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="9795c-187">Получает или задает ID сообщения, на которое это сообщение является ответом.</span><span class="sxs-lookup"><span data-stu-id="9795c-187">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="9795c-188">Содержит ID вызываемой команды.</span><span class="sxs-lookup"><span data-stu-id="9795c-188">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="9795c-189">Контекст, который вызвал событие.</span><span class="sxs-lookup"><span data-stu-id="9795c-189">The context that triggered the event.</span></span> <span data-ttu-id="9795c-190">Это должно быть `compose` .</span><span class="sxs-lookup"><span data-stu-id="9795c-190">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="9795c-191">Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра.</span><span class="sxs-lookup"><span data-stu-id="9795c-191">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="9795c-192">Он должен быть `default` `contrast` , или `dark` .</span><span class="sxs-lookup"><span data-stu-id="9795c-192">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="9795c-193">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-193">Example</span></span>

<span data-ttu-id="9795c-194">Свойства активности полезной нагрузки при вызове модуля задач из канала (новая должность) приводятся в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9795c-194">The payload activity properties when a task module is invoked from a channel (new post) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:a5fbb109-c989-c449-ee83-71ac99919d4b",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "Test",
    "commandContext": "compose",
    "requestId": "5336640edc7748b28ce2df43f5b45963",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-channel-reply-to-thread"></a><span data-ttu-id="9795c-195">Свойства активности полезной нагрузки при вызове модуля задач из канала (ответ на поток)</span><span class="sxs-lookup"><span data-stu-id="9795c-195">Payload activity properties when a task module is invoked from a channel (reply to thread)</span></span> 

<span data-ttu-id="9795c-196">Свойства активности полезной нагрузки при вызове модуля задач из канала (ответ на поток) перечислены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9795c-196">The payload activity properties when a task module is invoked from a channel (reply to thread) are listed as follows:</span></span>

|<span data-ttu-id="9795c-197">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-197">Property name</span></span>|<span data-ttu-id="9795c-198">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-198">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9795c-199">Тип запроса.</span><span class="sxs-lookup"><span data-stu-id="9795c-199">Type of request.</span></span> <span data-ttu-id="9795c-200">Это должно быть `invoke` .</span><span class="sxs-lookup"><span data-stu-id="9795c-200">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="9795c-201">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="9795c-201">Type of command that is issued to your service.</span></span> <span data-ttu-id="9795c-202">Это должно быть `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="9795c-202">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="9795c-203">ID пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-203">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="9795c-204">Имя пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-204">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="9795c-205">ID объекта Azure Active Directory пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-205">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="9795c-206">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9795c-206">Azure Active Directory tenant ID.</span></span> |
|`channelData.channel.id`| <span data-ttu-id="9795c-207">ID канала (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9795c-207">Channel ID (if the request was made in a channel).</span></span> |
|`channelData.team.id`| <span data-ttu-id="9795c-208">Team ID (если запрос был сделан в канале).</span><span class="sxs-lookup"><span data-stu-id="9795c-208">Team ID (if the request was made in a channel).</span></span> |
|`channelData.source.name`| <span data-ttu-id="9795c-209">Имя источника, из которого вызывается модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-209">The source name from where task module is invoked.</span></span> |
|`ChannelData.legacy. replyToId`| <span data-ttu-id="9795c-210">Получает или задает ID сообщения, на которое это сообщение является ответом.</span><span class="sxs-lookup"><span data-stu-id="9795c-210">Gets or sets the ID of the message to which this message is a reply.</span></span> |
|`value.commandId` | <span data-ttu-id="9795c-211">Содержит ID вызываемой команды.</span><span class="sxs-lookup"><span data-stu-id="9795c-211">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="9795c-212">Контекст, который вызвал событие.</span><span class="sxs-lookup"><span data-stu-id="9795c-212">The context that triggered the event.</span></span> <span data-ttu-id="9795c-213">Это должно быть `compose` .</span><span class="sxs-lookup"><span data-stu-id="9795c-213">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="9795c-214">Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра.</span><span class="sxs-lookup"><span data-stu-id="9795c-214">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="9795c-215">Он должен быть `default` или `contrast` `dark` .</span><span class="sxs-lookup"><span data-stu-id="9795c-215">It must be `default`, `contrast` or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="9795c-216">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-216">Example</span></span>

<span data-ttu-id="9795c-217">Свойства активности полезной нагрузки при вызове модуля задач из канала (ответ на поток) приводятся в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9795c-217">The payload activity properties when a task module is invoked from a channel (reply to thread) are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:19ccc884-c792-35ef-2f40-d0ff43dcca71",
  "from": {
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype;messageid=1611060744833",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "message",
    "requestId": "7f7d22efe5414818becebcec649a7912",
    "messagePayload": {
      "linkToMessage": "https://teams.microsoft.com/l/message/19:6decf54d86d945e4b3924b63a9161a78@thread.skype/1611060744833",
      "id": "1611060744833",
      "replyToId": null,
      "createdDateTime": "2021-01-19T12:52:24.833Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "<div><div><at id=\"0\">Testing outgoing Webhook-Nikitha</at> - Hi</div>\n</div>"
      },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc",
          "displayName": "Olo Brockhouse"
        },
        "application": null
      },
      "reactions": [],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Testing outgoing Webhook-Nikitha",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": null,
            "application": {
              "applicationIdentityType": "webhook",
              "id": "b8c1c68c-e290-4bdd-81c3-266f310751dc",
              "displayName": "Testing outgoing Webhook-Nikitha"
            }
          }
        }
      ],
      "attachments": []
    },
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

## <a name="payload-activity-properties-when-a-task-module-is-invoked-from-a-command-box"></a><span data-ttu-id="9795c-218">Свойства активности полезной нагрузки при вызове модуля задач из командного окна</span><span class="sxs-lookup"><span data-stu-id="9795c-218">Payload activity properties when a task module is invoked from a command box</span></span> 

<span data-ttu-id="9795c-219">Свойства активности полезной нагрузки при вызове модуля задач из командного окна перечислены следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9795c-219">The payload activity properties when a task module is invoked from a command box are listed as follows:</span></span>

|<span data-ttu-id="9795c-220">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-220">Property name</span></span>|<span data-ttu-id="9795c-221">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-221">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9795c-222">Тип запроса.</span><span class="sxs-lookup"><span data-stu-id="9795c-222">Type of request.</span></span> <span data-ttu-id="9795c-223">Это должно быть `invoke` .</span><span class="sxs-lookup"><span data-stu-id="9795c-223">It must be `invoke`.</span></span> |
|`name`| <span data-ttu-id="9795c-224">Тип команды, выданной службе.</span><span class="sxs-lookup"><span data-stu-id="9795c-224">Type of command that is issued to your service.</span></span> <span data-ttu-id="9795c-225">Это должно быть `composeExtension/fetchTask` .</span><span class="sxs-lookup"><span data-stu-id="9795c-225">It must be `composeExtension/fetchTask`.</span></span> |
|`from.id`| <span data-ttu-id="9795c-226">ID пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-226">ID of the user that sent the request.</span></span> |
|`from.name`| <span data-ttu-id="9795c-227">Имя пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-227">Name of the user that sent the request.</span></span> |
|`from.aadObjectId`| <span data-ttu-id="9795c-228">ID объекта Azure Active Directory пользователя, отправив запрос.</span><span class="sxs-lookup"><span data-stu-id="9795c-228">Azure Active Directory object ID of the user that sent the request.</span></span> |
|`channelData.tenant.id`| <span data-ttu-id="9795c-229">Идентификатор клиента Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9795c-229">Azure Active Directory tenant ID.</span></span> |
|`channelData.source.name`| <span data-ttu-id="9795c-230">Имя источника, из которого вызывается модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-230">The source name from where task module is invoked.</span></span> |
|`value.commandId` | <span data-ttu-id="9795c-231">Содержит ID вызываемой команды.</span><span class="sxs-lookup"><span data-stu-id="9795c-231">Contains the ID of the command that was invoked.</span></span> |
|`value.commandContext` | <span data-ttu-id="9795c-232">Контекст, который вызвал событие.</span><span class="sxs-lookup"><span data-stu-id="9795c-232">The context that triggered the event.</span></span> <span data-ttu-id="9795c-233">Это должно быть `compose` .</span><span class="sxs-lookup"><span data-stu-id="9795c-233">It must be `compose`.</span></span> |
|`value.context.theme` | <span data-ttu-id="9795c-234">Клиентская тема пользователя, полезная для встраиваемого форматирования веб-просмотра.</span><span class="sxs-lookup"><span data-stu-id="9795c-234">The user's client theme, useful for embedded web view formatting.</span></span> <span data-ttu-id="9795c-235">Он должен быть `default` `contrast` , или `dark` .</span><span class="sxs-lookup"><span data-stu-id="9795c-235">It must be `default`, `contrast`, or `dark`.</span></span> |

### <a name="example"></a><span data-ttu-id="9795c-236">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-236">Example</span></span>

<span data-ttu-id="9795c-237">Свойства активности полезной нагрузки при вызове модуля задач из командного окна приводятся в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9795c-237">The payload activity properties when a task module is invoked from a command box are given in the following example:</span></span>

```json
{
  "type": "invoke",
  "id": "f:172560f1-95f9-3189-edb2-b7612cd1a3cd",
    "id": "29:1aBjVi5MwCFfhPIV03E5uDdfpBFXp_2Yz-sjrvVg12oavg96cqpE_DiMhOpmN9zHeZpYbJcuUEKuSDy2AYWPz1A",
    "name": "Olo Brockhouse",
    "aadObjectId": "b130c271-d2eb-45f9-83ab-9eb3fe3788bc"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype",
    "name": "parsable",
    "tenantId": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
  },
  "channelData": {
    "channel": {
      "id": "19:6decf54d86d945e4b3924b63a9161a78@thread.skype"
    },
    "team": {
      "id": "19:acca514e83cb497e960e0b014d405336@thread.skype"
    },
    "tenant": {
      "id": "0d9b645f-597b-41f0-a2a3-ef103fbd91bb"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "TEst",
    "commandContext": "compose",
    "requestId": "d2ce690cdc2b4920a538e75882610a30",
    "context": {
      "theme": "default"
    }
  },
  "name": "composeExtension/fetchTask"
}
```

### <a name="example"></a><span data-ttu-id="9795c-238">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-238">Example</span></span> 

<span data-ttu-id="9795c-239">В следующем разделе кода приводится пример `fetchTask` запроса:</span><span class="sxs-lookup"><span data-stu-id="9795c-239">The following code section is an example of `fetchTask` request:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9795c-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9795c-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9795c-241">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9795c-241">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[<span data-ttu-id="9795c-242">JSON</span><span class="sxs-lookup"><span data-stu-id="9795c-242">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a><span data-ttu-id="9795c-243">Начальный запрос на вызов из сообщения</span><span class="sxs-lookup"><span data-stu-id="9795c-243">Initial invoke request from a message</span></span>

<span data-ttu-id="9795c-244">Если бот вызывается из сообщения, объект в первоначальном запросе на вызов должен содержать сведения о сообщении, из которых вызывается расширение `value` обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9795c-244">When your bot is invoked from a message,  the `value` object in the initial invoke request must contain the details of the message that your messaging extension is invoked from.</span></span> <span data-ttu-id="9795c-245">Массивы и массивы необязательны, и они не присутствуют, если в исходном сообщении нет реакций или `reactions` `mentions` упоминаний.</span><span class="sxs-lookup"><span data-stu-id="9795c-245">The `reactions` and `mentions` arrays are optional, and they are not present if there are no reactions or mentions in the original message.</span></span> <span data-ttu-id="9795c-246">В следующем разделе приводится пример `value` объекта:</span><span class="sxs-lookup"><span data-stu-id="9795c-246">The following section is an example of the `value` object:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9795c-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9795c-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9795c-248">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9795c-248">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[<span data-ttu-id="9795c-249">JSON</span><span class="sxs-lookup"><span data-stu-id="9795c-249">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a><span data-ttu-id="9795c-250">Ответ на fetchTask</span><span class="sxs-lookup"><span data-stu-id="9795c-250">Respond to the fetchTask</span></span>

<span data-ttu-id="9795c-251">Откликнитесь на запрос на вызов с помощью объекта, который содержит объект с адаптивной картой или `task` `taskInfo` веб-URL-адресом, или простое строковом сообщении.</span><span class="sxs-lookup"><span data-stu-id="9795c-251">Respond to the invoke request with a `task` object that contains either a `taskInfo` object with the Adaptive Card or web URL, or a simple string message.</span></span>

|<span data-ttu-id="9795c-252">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-252">Property name</span></span>|<span data-ttu-id="9795c-253">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-253">Purpose</span></span>|
|---|---|
|`type`| <span data-ttu-id="9795c-254">Может быть либо `continue` представить форму, либо `message` простое всплывающее всплывающее.</span><span class="sxs-lookup"><span data-stu-id="9795c-254">Can be either `continue` to present a form, or `message` for a simple popup.</span></span> |
|`value`| <span data-ttu-id="9795c-255">Объект `taskInfo` для формы или для `string` сообщения.</span><span class="sxs-lookup"><span data-stu-id="9795c-255">Either a `taskInfo` object for a form, or a `string` for a message.</span></span> |

<span data-ttu-id="9795c-256">Схема объекта taskInfo заключается в:</span><span class="sxs-lookup"><span data-stu-id="9795c-256">The schema for the taskInfo object is:</span></span>

|<span data-ttu-id="9795c-257">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="9795c-257">Property name</span></span>|<span data-ttu-id="9795c-258">Назначение</span><span class="sxs-lookup"><span data-stu-id="9795c-258">Purpose</span></span>|
|---|---|
|`title`| <span data-ttu-id="9795c-259">Название модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-259">The title of the task module.</span></span>|
|`height`| <span data-ttu-id="9795c-260">Он должен быть либо integer (в пикселях), или `small` `medium` , , `large` .</span><span class="sxs-lookup"><span data-stu-id="9795c-260">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`width`| <span data-ttu-id="9795c-261">Он должен быть либо integer (в пикселях), или `small` `medium` , , `large` .</span><span class="sxs-lookup"><span data-stu-id="9795c-261">It must be either an integer (in pixels), or `small`, `medium`, `large`.</span></span>|
|`card`| <span data-ttu-id="9795c-262">Адаптивная карта, определяющая форму (при ее использовании).</span><span class="sxs-lookup"><span data-stu-id="9795c-262">The adaptive card defining the form (if using one).</span></span>
|`url`| <span data-ttu-id="9795c-263">URL-адрес, открытый внутри модуля задач в качестве встроенного веб-представления.</span><span class="sxs-lookup"><span data-stu-id="9795c-263">The URL to be opened inside of the task module as an embedded web view.</span></span>|
|`fallbackUrl`| <span data-ttu-id="9795c-264">Если клиент не поддерживает функцию модуля задач, этот URL-адрес открывается на вкладке браузера.</span><span class="sxs-lookup"><span data-stu-id="9795c-264">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |

### <a name="respond-to-the-fetchtask-with-an-adaptive-card"></a><span data-ttu-id="9795c-265">Ответ на fetchTask с помощью адаптивной карты</span><span class="sxs-lookup"><span data-stu-id="9795c-265">Respond to the fetchTask with an Adaptive Card</span></span>

<span data-ttu-id="9795c-266">При использовании адаптивной карты необходимо отвечать объектом с `task` `value` объектом, содержащим адаптивную карту.</span><span class="sxs-lookup"><span data-stu-id="9795c-266">When using an adaptive card, you must respond with a `task` object with the `value` object containing an Adaptive Card.</span></span>

#### <a name="example"></a><span data-ttu-id="9795c-267">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-267">Example</span></span>

<span data-ttu-id="9795c-268">В следующем разделе кода приводится пример ответа `fetchTask` с помощью адаптивной карты:</span><span class="sxs-lookup"><span data-stu-id="9795c-268">The following code section is an example to `fetchTask` response with an adaptive card:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="9795c-269">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9795c-269">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="9795c-270">В этом примере [используется пакет AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) в дополнение к SDK Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="9795c-270">This sample uses the [AdaptiveCards NuGet package](https://www.nuget.org/packages/AdaptiveCards) in addition to the Bot Framework SDK.</span></span>

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9795c-271">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9795c-271">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="json"></a>[<span data-ttu-id="9795c-272">JSON</span><span class="sxs-lookup"><span data-stu-id="9795c-272">JSON</span></span>](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ]
      }
    }
  }
}
```

* * *

### <a name="create-a-task-module-with-an-embedded-web-view"></a><span data-ttu-id="9795c-273">Создание модуля задач со встроенным веб-представлением</span><span class="sxs-lookup"><span data-stu-id="9795c-273">Create a task module with an embedded web view</span></span>

<span data-ttu-id="9795c-274">При использовании встроенного веб-представления необходимо отвечать объектом с объектом, содержащим URL-адрес, в веб-форму, которую необходимо `task` `value` загрузить.</span><span class="sxs-lookup"><span data-stu-id="9795c-274">When using an embedded web view, you must respond with a `task` object with the `value` object containing the URL to the web form that you want to load.</span></span> <span data-ttu-id="9795c-275">Домены любого URL-адреса, который необходимо загрузить, должны быть включены в массив `validDomains` манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="9795c-275">The domains of any URL you want to load must be included in the `validDomains` array in your app's manifest.</span></span> <span data-ttu-id="9795c-276">Дополнительные сведения о создании встроенного веб-представления см. в [документации по модулям задач.](~/task-modules-and-cards/what-are-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="9795c-276">For more information on building your embedded web view, see the [task module documentation](~/task-modules-and-cards/what-are-task-modules.md).</span></span> 

# <a name="cnet"></a>[<span data-ttu-id="9795c-277">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9795c-277">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="9795c-278">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="9795c-278">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="9795c-279">JSON</span><span class="sxs-lookup"><span data-stu-id="9795c-279">JSON</span></span>](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

### <a name="request-to-install-your-conversational-bot"></a><span data-ttu-id="9795c-280">Запрос на установку разговорного бота</span><span class="sxs-lookup"><span data-stu-id="9795c-280">Request to install your conversational bot</span></span>

<span data-ttu-id="9795c-281">Если приложение содержит разговорный бот, установите бот в беседе и загрузив модуль задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-281">If the app contains a conversational bot, install the bot in the conversation and then load the task module.</span></span> <span data-ttu-id="9795c-282">Бот полезен для получения дополнительного контекста для модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-282">The bot is useful to get additional context for the task module.</span></span> <span data-ttu-id="9795c-283">Примером этого сценария является извлечение списка для заполнения управления сборщиком людей или списка каналов в команде.</span><span class="sxs-lookup"><span data-stu-id="9795c-283">An example for this scenario is to fetch the roster to populate a people picker control or the list of channels in a team.</span></span>

<span data-ttu-id="9795c-284">Когда расширение обмена сообщениями получает вызов, проверьте, установлен ли бот в текущем контексте для `composeExtension/fetchTask` облегчения потока.</span><span class="sxs-lookup"><span data-stu-id="9795c-284">When the messaging extension receives the `composeExtension/fetchTask` invoke, check if the bot is installed in the current context to facilitate the flow.</span></span> <span data-ttu-id="9795c-285">Например, проверьте поток с помощью вызова реестра получения.</span><span class="sxs-lookup"><span data-stu-id="9795c-285">For example, check the flow with a get roster call.</span></span> <span data-ttu-id="9795c-286">Если бот не установлен, верни адаптивную карту с действием, которое запрашивает у пользователя установку бота.</span><span class="sxs-lookup"><span data-stu-id="9795c-286">If the bot is not installed, return an Adaptive Card with an action that requests the user to install the bot.</span></span> <span data-ttu-id="9795c-287">Пользователь должен иметь разрешение на установку приложений в этом расположении для проверки.</span><span class="sxs-lookup"><span data-stu-id="9795c-287">The user must have the permission to install the apps in that location for checking.</span></span> <span data-ttu-id="9795c-288">Если установка приложения не увенчается успехом, пользователь получает сообщение, чтобы связаться с администратором.</span><span class="sxs-lookup"><span data-stu-id="9795c-288">If the app installation is unsuccessful, the user receives a message to contact the administrator.</span></span>

#### <a name="example"></a><span data-ttu-id="9795c-289">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-289">Example</span></span> 

<span data-ttu-id="9795c-290">В следующем разделе кода приводится пример ответа:</span><span class="sxs-lookup"><span data-stu-id="9795c-290">The following code section is an example of the response:</span></span>

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

<span data-ttu-id="9795c-291">После установки разговорного бота он получает еще одно сообщение с вызовом `name = composeExtension/submitAction` и `value.data.msteams.justInTimeInstall = true` .</span><span class="sxs-lookup"><span data-stu-id="9795c-291">After the installation of conversational bot, it receives another invoke message with `name = composeExtension/submitAction`, and `value.data.msteams.justInTimeInstall = true`.</span></span>

#### <a name="example"></a><span data-ttu-id="9795c-292">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-292">Example</span></span> 

<span data-ttu-id="9795c-293">В следующем разделе кода приводится пример ответа задачи на вызов:</span><span class="sxs-lookup"><span data-stu-id="9795c-293">The following code section is an example of the task response to the invoke:</span></span>

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

<span data-ttu-id="9795c-294">Ответ на вызов задачи должен быть похож на ответ установленного бота.</span><span class="sxs-lookup"><span data-stu-id="9795c-294">The task response to the invoke must be similar to that of the installed bot.</span></span>

#### <a name="example"></a><span data-ttu-id="9795c-295">Пример</span><span class="sxs-lookup"><span data-stu-id="9795c-295">Example</span></span> 

<span data-ttu-id="9795c-296">В следующем разделе кода приводится пример установки приложения с адаптивной картой вовремя:</span><span class="sxs-lookup"><span data-stu-id="9795c-296">The following code section is an example of just-in time installation of app with Adaptive card:</span></span> 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="code-sample"></a><span data-ttu-id="9795c-297">Пример кода</span><span class="sxs-lookup"><span data-stu-id="9795c-297">Code sample</span></span>

| <span data-ttu-id="9795c-298">Имя образца</span><span class="sxs-lookup"><span data-stu-id="9795c-298">Sample Name</span></span>           | <span data-ttu-id="9795c-299">Описание</span><span class="sxs-lookup"><span data-stu-id="9795c-299">Description</span></span> | <span data-ttu-id="9795c-300">.NET</span><span class="sxs-lookup"><span data-stu-id="9795c-300">.NET</span></span>    | <span data-ttu-id="9795c-301">Node.js</span><span class="sxs-lookup"><span data-stu-id="9795c-301">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="9795c-302">Действие расширения обмена сообщениями teams</span><span class="sxs-lookup"><span data-stu-id="9795c-302">Teams messaging extension action</span></span>| <span data-ttu-id="9795c-303">Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач.</span><span class="sxs-lookup"><span data-stu-id="9795c-303">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="9795c-304">View</span><span class="sxs-lookup"><span data-stu-id="9795c-304">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="9795c-305">View</span><span class="sxs-lookup"><span data-stu-id="9795c-305">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="9795c-306">Командный поиск расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="9795c-306">Teams messaging extension search</span></span>   |  <span data-ttu-id="9795c-307">Описывает, как определить команды поиска и реагировать на поиски.</span><span class="sxs-lookup"><span data-stu-id="9795c-307">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="9795c-308">View</span><span class="sxs-lookup"><span data-stu-id="9795c-308">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="9795c-309">View</span><span class="sxs-lookup"><span data-stu-id="9795c-309">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="see-also"></a><span data-ttu-id="9795c-310">См. также</span><span class="sxs-lookup"><span data-stu-id="9795c-310">See also</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="9795c-311">Определение команд действий</span><span class="sxs-lookup"><span data-stu-id="9795c-311">Define action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)


## <a name="next-step"></a><span data-ttu-id="9795c-312">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="9795c-312">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="9795c-313">Ответ на команду действий</span><span class="sxs-lookup"><span data-stu-id="9795c-313">Respond to action command</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

