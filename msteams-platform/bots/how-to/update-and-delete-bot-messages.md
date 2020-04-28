---
title: Обновление и удаление сообщений, отправленных с ленты.
author: WashingtonKayaker
description: Обновление и удаление сообщений, отправленных с ленты Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 222409fa0d02a571b7295dedb0c60b1ca3f90cca
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914611"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="64797-103">Обновление и удаление сообщений, отправленных с ленты.</span><span class="sxs-lookup"><span data-stu-id="64797-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="64797-104">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="64797-104">Updating messages</span></span>

<span data-ttu-id="64797-105">Вместо того чтобы сообщения были статическими моментальными снимками данных, ваш Bot может динамически обновлять сообщения после их отправки.</span><span class="sxs-lookup"><span data-stu-id="64797-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="64797-106">Динамическое обновление сообщений можно использовать для таких сценариев, как обновление опросов, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.</span><span class="sxs-lookup"><span data-stu-id="64797-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="64797-107">Новое сообщение не должно быть соответствующим исходному типу.</span><span class="sxs-lookup"><span data-stu-id="64797-107">The new message need not match the original in type.</span></span> <span data-ttu-id="64797-108">Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="64797-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="64797-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="64797-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="64797-110">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `UpdateActivityAsync` метод `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="64797-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="64797-111">*Просмотр* [турнконтексткласс](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="64797-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="64797-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="64797-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="64797-113">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `updateActivity` метод `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="64797-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="64797-114">*Просмотр* [упдатеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="64797-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="64797-115">Python</span><span class="sxs-lookup"><span data-stu-id="64797-115">Python</span></span>](#tab/python)

<span data-ttu-id="64797-116">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `update_activity` метод `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="64797-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="64797-117">Обратитесь к разделу [турнконтексткласс](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="64797-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a><span data-ttu-id="64797-118">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="64797-118">Deleting messages</span></span>

<span data-ttu-id="64797-119">В Bot Framework каждое сообщение имеет собственный уникальный идентификатор действия.</span><span class="sxs-lookup"><span data-stu-id="64797-119">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="64797-120">Сообщения можно удалять с помощью `DeleteActivity` метода Bot Framework, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="64797-120">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="64797-121">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="64797-121">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="64797-122">Чтобы удалить это сообщение, передайте идентификатор действия `DeleteActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="64797-122">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="64797-123">*Просмотр* [метода турнконтекст. делетеактивитясинк](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="64797-123">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="64797-124">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="64797-124">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="64797-125">Чтобы удалить это сообщение, передайте идентификатор действия `deleteActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="64797-125">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="64797-126">*Просмотр* [делетеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="64797-126">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="64797-127">Python</span><span class="sxs-lookup"><span data-stu-id="64797-127">Python</span></span>](#tab/python)

<span data-ttu-id="64797-128">Чтобы удалить это сообщение, передайте идентификатор действия `delete_activity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="64797-128">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="64797-129">См. [действие действия — обновление и удаление](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="64797-129">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---

