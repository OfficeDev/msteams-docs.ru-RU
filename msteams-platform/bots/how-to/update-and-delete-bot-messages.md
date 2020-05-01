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
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Обновление и удаление сообщений, отправленных с ленты.

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a>Обновление сообщений

Вместо того чтобы сообщения были статическими моментальными снимками данных, ваш Bot может динамически обновлять сообщения после их отправки. Динамическое обновление сообщений можно использовать для таких сценариев, как обновление опросов, изменение доступных действий после нажатия кнопки или любое другое изменение асинхронного состояния.

Новое сообщение не должно быть соответствующим исходному типу. Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `UpdateActivityAsync` метод `TurnContext` класса. *Просмотр* [турнконтексткласс](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `updateActivity` метод `TurnContext` объекта. *Просмотр* [упдатеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Чтобы обновить существующее сообщение, передайте новый `Activity` объект с существующим идентификатором действия в `update_activity` метод `TurnContext` класса. Обратитесь к разделу [турнконтексткласс](link to Python API ref docs).

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[REST API](#tab/rest)

>[!NOTE]
>Вы можете разрабатывать приложения Teams в любой технологии веб-программирования и напрямую вызывать [API REST службы соединителя Bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0). Для этого необходимо реализовать процедуры безопасности [проверки подлинности](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) с помощью запросов API.

Чтобы обновить существующее действие в беседе, включите в конечную точку запроса `conversationId` и `activityId` . Для выполнения этого сценария необходимо кэшировать идентификатор действия, возвращенный исходным вызовом POST.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **Основной текст запроса** | Объект [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object) |
| **Возвращаемое значение** | Объект [ресаурцереспонсе](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object) |

---

## <a name="deleting-messages"></a>Удаление сообщений

В Bot Framework каждое сообщение имеет собственный уникальный идентификатор действия.
Сообщения можно удалять с помощью `DeleteActivity` метода Bot Framework, как показано ниже.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Чтобы удалить это сообщение, передайте идентификатор действия `DeleteActivityAsync` методу `TurnContext` класса. *Просмотр* [метода турнконтекст. делетеактивитясинк](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

Чтобы удалить это сообщение, передайте идентификатор действия `deleteActivity` методу `TurnContext` объекта. *Просмотр* [делетеактивити](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Чтобы удалить это сообщение, передайте идентификатор действия `delete_activity` методу `TurnContext` объекта. См. [действие действия — обновление и удаление](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

 Чтобы удалить существующее действие в беседе, включите в конечную точку запроса `conversationId` и `activityId` .

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **Основной текст запроса** | н/д |
| **Возвращаемое значение** | Код состояния HTTP, указывающий результат операции. В тексте ответа ничего не указывается. |

---
