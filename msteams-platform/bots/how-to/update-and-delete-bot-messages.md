---
title: Обновление и удаление сообщений, отправленных из бота
author: WashingtonKayaker
description: Обновление и удаление сообщений, отправленных из бота Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a2836d59c22b9784f1f1a0c84306072bb6a97d3e
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996004"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="a28cd-103">Обновление и удаление сообщений, отправленных из бота</span><span class="sxs-lookup"><span data-stu-id="a28cd-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="a28cd-104">Ваш бот может динамически обновлять сообщения после отправки, а не иметь их в виде статических снимков данных.</span><span class="sxs-lookup"><span data-stu-id="a28cd-104">Your bot can dynamically update messages after sending them instead of having them as static snapshots of data.</span></span> <span data-ttu-id="a28cd-105">Сообщения также можно удалить с помощью метода Bot `DeleteActivity` Framework.</span><span class="sxs-lookup"><span data-stu-id="a28cd-105">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="update-messages"></a><span data-ttu-id="a28cd-106">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="a28cd-106">Update messages</span></span>

<span data-ttu-id="a28cd-107">Динамические обновления сообщений можно использовать для сценариев, таких как обновления опросов, изменение доступных действий после нажатия кнопки или любое другое асинхронное изменение состояния.</span><span class="sxs-lookup"><span data-stu-id="a28cd-107">You can use dynamic message updates for scenarios, such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="a28cd-108">Новое сообщение не обязательно соответствует исходному типу.</span><span class="sxs-lookup"><span data-stu-id="a28cd-108">It is not necessary for the new message to match the original in type.</span></span> <span data-ttu-id="a28cd-109">Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="a28cd-109">For example, if the original message contains an attachment, the new message can be a simple text message.</span></span>

# <a name="c"></a>[<span data-ttu-id="a28cd-110">C#</span><span class="sxs-lookup"><span data-stu-id="a28cd-110">C#</span></span>](#tab/dotnet)

<span data-ttu-id="a28cd-111">Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `UpdateActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="a28cd-111">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="a28cd-112">Дополнительные сведения см. в [тексте TurnContextClass.](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-112">For more information, see [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="a28cd-113">TypeScript</span><span class="sxs-lookup"><span data-stu-id="a28cd-113">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="a28cd-114">Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `updateActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="a28cd-114">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="a28cd-115">Дополнительные сведения см. [в обновленной версииActivity.](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-115">For more information, see [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="a28cd-116">Python</span><span class="sxs-lookup"><span data-stu-id="a28cd-116">Python</span></span>](#tab/python)

<span data-ttu-id="a28cd-117">Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `update_activity` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="a28cd-117">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="a28cd-118">См. [turnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a28cd-118">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="a28cd-119">REST API</span><span class="sxs-lookup"><span data-stu-id="a28cd-119">REST API</span></span>](#tab/rest)

> [!NOTE]

> <span data-ttu-id="a28cd-120">Вы можете разрабатывать приложения Teams в любой технологии веб-программирования и напрямую вызывать API REST службы [Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-120">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="a28cd-121">Для этого необходимо реализовать [](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) процедуры безопасности проверки подлинности с помощью запросов API.</span><span class="sxs-lookup"><span data-stu-id="a28cd-121">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="a28cd-122">Чтобы обновить существующее действие в беседе, включив конечную точку запроса и в `conversationId` `activityId` нее.</span><span class="sxs-lookup"><span data-stu-id="a28cd-122">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="a28cd-123">Чтобы завершить этот сценарий, необходимо кэшировали ID активности, возвращаемую исходным вызовом после.</span><span class="sxs-lookup"><span data-stu-id="a28cd-123">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| <span data-ttu-id="a28cd-124">**Запрос и responce**</span><span class="sxs-lookup"><span data-stu-id="a28cd-124">**Request and Responce**</span></span> | <span data-ttu-id="a28cd-125">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a28cd-125">**Description**</span></span> |
|----|----|
| <span data-ttu-id="a28cd-126">Объект [активности](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-126">An [activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object</span></span> | <span data-ttu-id="a28cd-127">Объект [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-127">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object</span></span> |

---
* * *

<span data-ttu-id="a28cd-128">Теперь, когда у вас есть обновленные сообщения, обнови существующую карту на выбор кнопок для входящих действий.</span><span class="sxs-lookup"><span data-stu-id="a28cd-128">Now that you have updated messages, update the existing card on button selection for incoming activities.</span></span>

## <a name="update-cards"></a><span data-ttu-id="a28cd-129">Обновление карт</span><span class="sxs-lookup"><span data-stu-id="a28cd-129">Update cards</span></span>

<span data-ttu-id="a28cd-130">Чтобы обновить существующую карту при выборе кнопки, можно использовать `ReplyToId` входящие действия.</span><span class="sxs-lookup"><span data-stu-id="a28cd-130">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="a28cd-131">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="a28cd-131">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="a28cd-132">Чтобы обновить существующую карту на выбор кнопки, передай новый объект с обновленной картой и в качестве удостоверения действий `Activity` `ReplyToId` `UpdateActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="a28cd-132">To update existing card on a button selection, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="a28cd-133">См. [turnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a28cd-133">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="a28cd-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="a28cd-134">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="a28cd-135">Чтобы обновить существующую карту при выборе кнопки, передай новый объект с обновленной картой и в качестве удостоверения активности `Activity` `replyToId` `updateActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="a28cd-135">To update existing card on a button selection, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="a28cd-136">См. [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a28cd-136">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="a28cd-137">Python</span><span class="sxs-lookup"><span data-stu-id="a28cd-137">Python</span></span>](#tab/python)

<span data-ttu-id="a28cd-138">Чтобы обновить существующую карту нажатием кнопки, передайте новый объект с обновленной картой и в качестве удостоверения действий `Activity` `reply_to_id` `update_activity` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="a28cd-138">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="a28cd-139">См. [turnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a28cd-139">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="a28cd-140">REST API</span><span class="sxs-lookup"><span data-stu-id="a28cd-140">REST API</span></span>](#tab/rest)

> [!NOTE]
> <span data-ttu-id="a28cd-141">Вы можете разрабатывать приложения Teams в любой технологии веб-программирования и напрямую вызывать API службы подключения [ботов REST.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-141">You can develop Teams apps in any web programming technology and directly call the [bot connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="a28cd-142">Для этого необходимо реализовать [процедуры](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) безопасности проверки подлинности с помощью запросов API.</span><span class="sxs-lookup"><span data-stu-id="a28cd-142">To do this, you must implement [authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="a28cd-143">Чтобы обновить существующее действие в беседе, включив конечную точку запроса и в `conversationId` `activityId` нее.</span><span class="sxs-lookup"><span data-stu-id="a28cd-143">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="a28cd-144">Чтобы завершить этот сценарий, необходимо кэшировали ID активности, возвращаемую исходным вызовом после.</span><span class="sxs-lookup"><span data-stu-id="a28cd-144">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="a28cd-145">Запрос</span><span class="sxs-lookup"><span data-stu-id="a28cd-145">Request</span></span> |<span data-ttu-id="a28cd-146">Отклик</span><span class="sxs-lookup"><span data-stu-id="a28cd-146">Response</span></span> |
|----|----|
| <span data-ttu-id="a28cd-147">Объект [активности.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-147">An [activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="a28cd-148">Объект [ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-148">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

* * *

<span data-ttu-id="a28cd-149">Теперь, когда у вас есть обновленные карты, вы можете удалять сообщения с помощью Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a28cd-149">Now that you have updated cards, you can delete messages using the Bot Framework.</span></span>

## <a name="delete-messages"></a><span data-ttu-id="a28cd-150">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="a28cd-150">Delete messages</span></span>

<span data-ttu-id="a28cd-151">В bot Framework каждое сообщение имеет свой уникальный идентификатор активности.</span><span class="sxs-lookup"><span data-stu-id="a28cd-151">In the Bot Framework, every message has its unique activity identifier.</span></span> <span data-ttu-id="a28cd-152">Сообщения можно удалить с помощью метода Bot `DeleteActivity` Framework.</span><span class="sxs-lookup"><span data-stu-id="a28cd-152">Messages can be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

# <a name="c"></a>[<span data-ttu-id="a28cd-153">C#</span><span class="sxs-lookup"><span data-stu-id="a28cd-153">C#</span></span>](#tab/dotnet)

<span data-ttu-id="a28cd-154">Чтобы удалить сообщение, передайте его ID `DeleteActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="a28cd-154">To delete a message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="a28cd-155">Дополнительные сведения см. в [методе TurnContext.DeleteActivityAsync.](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-155">For more information, see [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="a28cd-156">TypeScript</span><span class="sxs-lookup"><span data-stu-id="a28cd-156">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="a28cd-157">Чтобы удалить сообщение, передайте его ID `deleteActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="a28cd-157">To delete a message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="a28cd-158">Дополнительные сведения см. в [публикации deleteActivity.](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="a28cd-158">For more information, see [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="a28cd-159">Python</span><span class="sxs-lookup"><span data-stu-id="a28cd-159">Python</span></span>](#tab/python)

<span data-ttu-id="a28cd-160">Чтобы удалить это сообщение, передайте его ID `delete_activity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="a28cd-160">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="a28cd-161">Дополнительные сведения см. [в публикации activity-update-and-delete.](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)</span><span class="sxs-lookup"><span data-stu-id="a28cd-161">For more information, see [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="a28cd-162">REST API</span><span class="sxs-lookup"><span data-stu-id="a28cd-162">REST API</span></span>](#tab/rest)

<span data-ttu-id="a28cd-163">Чтобы удалить существующее действие в беседе, включите конечную точку запроса и в `conversationId` `activityId` нее.</span><span class="sxs-lookup"><span data-stu-id="a28cd-163">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| <span data-ttu-id="a28cd-164">**Запрос и responce**</span><span class="sxs-lookup"><span data-stu-id="a28cd-164">**Request and Responce**</span></span> | <span data-ttu-id="a28cd-165">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a28cd-165">**Description**</span></span> |
|----|----|
| <span data-ttu-id="a28cd-166">Недоступно</span><span class="sxs-lookup"><span data-stu-id="a28cd-166">N/A</span></span> | <span data-ttu-id="a28cd-167">Код состояния HTTP, который указывает результат операции.</span><span class="sxs-lookup"><span data-stu-id="a28cd-167">An HTTP status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="a28cd-168">В теле ответа ничего не указывается.</span><span class="sxs-lookup"><span data-stu-id="a28cd-168">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-sample"></a><span data-ttu-id="a28cd-169">Пример кода</span><span class="sxs-lookup"><span data-stu-id="a28cd-169">Code sample</span></span>

<span data-ttu-id="a28cd-170">В следующем примере кода демонстрируются основы бесед:</span><span class="sxs-lookup"><span data-stu-id="a28cd-170">The following code sample demonstrates basics of conversations:</span></span>

| <span data-ttu-id="a28cd-171">**Имя образца**</span><span class="sxs-lookup"><span data-stu-id="a28cd-171">**Sample Name**</span></span> | <span data-ttu-id="a28cd-172">**Описание**</span><span class="sxs-lookup"><span data-stu-id="a28cd-172">**Description**</span></span> | <span data-ttu-id="a28cd-173">**.NET**</span><span class="sxs-lookup"><span data-stu-id="a28cd-173">**.NET**</span></span> | <span data-ttu-id="a28cd-174">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="a28cd-174">**Node.js**</span></span> | <span data-ttu-id="a28cd-175">**Python**</span><span class="sxs-lookup"><span data-stu-id="a28cd-175">**Python**</span></span> |
|----------------------|-----------------|--------|-------------|--------|
| <span data-ttu-id="a28cd-176">Основы беседы teams</span><span class="sxs-lookup"><span data-stu-id="a28cd-176">Teams Conversation Basics</span></span>  | <span data-ttu-id="a28cd-177">Демонстрирует основы бесед в Teams, включая обновление и удаление сообщений.</span><span class="sxs-lookup"><span data-stu-id="a28cd-177">Demonstrates basics of conversations in Teams including message update and delete.</span></span> | [<span data-ttu-id="a28cd-178">View</span><span class="sxs-lookup"><span data-stu-id="a28cd-178">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="a28cd-179">View</span><span class="sxs-lookup"><span data-stu-id="a28cd-179">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="a28cd-180">View</span><span class="sxs-lookup"><span data-stu-id="a28cd-180">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="a28cd-181">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="a28cd-181">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a28cd-182">Контекст Get Teams</span><span class="sxs-lookup"><span data-stu-id="a28cd-182">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)
