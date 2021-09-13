---
title: Обновление и удаление сообщений, отправленных из бота
author: WashingtonKayaker
description: Обновление и удаление сообщений, отправленных из Microsoft Teams бота
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 2db2ad28da41fd464f82ce5836acc8202f118923
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156337"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Обновление и удаление сообщений, отправленных из бота

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Ваш бот может динамически обновлять сообщения после отправки, а не иметь их в виде статических снимков данных. Сообщения также можно удалить с помощью метода Bot `DeleteActivity` Framework.

## <a name="update-messages"></a>Обновление сообщений

Динамические обновления сообщений можно использовать для сценариев, таких как обновления опросов, изменение доступных действий после нажатия кнопки или любое другое асинхронное изменение состояния.

Новое сообщение не обязательно соответствует исходному типу. Например, если исходное сообщение содержит вложение, новое сообщение может быть простым текстовым сообщением.

# <a name="c"></a>[C#](#tab/dotnet)

Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `UpdateActivityAsync` методу `TurnContext` класса. Дополнительные сведения см. в [тексте TurnContextClass.](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `updateActivity` методу `TurnContext` объекта. Дополнительные сведения см. [в обновленной версииActivity.](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Чтобы обновить существующее сообщение, передай новый объект с существующим ИД действий `Activity` `update_activity` методу `TurnContext` класса. См. [turnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]

> Вы можете разрабатывать Teams в любой технологии веб-программирования и напрямую вызывать API REST службы [Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) Для этого необходимо реализовать [](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) процедуры безопасности проверки подлинности с помощью запросов API.

Чтобы обновить существующее действие в беседе, включив конечную точку запроса и в `conversationId` `activityId` нее. Чтобы завершить этот сценарий, необходимо кэшировали ID активности, возвращаемую исходным вызовом после.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Запрос |Отклик |
|----|----|
| Объект [Activity.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) | Объект [ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) |

---
* * *

Теперь, когда у вас есть обновленные сообщения, обнови существующую карту на выбор кнопок для входящих действий.

## <a name="update-cards"></a>Обновление карт

Чтобы обновить существующую карту при выборе кнопки, можно использовать `ReplyToId` входящие действия.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Чтобы обновить существующую карту на выбор кнопки, передай новый объект с обновленной картой и в качестве удостоверения действий `Activity` `ReplyToId` `UpdateActivityAsync` методу `TurnContext` класса. См. [turnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Чтобы обновить существующую карту при выборе кнопки, передай новый объект с обновленной картой и в качестве удостоверения активности `Activity` `replyToId` `updateActivity` методу `TurnContext` объекта. См. [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

Чтобы обновить существующую карту нажатием кнопки, передайте новый объект с обновленной картой и в качестве удостоверения действий `Activity` `reply_to_id` `update_activity` методу `TurnContext` класса. См. [turnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> Вы можете разрабатывать Teams в любой технологии веб-программирования и напрямую вызывать [API-API](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)службы подключения ботов. Для этого необходимо реализовать [процедуры](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) безопасности проверки подлинности с помощью запросов API.

Чтобы обновить существующее действие в беседе, включив конечную точку запроса и в `conversationId` `activityId` нее. Чтобы завершить этот сценарий, необходимо кэшировали ID активности, возвращаемую исходным вызовом после.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Запрос |Отклик |
|----|----|
| Объект [активности.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) | Объект [ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) |

* * *

Теперь, когда у вас есть обновленные карты, вы можете удалять сообщения с помощью Bot Framework.

## <a name="delete-messages"></a>Удаление сообщений

В bot Framework каждое сообщение имеет свой уникальный идентификатор активности. Сообщения можно удалить с помощью метода Bot `DeleteActivity` Framework.

# <a name="c"></a>[C#](#tab/dotnet)

Чтобы удалить сообщение, передайте его ID `DeleteActivityAsync` методу `TurnContext` класса. Дополнительные сведения см. в [методе TurnContext.DeleteActivityAsync.](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Чтобы удалить сообщение, передайте его ID `deleteActivity` методу `TurnContext` объекта. Дополнительные сведения см. в [публикации deleteActivity.](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Чтобы удалить это сообщение, передайте его ID `delete_activity` методу `TurnContext` объекта. Дополнительные сведения см. [в публикации activity-update-and-delete.](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

Чтобы удалить существующее действие в беседе, включите конечную точку запроса и в `conversationId` `activityId` нее.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **Запрос и ответ** | **Описание** |
|----|----|
| Н/Д | Код состояния HTTP, указывающий результат операции. В теле ответа ничего не указывается. |

---

## <a name="code-sample"></a>Пример кода

В следующем примере кода демонстрируются основы бесед:

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Teams Основы беседы  | Демонстрирует основы бесед в Teams, включая обновление и удаление сообщений. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Получить Teams контекст](~/bots/how-to/get-teams-context.md)
