---
title: Обновление и удаление сообщений, отправленных с ленты.
author: WashingtonKayaker
description: Обновление и удаление сообщений, отправленных с ленты Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 012a6edb77f75c43cff01c58fb94e03fd4f61a85
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675552"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="5226a-103">Обновление и удаление сообщений, отправленных с ленты.</span><span class="sxs-lookup"><span data-stu-id="5226a-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="5226a-104">Обновление сообщений</span><span class="sxs-lookup"><span data-stu-id="5226a-104">Updating messages</span></span>

<span data-ttu-id="5226a-105">Вместо того чтобы сообщения были статическими моментальными снимками данных, ваш Bot может динамически обновлять сообщения после их отправки.</span><span class="sxs-lookup"><span data-stu-id="5226a-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="5226a-106">Динамическое обновление сообщений можно использовать для таких сценариев, как обновление опросов, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.</span><span class="sxs-lookup"><span data-stu-id="5226a-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="5226a-107">Новое сообщение не должно быть соответствующим исходному типу.</span><span class="sxs-lookup"><span data-stu-id="5226a-107">The new message need not match the original in type.</span></span> <span data-ttu-id="5226a-108">Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.</span><span class="sxs-lookup"><span data-stu-id="5226a-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="5226a-109">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="5226a-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="5226a-110">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `UpdateActivityAsync` метод `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="5226a-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="5226a-111">*Просмотр* [турнконтексткласс](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="5226a-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="5226a-112">TypeScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="5226a-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="5226a-113">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `updateActivity` метод `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="5226a-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="5226a-114">*Просмотр* [упдатеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="5226a-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="5226a-115">Python</span><span class="sxs-lookup"><span data-stu-id="5226a-115">Python</span></span>](#tab/python)

<span data-ttu-id="5226a-116">Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `update_activity` метод `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="5226a-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="5226a-117">Обратитесь к разделу [турнконтексткласс](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="5226a-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a><span data-ttu-id="5226a-118">Удаление сообщений</span><span class="sxs-lookup"><span data-stu-id="5226a-118">Deleting messages</span></span>

<span data-ttu-id="5226a-119">В Bot Framework каждое сообщение имеет собственный уникальный идентификатор действия.</span><span class="sxs-lookup"><span data-stu-id="5226a-119">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="5226a-120">Сообщения можно удалять с помощью `DeleteActivity` метода Bot Framework, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5226a-120">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="5226a-121">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="5226a-121">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="5226a-122">Чтобы удалить это сообщение, передайте идентификатор действия `DeleteActivityAsync` методу `TurnContext` класса.</span><span class="sxs-lookup"><span data-stu-id="5226a-122">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="5226a-123">*Просмотр* [метода турнконтекст. делетеактивитясинк](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="5226a-123">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="5226a-124">TypeScript/Node. js</span><span class="sxs-lookup"><span data-stu-id="5226a-124">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="5226a-125">Чтобы удалить это сообщение, передайте идентификатор действия `deleteActivity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="5226a-125">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="5226a-126">*Просмотр* [делетеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="5226a-126">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="pythontabpython"></a>[<span data-ttu-id="5226a-127">Python</span><span class="sxs-lookup"><span data-stu-id="5226a-127">Python</span></span>](#tab/python)

<span data-ttu-id="5226a-128">Чтобы удалить это сообщение, передайте идентификатор действия `delete_activity` методу `TurnContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="5226a-128">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="5226a-129">Просмотрите [delete_activity](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="5226a-129">See [delete_activity](link to Python API ref docs).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---

