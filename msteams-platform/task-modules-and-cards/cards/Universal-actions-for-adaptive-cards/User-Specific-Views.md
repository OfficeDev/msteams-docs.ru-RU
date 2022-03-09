---
title: Пользовательские просмотры
description: Узнайте о пользовательских представлениях с использованием универсальных действий с образцом кода
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 284fda042d5862929004f7809aea9080d0c5d3fd
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356366"
---
# <a name="user-specific-views"></a>Пользовательские просмотры

Ранее, если адаптивные карточки были отправлены в беседе Teams, все пользователи видят одно и то же содержимое карты. С введением модели универсальных `refresh` действий и адаптивных карт разработчики ботов теперь могут предоставлять пользователям специальные представления адаптивных карт. Теперь та же адаптивная карта может обновиться до специальной адаптивной карты пользователя. Не более 60 разных пользователей могут видеть другую версию карты с дополнительной информацией или действиями. Адаптивная карта предоставляет мощные сценарии, такие как утверждения, элементы управления создателями опросов, билеты, управление инцидентами и карты управления проектами.

> [!NOTE]
> Пользовательское представление поддерживается для адаптивных карт, отправленных ботом, и зависит от универсальных действий.

Например, Меган, инспектор безопасности в Contoso, хочет создать инцидент и назначить его Алексу. Меган также хочет, чтобы все в команде знали об инциденте. Меган использует расширение сообщений об инцидентах Contoso с питанием от универсальных действий для адаптивных карт.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Представления для мобильных пользователей":::

# <a name="desktop"></a>[Компьютер](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Пользовательские просмотры":::

* * *

## <a name="user-specific-views-for-adaptive-cards"></a>Пользовательские представления для адаптивных карт

В следующем коде приводится пример адаптивных карт:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView",
      "data": {
            "refresh info": "<refresh info>"
      }
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ]
}
```

**Чтобы отправить адаптивные карты, обновить пользовательские представления и вызвать запросы к боту**

1. Когда Меган создает новый инцидент, бот отправляет адаптивную карту или общую карту с сведениями об инциденте в Teams беседе.
2. Теперь эта карта автоматически обновляется до пользовательского представления для Меган и Алекс. МРИС пользователя `userIds` `refresh` Алекса и Меган добавляются в свойство свойства адаптивной карты JSON. Карта остается той же для других пользователей в беседе.
3. Для Меган автоматическое обновление вызывает запрос `adaptiveCard/action` на вызов бота. Бот может вернуть карточку создателя инцидента с помощью кнопки `Edit` в качестве ответа на этот запрос на вызов.
4. Аналогично для Alex автоматическое обновление вызывает другой запрос `adaptiveCard/action` на вызов бота. Бот может вернуть кнопку карточки владельца инцидента `Resolve` в качестве ответа на этот запрос на вызов.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Вызов запроса, отправленного Teams клиента боту

В следующем коде приводится пример запроса на вызов, отправленного от клиента Алекса и Меган Teams боту:

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "editOrResolveView",
      "data": { 
            "refresh info": "<refresh info>"
      } 
    },
    "trigger": "automatic" 
  }
}
```

## <a name="adaptivecardaction-invoke-response-card"></a>adaptiveCard/action вызывает карточку ответа

В следующем коде приводится пример адаптивной карты/действия, вызываемой для Меган:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Edit",
      "verb": "edit",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action вызывает карточку ответа для Alex

В следующем коде приводится пример адаптивной карточки вызова ответа на действия для Alex:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Refresh",
      "verb": "editOrResolveView"
    },
    "userIds": ["<Megan's user MRI>", "<Alex's user MRI>"]
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Incident 1234"
    },
    {
      "type": "TextBlock",
      "text": "Incident details: <incident details>"
    }
  ],
  "actions": [
    {
      "type": "Action.Execute",
      "title": "Resolve",
      "verb": "resolve",
      "data": {
            "additional info": "<additional info>",
            ...
      }
    }
  ]
}
```

## <a name="invoke-response-to-return-adaptive-cards"></a>Вызов ответа для возврата адаптивных карт

В следующем коде приводится пример ответа на вызов для возврата адаптивных карт:

### <a name="c"></a>[C#](#tab/C)

```csharp
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
var card = "<adaptive card json>";
 
const cardRes = {
        statusCode: 200,
        type: 'application/vnd.microsoft.card.adaptive',
        value: card
    };
    const res = {
        status: 200,
        body: cardRes
    };
    return res;

```

---

Рекомендации по разработке карт, которые необходимо иметь в виду при разработке пользовательских представлений:

* Можно создать не более **60** пользовательских представлений для определенной карты, отправленной в чат или канал, указав их `userIds` в разделе `refresh` .
* **Базовая карта:** Базовая версия карты, которую разработчик бота отправляет в чат. Базовая версия — это версия адаптивной карты для всех пользователей, не указанных в разделе `userIds` .
* Обновление сообщения можно использовать для обновления базовой карты и одновременного обновления пользовательской конкретной карты. Открытие чата или канала также обновляет карту для пользователей с включенной поддержкой обновления.
* В сценариях с более крупными группами, в которых пользователи переключаются на представление о действии, которое требует динамических обновлений для ответчиков, можно продолжать добавлять до 60 пользователей в `userIds` список. Первый ответ можно удалить из списка при ответе 61-го пользователя. Для пользователей, которые удаляются `userIds` из списка, вы можете предоставить ручную кнопку обновления или использовать кнопку обновления в меню параметры сообщений, чтобы получить последний результат.
* Дайте пользователям подсказку для получения пользовательского представления, в котором они видят только определенное представление карты или какие-либо действия.

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | .NETCore | Node.js |
|----------------|-----------------|--------------|--------------|
| Адаптивные карточки последовательного рабочего процесса | Демонстрация того, как реализовать последовательное рабочий процесс, пользовательские представления и адаптивные карты в ботах. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-sequential-flow-adaptive-cards/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Просмотры на сегодняшний день](Up-To-Date-Views.md)
* [Отзывы о завершении формы](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
