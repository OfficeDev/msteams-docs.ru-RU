---
title: Обновление и удаление сообщений, отправленных с ленты.
author: WashingtonKayaker
description: Обновление и удаление сообщений, отправленных с ленты Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 46994c6810197002ef1c108af4f725426395b37f
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2020
ms.locfileid: "43957189"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="f829b-103">Обновление и удаление сообщений, отправленных с ленты.</span><span class="sxs-lookup"><span data-stu-id="f829b-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="f829b-104">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="f829b-104">Updating messages</span></span>

<span data-ttu-id="f829b-105">Вместо того чтобы сообщения были статическими моментальными снимками данных, ваш Bot может динамически обновлять сообщения после их отправки.</span><span class="sxs-lookup"><span data-stu-id="f829b-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="f829b-106">Динамическое обновление сообщений можно использовать для таких сценариев, как обновление опросов, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.</span><span class="sxs-lookup"><span data-stu-id="f829b-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="f829b-107">Новое сообщение не должно быть соответствующим исходному типу.</span><span class="sxs-lookup"><span data-stu-id="f829b-107">The new message need not match the original in type.</span></span> <span data-ttu-id="f829b-108">Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="f829b-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f829b-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f829b-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f829b-110">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `UpdateActivityAsync` метод `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="f829b-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="f829b-111">*Просмотр* [турнконтексткласс](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="f829b-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f829b-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f829b-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="f829b-113">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `updateActivity` метод `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="f829b-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f829b-114">*Просмотр* [упдатеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="f829b-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="f829b-115">Python</span><span class="sxs-lookup"><span data-stu-id="f829b-115">Python</span></span>](#tab/python)

<span data-ttu-id="f829b-116">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `update_activity` метод `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="f829b-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="f829b-117">Обратитесь к разделу [турнконтексткласс](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="f829b-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="f829b-118">REST API</span><span class="sxs-lookup"><span data-stu-id="f829b-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="f829b-119">Вы можете разрабатывать приложения Teams в любой технологии веб-программирования и напрямую вызывать [API REST службы соединителя Bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span><span class="sxs-lookup"><span data-stu-id="f829b-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span></span> <span data-ttu-id="f829b-120">Для этого необходимо реализовать процедуры безопасности [проверки подлинности](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) с помощью запросов API.</span><span class="sxs-lookup"><span data-stu-id="f829b-120">To do so, you'll need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) security procedures with your API requests.</span></span>

<span data-ttu-id="f829b-121">Чтобы обновить существующее действие в беседе, включите в конечную точку запроса `conversationId` и `activityId` .</span><span class="sxs-lookup"><span data-stu-id="f829b-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="f829b-122">Для выполнения этого сценария необходимо кэшировать идентификатор действия, возвращенный исходным вызовом POST.</span><span class="sxs-lookup"><span data-stu-id="f829b-122">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="f829b-123">**Основной текст запроса**</span><span class="sxs-lookup"><span data-stu-id="f829b-123">**Request body**</span></span> | <span data-ttu-id="f829b-124">Объект [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object)</span><span class="sxs-lookup"><span data-stu-id="f829b-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object) object</span></span> |
| <span data-ttu-id="f829b-125">**Возвращаемое значение**</span><span class="sxs-lookup"><span data-stu-id="f829b-125">**Returns**</span></span> | <span data-ttu-id="f829b-126">Объект [ресаурцереспонсе](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object)</span><span class="sxs-lookup"><span data-stu-id="f829b-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object) object</span></span> |

---

## <a name="deleting-messages"></a><span data-ttu-id="f829b-127">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="f829b-127">Deleting messages</span></span>

<span data-ttu-id="f829b-128">В Bot Framework каждое сообщение имеет собственный уникальный идентификатор действия.</span><span class="sxs-lookup"><span data-stu-id="f829b-128">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="f829b-129">Сообщения можно удалять с помощью `DeleteActivity` метода Bot Framework, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f829b-129">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f829b-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f829b-130">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f829b-131">Чтобы удалить это сообщение, передайте идентификатор действия `DeleteActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="f829b-131">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="f829b-132">*Просмотр* [метода турнконтекст. делетеактивитясинк](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="f829b-132">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f829b-133">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f829b-133">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="f829b-134">Чтобы удалить это сообщение, передайте идентификатор действия `deleteActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="f829b-134">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f829b-135">*Просмотр* [делетеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="f829b-135">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="f829b-136">Python</span><span class="sxs-lookup"><span data-stu-id="f829b-136">Python</span></span>](#tab/python)

<span data-ttu-id="f829b-137">Чтобы удалить это сообщение, передайте идентификатор действия `delete_activity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="f829b-137">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f829b-138">См. [действие действия — обновление и удаление](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="f829b-138">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="f829b-139">REST API</span><span class="sxs-lookup"><span data-stu-id="f829b-139">REST API</span></span>](#tab/rest)

 <span data-ttu-id="f829b-140">Чтобы удалить существующее действие в беседе, включите в конечную точку запроса `conversationId` и `activityId` .</span><span class="sxs-lookup"><span data-stu-id="f829b-140">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="f829b-141">**Основной текст запроса**</span><span class="sxs-lookup"><span data-stu-id="f829b-141">**Request body**</span></span> | <span data-ttu-id="f829b-142">н/д</span><span class="sxs-lookup"><span data-stu-id="f829b-142">n/a</span></span> |
| <span data-ttu-id="f829b-143">**Возвращаемое значение**</span><span class="sxs-lookup"><span data-stu-id="f829b-143">**Returns**</span></span> | <span data-ttu-id="f829b-144">Код состояния HTTP, указывающий результат операции.</span><span class="sxs-lookup"><span data-stu-id="f829b-144">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="f829b-145">В тексте ответа ничего не указывается.</span><span class="sxs-lookup"><span data-stu-id="f829b-145">Nothing is specified in the body of the response.</span></span> |

---
