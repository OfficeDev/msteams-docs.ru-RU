---
title: Последовательные рабочие процессы
description: Пример последовательного рабочего процесса с использованием универсальных действий
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 7f285bf76aac4f0ca276321aee2ce4b4e5c3e7e4
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555404"
---
# <a name="sequential-workflows"></a>Последовательные рабочие процессы

Адаптивные карты теперь поддерживают секентальные процессы, то есть, когда адаптивные карты обновляются в действии пользователя, и пользователь может пройти через ряд карт, которые требуют ввода пользователя. Это поддерживается с помощью , что позволяет разработчикам-ботам возвращать адаптивные карты в ответ `Action.Execute` на действия пользователя.

Например, возьмем сценарий, в котором кафетерий хочет сделать заказ для команды или канала. Выбор пользователя для различных элементов, таких как еда, напитки и т. д., можно записывать `Action.Execute` последовательно. Пользователь также может проходить по картам по логике, определенной разработчиком бота. <br/>

На следующем изображении показан секентальный рабочий процесс:

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

Пользователь может добиться прогресса в процессе рабочего процесса без изменения карты для других пользователей. Это также полезно для проведения викторин с помощью последовательной адаптивной карты. Как показано на следующем изображении, различные пользователи могут быть на разных этапах рабочего процесса, и они видят различные состояния карты:

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="Состояния бота кейтеринга":::

> [!NOTE]
> Чтобы синхронизировать прогресс пользователя на устройствах, используйте свойство в `refresh` Adaptive Card JSON.

## <a name="sequential-workflow-for-adaptive-cards"></a>Последовательное рабочий процесс для адаптивных карт

В следующем коде приводится пример адаптивных карт:

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "body": [
    {
      "type": "TextBlock",
      "text": "Select from food options"
    },
    { 
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Chicken",
          "verb": "food",
          "data": {
              "item": "chicken"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Beef",
          "verb": "food",
          "data": {
              "item": "beef"
          }
        },
        {
          "type": "Action.Execute",
          "title": "Vegan",
          "verb": "food",
          "data": {
              "item": "vegan"
          }
        }
      ]
    }
  ]
}
```

`Action.Execute`в качестве ответа бот может возвращать адаптивные карты, которые заменяют существующую карту в Teams.
В следующем примере приводится информация о том, что возвращает бот при выборе продуктов питания или напитках или подтверждении заказа:

* При выборе продуктов питания из карточки 1 бот может вернуть карточку для выбора напитков с карточкой 2.
* При выборе напитка из карты 2 бот может вернуть карту подтверждения заказа, которая является карточкой 3.
* При подтверждении заказа с карты 3 бот может вернуть подтвержденную карту заказа, которая является карточкой 4.

## <a name="invoke-request-received-on-bot-side"></a>Вызов запроса, полученного на стороне бота

В следующем коде приводится пример запроса на вызов, полученного на стороне бота:

```JSON
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "", 
      "verb": "food",
      "data": { 
            "item": "vegan"
      } 
    },
    "trigger": "manual" 
  }
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

## <a name="see-also"></a>См. также

* [Действия адаптивной карты в Teams](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)
* [Как работают боты](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)
* [Работа с универсальными действиями для адаптивных карточек](Work-with-universal-actions-for-adaptive-cards.md)
