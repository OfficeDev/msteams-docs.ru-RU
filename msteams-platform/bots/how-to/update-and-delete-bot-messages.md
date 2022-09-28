---
title: Обновляйте и удаляйте сообщения, отправленные ботом
author: WashingtonKayaker
description: Узнайте, как обновлять и удалять сообщения, отправленные из бота Microsoft Teams в разных средах и с помощью REST API, с помощью примеров (.NET, Node.js, Python).
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: d85bb7086661eba58c6cf852cab599970fdc9c80
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100821"
---
# <a name="update-and-delete-messages-sent-from-bot"></a>Обновление и удаление сообщений, отправленных ботом 

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Бот может динамически обновлять сообщения после их отправки, а не сохранять их в виде статических снимков данных. Сообщения также можно удалить с помощью метода `DeleteActivity` Bot Framework.

## <a name="update-messages"></a>Обновление сообщений

Вы можете использовать динамические обновления сообщений для таких сценариев, как обновления опроса, изменение действий, доступных после нажатия кнопки, или любое другое асинхронное изменение состояния.

Новое сообщение не обязательно должно совпадать по типу с исходным. Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.

# <a name="c"></a>[C#](#tab/dotnet)

Чтобы обновить существующее сообщение, передайте новый объект `Activity` с существующим идентификатором действия в метод `UpdateActivityAsync` класса `TurnContext`. Подробнее в разделе [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Чтобы обновить существующее сообщение, передайте новый объект `Activity` с существующим идентификатором действия в метод `updateActivity` объекта `TurnContext`. Подробнее в разделе [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Чтобы обновить существующее сообщение, передайте новый объект `Activity` с существующим идентификатором действия в метод `update_activity` класса `TurnContext`. См. [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> Вы можете разрабатывать приложения Teams с помощью любой технологии веб-программирования и напрямую вызывать [REST API службы соединителя ботов](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Для этого вам необходимо реализовать процедуры безопасности [Проверки подлинности](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) безопасности с вашими запросами API.

Чтобы обновить существующее действие в беседе, включите `conversationId` и `activityId` в конечную точку запроса. Чтобы выполнить этот сценарий, вы должны кэшировать идентификатор действия, возвращенный исходным почтовым вызовом.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Запрос |Отклик |
|----|----|
| Объект [Действия](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true). | Объект [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true). |

---
---

Теперь, когда вы обновили сообщения, обновите существующую карточку при выборе кнопки для входящих действий.

## <a name="update-cards"></a>Обновить карточки

Чтобы обновить существующую карточку при выборе кнопки, вы можете использовать `ReplyToId` входящую активность.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Чтобы обновить существующую карточку при выборе кнопки, передайте новый объект `Activity` с обновленной карточкой и `ReplyToId` как идентификатор действия для метода `UpdateActivityAsync` класса `TurnContext`. См. [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Чтобы обновить существующую карточку при выборе кнопки, передайте новый объект `Activity` с обновленной карточкой и `replyToId` как идентификатор действия для метода `updateActivity` объекта `TurnContext` См. [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

Чтобы обновить существующую карточку при нажатии кнопки, передайте новый объект `Activity` с обновленной карточкой и `reply_to_id` как идентификатор действия для метода `update_activity` класса `TurnContext`. См. [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> Вы можете разрабатывать приложения Teams с помощью любой технологии веб-программирования и напрямую вызывать [REST API службы соединителя ботов](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Для этого вам необходимо реализовать процедуры безопасности [Проверки подлинности](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) безопасности с вашими запросами API.

Чтобы обновить существующее действие в беседе, включите `conversationId` и `activityId` в конечную точку запроса. Чтобы выполнить этот сценарий, вы должны кэшировать идентификатор действия, возвращенный исходным почтовым вызовом.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Запрос |Отклик |
|----|----|
| Объект [Действия](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true). | Объект [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true). |

---

Теперь, когда у вас есть обновленные карточки, вы можете удалять сообщения с помощью Bot Framework.

## <a name="delete-messages"></a>Удаление сообщений

В Bot Framework каждое сообщение имеет уникальный идентификатор действия. Сообщения можно удалить с помощью метода `DeleteActivity` Bot Framework.

# <a name="c"></a>[C#](#tab/dotnet)

Чтобы удалить сообщение, передайте идентификатор этого действия методу `DeleteActivityAsync` класса `TurnContext`. Подробнее см. [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Чтобы удалить сообщение, передайте идентификатор этого действия методу `deleteActivity` объекта `TurnContext`. Подробнее см. [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Чтобы удалить это сообщение, передайте идентификатор этого действия методу `delete_activity` объекта `TurnContext`. Подробнее см. [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

Чтобы удалить существующее действие в беседе, включите `conversationId` и `activityId` в конечную точку запроса.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **Запрос и отклик** | **Описание** |
|----|----|
| Недоступно | Код состояния HTTP, указывающий результат операции. В тексте отклика ничего не указано. |

---

## <a name="code-sample"></a>Пример кода

В следующем образце кода демонстрируются основы бесед.

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Основы бесед в Teams  | Демонстрирует основы бесед в Teams, включая обновление и удаление сообщений. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Получить контекст Teams](~/bots/how-to/get-teams-context.md).
