---
title: Пользовательские просмотры
description: Пример для пользовательских конкретных представлений с использованием универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 696fc5ce25c79d749b301309bfe0c737e39ad294
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555446"
---
# <a name="user-specific-views"></a>Пользовательские просмотры

Ранее, если адаптивные карты были отправлены в Teams разговоре, все пользователи видят точно такой же контент карты. С введением модели Универсальные действия и для `refresh` адаптивных карт, разработчики ботов теперь могут предоставлять пользователям конкретные представления адаптивных карт для пользователей. Та же адаптивная карта теперь может обновляться до конкретной адаптивной карты пользователя.

Например, Меган, инспектор безопасности в Contoso, хочет создать инцидент и назначить его Алексу. Она также хочет, чтобы все в команде были в курсе инцидента. Меган использует Contoso инцидент отчетности сообщение расширение питание от универсальных действий для адаптивных карт.

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="Пользовательские просмотры":::

## <a name="user-specific-views-for-adaptive-cards"></a>Пользовательские конкретные представления для адаптивных карт

В следующем коде приведен пример адаптивных карт:

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

**Отправка адаптивных карт, обновление пользовательских представлений и вызов запросов боту**

1. Когда Меган создает новый инцидент, бот отправляет адаптивную карту или общую карту с деталями инцидента в Teams разговоре.
2. Теперь эта карта автоматически обновляется до user Specific View для Меган и Алекса. Пользовательские МИИ Алекса и Меган добавляются в `userIds` собственность `refresh` адаптивной карты JSON. Карта остается прежней для других пользователей в разговоре.
3. Для Меган автоматическое обновление вызывает запрос `adaptiveCard/action` на вызов бота. Бот может вернуть карту создателя инцидента с `Edit` кнопкой в ответ на этот запрос вызова.
4. Аналогичным образом для Alex автоматическое обновление вызывает еще один `adaptiveCard/action` запрос вызова для бота. Бот может вернуть кнопку карты владельца инцидента `Resolve` в ответ на этот запрос вызова.

## <a name="invoke-request-sent-from-teams-client-to-the-bot"></a>Запрос на вызов, отправленный Teams клиента боту

В следующем коде приводится пример запроса на вызов, отправленного от клиента Alex's и Меган Teams клиента боту:

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

## <a name="adaptivecardaction-invoke-response-card"></a>адаптивная Карта/действие вызывают карту ответа

Следующий код служит примером адаптивной карты/действия, на которую ссылается карта реагирования Меган:

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

## <a name="adaptivecardaction-invoke-response-card-for-alex"></a>adaptiveCard/action вызывает карту ответа для Алекса

Следующий код служит примером адаптивной карты/действия, на которую ссылается карта реагирования Alex:

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

## <a name="invoke-response-to-return-adaptive-cards"></a>Вызов ответа на возврат адаптивных карт

Следующий код служит примером ответа на вызов для возврата адаптивных карт:

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

Руководящие принципы проектирования карт, которые нужно иметь в виду при проектировании пользовательских представлений:

* Вы можете создать максимум **60 пользовательских представлений для** конкретной карты, отправляются в чат или канал, указав их `userIds` в `refresh` разделе.
* **Базовая карта:** Базовая версия карты, которую разработчик бота отправляет в чат. Это версия адаптивной карты для всех пользователей, которые не указаны в `userIds` разделе.
* Обновление или редактирование сообщений может быть использовано для обновления базовой карты и одновременного обновления конкретной карты пользователя.

## <a name="see-also"></a>См. также

* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
* [До даты просмотров](Up-To-Date-Views.md)
