---
title: Пользовательские просмотры
description: Пример для пользовательских представлений с помощью универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: c24697b300d07ed53a172df162d0d3851361f579
ms.sourcegitcommit: 37325179a532897fafbe827dcf9a7ca5fa5e7d0b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/09/2021
ms.locfileid: "52853517"
---
# <a name="user-specific-views"></a>Пользовательские просмотры

Ранее, если адаптивные карты были отправлены в беседе Teams, все пользователи видят одно и то же содержимое карты. С введением модели универсальных действий и адаптивных карт разработчики ботов теперь могут предоставлять пользователям специальные представления `refresh` адаптивных карт. Теперь та же адаптивная карта может обновиться до специальной адаптивной карты пользователя. Не более 60 разных пользователей могут видеть другую версию карты с дополнительной информацией или действиями. Это обеспечивает мощные сценарии, такие как утверждения, элементы управления создателями опросов, билеты, управление инцидентами и карты управления проектами.

Например, Меган, инспектор безопасности в Contoso, хочет создать инцидент и назначить его Алексу. Она также хочет, чтобы все в команде знали об инциденте. Меган использует расширение сообщений об инцидентах Contoso с питанием от универсальных действий для адаптивных карт.

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="Представления для мобильных пользователей":::

# <a name="desktop"></a>[Desktop](#tab/desktop)

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
2. Теперь эта карта автоматически обновляется до пользовательского представления для Меган и Алекс. МРИС пользователя Алекса и Меган добавляются в свойство `userIds` `refresh` свойства адаптивной карты JSON. Карта остается той же для других пользователей в беседе.
3. Для Меган автоматическое обновление вызывает запрос `adaptiveCard/action` на вызов бота. Бот может вернуть карточку создателя инцидента с помощью `Edit` кнопки в качестве ответа на этот запрос на вызов.
4. Аналогично для Alex автоматическое обновление вызывает другой запрос `adaptiveCard/action` на вызов бота. Бот может вернуть кнопку карточки владельца инцидента `Resolve` в качестве ответа на этот запрос на вызов.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Вызов запроса, отосланного Teams клиента боту

В следующем коде приводится пример запроса на вызов, отосланного от Teams клиента Алекса и Меган в бот:

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

```C#
string cardJson = "<adaptive card json>";
var card = JsonConvert.DeserializeObject(cardJson);

var adaptiveCardResponse = JObject.FromObject(new
 {
    statusCode = 200,
    type = "application/vnd.microsoft.adaptive.card",
    value = card
 });
```

Рекомендации по разработке карт, которые необходимо иметь в виду при разработке пользовательских представлений:

* Можно создать не более **60** пользовательских представлений для определенной карты, отправленной в чат или канал, указав их `userIds` в `refresh` разделе.
* **Базовая карта:** Базовая версия карты, которую разработчик бота отправляет в чат. Это версия адаптивной карты для всех пользователей, не указанных в `userIds` разделе.
* Обновление сообщения можно использовать для обновления базовой карты и одновременного обновления пользовательской конкретной карты. Открытие чата или канала также обновляет карту для пользователей с включенной поддержкой обновления.
* В сценариях с более крупными группами, в которых пользователи переключаются на представление о действии, которое требует динамических обновлений для ответчиков, можно продолжать добавлять до 60 пользователей в `userIds` список. Первый ответ можно удалить из списка при ответе 61-го пользователя. Для пользователей, которые удаляются из списка, вы можете предоставить ручную кнопку обновления или использовать кнопку обновления в меню параметры сообщений, чтобы `userIds` получить последний результат.
* Дайте пользователям подсказку для получения пользовательского представления, в котором они видят только определенное представление карты или какие-либо действия.

## <a name="see-also"></a>См. также

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [Просмотры на сегодняшний день](Up-To-Date-Views.md)
