---
title: Обновление и удаление сообщений, отправленных из бота
author: WashingtonKayaker
description: Обновление и удаление сообщений, отправленных из бота Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 664bd531bdee0093c6766bc23e35d2bf10307eb4
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449502"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="57df7-103">Обновление и удаление сообщений, отправленных из бота</span><span class="sxs-lookup"><span data-stu-id="57df7-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="update-messages"></a><span data-ttu-id="57df7-104">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="57df7-104">Update messages</span></span>

<span data-ttu-id="57df7-105">Ваш бот может динамически обновлять сообщения после их отправки.</span><span class="sxs-lookup"><span data-stu-id="57df7-105">Your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="57df7-106">Динамические обновления сообщений можно использовать для таких сценариев, как обновления опросов, изменение доступных действий после нажатия кнопки или любое другое асинхронное изменение состояния.</span><span class="sxs-lookup"><span data-stu-id="57df7-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="57df7-107">Новое сообщение не соответствует исходному типу.</span><span class="sxs-lookup"><span data-stu-id="57df7-107">The new message need not match the original in type.</span></span> <span data-ttu-id="57df7-108">Например, если исходное сообщение содержало вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="57df7-108">For example, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57df7-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57df7-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="57df7-110">Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `UpdateActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="57df7-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="57df7-111">См. [turnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="57df7-111">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57df7-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57df7-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="57df7-113">Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `updateActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="57df7-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="57df7-114">См. [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="57df7-114">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="57df7-115">Python</span><span class="sxs-lookup"><span data-stu-id="57df7-115">Python</span></span>](#tab/python)

<span data-ttu-id="57df7-116">Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `update_activity` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="57df7-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="57df7-117">См. [turnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span><span class="sxs-lookup"><span data-stu-id="57df7-117">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="57df7-118">REST API</span><span class="sxs-lookup"><span data-stu-id="57df7-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="57df7-119">Вы можете разрабатывать приложения Teams в любой технологии веб-программирования и напрямую вызывать API REST службы [Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="57df7-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="57df7-120">Для этого необходимо реализовать [](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) процедуры безопасности проверки подлинности с помощью запросов API.</span><span class="sxs-lookup"><span data-stu-id="57df7-120">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="57df7-121">Чтобы обновить существующее действие в беседе, включив конечную точку запроса и в `conversationId` `activityId` нее.</span><span class="sxs-lookup"><span data-stu-id="57df7-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="57df7-122">Чтобы завершить этот сценарий, необходимо кэшировали ID действия, возвращенный исходным вызовом POST.</span><span class="sxs-lookup"><span data-stu-id="57df7-122">To complete this scenario, you must cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="57df7-123">**Текст запроса**</span><span class="sxs-lookup"><span data-stu-id="57df7-123">**Request body**</span></span> | <span data-ttu-id="57df7-124">Объект [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="57df7-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object</span></span> |
| <span data-ttu-id="57df7-125">**Возвращаемое значение**</span><span class="sxs-lookup"><span data-stu-id="57df7-125">**Returns**</span></span> | <span data-ttu-id="57df7-126">Объект [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="57df7-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object</span></span> |

---

## <a name="update-cards"></a><span data-ttu-id="57df7-127">Обновление карт</span><span class="sxs-lookup"><span data-stu-id="57df7-127">Update cards</span></span>

<span data-ttu-id="57df7-128">Чтобы обновить существующую карту при выборе кнопки, можно использовать `ReplyToId` входящие действия.</span><span class="sxs-lookup"><span data-stu-id="57df7-128">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57df7-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57df7-129">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="57df7-130">Чтобы обновить существующую карту нажатием кнопки, передайте новый объект с обновленной картой и в качестве удостоверения действий `Activity` `ReplyToId` `UpdateActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="57df7-130">To update existing card on a button click, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="57df7-131">См. [turnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="57df7-131">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>
```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57df7-132">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57df7-132">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="57df7-133">Чтобы обновить существующую карту нажатием кнопки, передайте новый объект с обновленной картой и в качестве удостоверения действий `Activity` `replyToId` `updateActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="57df7-133">To update existing card on a button click, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="57df7-134">См. [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="57df7-134">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>
```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="57df7-135">Python</span><span class="sxs-lookup"><span data-stu-id="57df7-135">Python</span></span>](#tab/python)

<span data-ttu-id="57df7-136">Чтобы обновить существующую карту нажатием кнопки, передайте новый объект с обновленной картой и в качестве удостоверения действий `Activity` `reply_to_id` `update_activity` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="57df7-136">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="57df7-137">См. [turnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span><span class="sxs-lookup"><span data-stu-id="57df7-137">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)

```

## <a name="delete-messages"></a><span data-ttu-id="57df7-138">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="57df7-138">Delete messages</span></span>

<span data-ttu-id="57df7-139">В bot Framework каждое сообщение имеет свой уникальный идентификатор активности.</span><span class="sxs-lookup"><span data-stu-id="57df7-139">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="57df7-140">Сообщения можно удалить с помощью метода Bot `DeleteActivity` Framework, как показано здесь.</span><span class="sxs-lookup"><span data-stu-id="57df7-140">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="57df7-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="57df7-141">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="57df7-142">Чтобы удалить это сообщение, передайте его ID `DeleteActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="57df7-142">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="57df7-143">См. [метод TurnContext.DeleteActivityAsync.](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="57df7-143">See [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="57df7-144">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="57df7-144">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="57df7-145">Чтобы удалить это сообщение, передайте его ID `deleteActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="57df7-145">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="57df7-146">См. [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="57df7-146">See [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="57df7-147">Python</span><span class="sxs-lookup"><span data-stu-id="57df7-147">Python</span></span>](#tab/python)

<span data-ttu-id="57df7-148">Чтобы удалить это сообщение, передайте его ID `delete_activity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="57df7-148">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="57df7-149">См. [в публикации activity-update-and-delete.](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)</span><span class="sxs-lookup"><span data-stu-id="57df7-149">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="57df7-150">REST API</span><span class="sxs-lookup"><span data-stu-id="57df7-150">REST API</span></span>](#tab/rest)

 <span data-ttu-id="57df7-151">Чтобы удалить существующее действие в беседе, включите конечную точку запроса и в `conversationId` `activityId` нее.</span><span class="sxs-lookup"><span data-stu-id="57df7-151">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="57df7-152">**Текст запроса**</span><span class="sxs-lookup"><span data-stu-id="57df7-152">**Request body**</span></span> | <span data-ttu-id="57df7-153">н/д</span><span class="sxs-lookup"><span data-stu-id="57df7-153">n/a</span></span> |
| <span data-ttu-id="57df7-154">**Возвращаемое значение**</span><span class="sxs-lookup"><span data-stu-id="57df7-154">**Returns**</span></span> | <span data-ttu-id="57df7-155">Код состояния HTTP, который указывает результат операции.</span><span class="sxs-lookup"><span data-stu-id="57df7-155">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="57df7-156">В теле ответа ничего не указывается.</span><span class="sxs-lookup"><span data-stu-id="57df7-156">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-samples"></a><span data-ttu-id="57df7-157">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="57df7-157">Code samples</span></span>

<span data-ttu-id="57df7-158">Основные принципы официального разговора:</span><span class="sxs-lookup"><span data-stu-id="57df7-158">The official conversation basics are as follows:</span></span>

| <span data-ttu-id="57df7-159">Имя образца</span><span class="sxs-lookup"><span data-stu-id="57df7-159">Sample Name</span></span>           | <span data-ttu-id="57df7-160">Описание</span><span class="sxs-lookup"><span data-stu-id="57df7-160">Description</span></span>                                                                      | <span data-ttu-id="57df7-161">.NET</span><span class="sxs-lookup"><span data-stu-id="57df7-161">.NET</span></span>    | <span data-ttu-id="57df7-162">JavaScript</span><span class="sxs-lookup"><span data-stu-id="57df7-162">JavaScript</span></span>   | <span data-ttu-id="57df7-163">Python</span><span class="sxs-lookup"><span data-stu-id="57df7-163">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="57df7-164">Основы беседы teams</span><span class="sxs-lookup"><span data-stu-id="57df7-164">Teams Conversation Basics</span></span>  | <span data-ttu-id="57df7-165">Демонстрирует основы бесед в Teams, включая обновление и удаление сообщений.</span><span class="sxs-lookup"><span data-stu-id="57df7-165">Demonstrates basics of conversations in Teams, including message update and delete.</span></span>|[<span data-ttu-id="57df7-166">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="57df7-166">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="57df7-167">JavaScript</span><span class="sxs-lookup"><span data-stu-id="57df7-167">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="57df7-168">Python</span><span class="sxs-lookup"><span data-stu-id="57df7-168">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
